---
title: "XHP v4: namespaces and updated syntax"
layout: post
author: fred
category: blog
---

Today we are releasing significant changes to XHP - in Hack, HHVM, and in
[the class/function library](https://github.com/hhvm/xhp-lib); **XHP now fully
supports namespaces** - both using XHP from other namespaces, and defining XHP
components in namespaces.

XHP v4 includes several changes to:
- directly support namespaces.
- remove features that would introduce parser ambiguities when combined with
  namespace support.
- remove features that surprise users and can be expressed in other, more
  consistent ways.
- make a clear distinction between 'core' and HTML functionality, to enable
  broader use of XHP in new contexts.
- be consistent with other modern Hack libraries, especially the HSL.

We expect future development of XHP to be focussed on making XHP more consistent
with the rest of Hack, especially from a type system perspective.

# Overview

- XHP classes are now declared as `xhp class foo {}` instead of `class :foo`
- in XHP contexts, the `:` token acts as a namespace separator; `foo:bar` is
  equivalent to `foo\bar` (and `namespace\foo\bar`), and `:foo:bar` is
  equivalent to `\foo\bar`.
- children declarations have been replaced with a trait and are no longer a
  language feature
- categories have been replaced with interfaces
- the XHP class and function library is now namespaced
- `renderAsync()` replaces `asyncRender()` and `render()`

## XHP v3 Example

```
class :foo:bar extends :x:element {
  category %flow;
  children (:div, :code*);

  protected function render(): void {
    return <x:frag>{$this->getChildren());
  }
}
```

## XHP v4 Example

```
namespace foo;

use namespace Facebook\XHP\Core as x;
use namespace Facebook\XHP\ChildValidation as XHPChild;
use type Facebook\XHP\HTML\{div, code};

xhp class bar extends x\element
implements \Facebook\XHP\HTML\Category\Flow {
  use XHPChild\Validation;

  protected static function getChildrenDeclaration(): XHPChild\Constraint {
    return XHPChild\any_of(
      XHPChild\of_type<div>(),
      XHPChild\at_least_one_of(XHPChild\of_type<code>()),
    );
  }

  protected async function renderAsync(): Awaitable<XHPRoot> {
    return <x:frag>{$this->getChildren()}</x:frag>;
    // alternatively:
    return
      <:Facebook:XHP:Core:frag>
        {$this->getChildren()}
      </:Facebook:XHP:Core:frag>;
  }
}
```

# Migration

Automated migrations for all language changes, and for most classes and
functions renamed in xhp-lib v4, are available in
[HHAST 4.64.6 or newer](https://github.com/hhvm/hhast/releases) (some also
available in older HHAST versions).

- `hhast-migrate --add-xhp-children-declaration-method` adds
  the `ChildValidation` trait and `getChildrenDeclaration()` method based on
  existing `children` declarations.
- `hhast-migrate --remove-xhp-child-declarations` (run after the above
  migration) will remove the now redundant `children` declarations.
- `hhast-migrate --demangle-xhp-class-names` replaces `-` in XHP class names
  with `_`
- `hhast-migrate --xhp-class-modifier` migrates `class :foo:bar`
  to `xhp class foo:bar`
- `hhast-migrate --xhp-lib-v3-to-v4` migrates most class and function names
  changed in xhp-lib v4, adds the necessary `use` clauses (this includes all
  HTML tags)

In rare cases, these migrations can result in typechecker errors (e.g. naming
conflicts due to the removal of XHP class name mangling) or hhast-lint errors
(e.g. redundant `use` clauses) which need to be fixed manually.

Additional changes that may require manual migration:

- Consider moving any XHP class declarations from the global namespace into
  namespaces consistent with the rest of your codebase.
- Optionally change `xhp class foo:bar:baz { ... }` to the equivalent
  `namespace foo\bar; xhp class baz { ... }` based on your preferred style.
- Replace `category` declarations with interfaces (new or existing; common ones
  can be found in the `Facebook\XHP\HTML\Category` namespace).
- Calls to `$xhp->toString()` need to be updated to `$xhp->toStringAsync()`.
- Calls to `$xhp->getChildren(...)`, `$xhp->getFirstChild(...)` and other
  methods that had their argument removed need to be updated to
  `$xhp->getChildrenOfType<...>()`, `$xhp->getFirstChildOfType<...>()`, etc.
- Most deprecated features (e.g. attribute clobbering, `forceAttribute`) are not
  handled by the automated migrations, we recommend replacing them with
  equivalent or similar non-deprecated features.

# Details

## Language changes

A [more formal](https://gist.github.com/fredemmott/de7eeb91765b0c98fafac9c591263aca) description of these changes is also available.

### Syntax

Previously, XHP classes were declared with a leading colon, e.g.

```Hack
class :foo:bar {}
```

XHP classes are now declared with the following syntax:
```Hack
namespace foo;

xhp class bar {}
```

This new syntax avoids ambiguities that would otherwise be introduced by the addition of namespace support.

`xhp class foo:bar {}` is also permitted - it is intended to be used:
- by existing codebases, as a migration aid
- as a stylistic preference by codebases that choose to minimize use of namespaces

### Naming

Previously, XHP class names were 'mangled' into a form that meets the usual restrictions for Hack class names; for example, `class :foo:bar-baz {}` actually defined the class `xhp_foo__bar_baz`.

XHP class names are no longer mangled: `xhp class foo` defines the class `foo`, and `xhp class foo:bar` defines the class `foo\bar`; this may cause problems if you are storing or otherwise interacting with `classname<T>` of XHP classes, or storing serialized instances of XHP classes.

This also means that XHP class names must now be valid Hack XHP class names; the most significant effect is that the `-` character is no longer permitted in XHP class names.

### Colons in XHP class types

Colons are now a namespace separator (largely equivalent to `\`), but are only permitted in some contexts:
- in XHP-specific language constructs, such as `xhp class foo:bar`, `<foo:bar>`
- when fully-qualified, in other contexts where qualified names are permitted - for example, `function foo(:bar:baz $_)` is permitted, but `function foo(bar:baz $_)` is not permitted

`\` is not permitted in XHP constructor calls (e.g. `<foo\bar>` is an error), or XHP class declaration names (e.g. `xhp class foo\bar`). It is permitted in parent class references, e.g. `xhp class foo extends bar\baz {}`.

Like `\`, `:` can be used to indicate that a name is fully qualified; for example, `foo\bar` and `foo:bar` both refer to `namespace\foo\bar` (unless there is a relevant `use` statement), and `\foo\bar` and `:foo:bar` both always refer to `\foo\bar`. Similarly, `<foo:bar />` is a reference to `namespace\foo\bar`, and `<:foo:bar />` is now permitted as a reference to `\foo\bar`.

There are several situations where both `\` and `:` are permitted; we recommend that codebases decide on a consistent style; for example, code bases may wish to ban:
- using `:` for anything that is not an XHP class
- using `\` in XHP-specific contexts
- declaring elements in sub-namespaces (e.g. permit `namespace foo { xhp class bar {} }`, but ban `xhp class foo:bar {}`)

## Category Declarations

The `category %foo, %bar` syntax is no longer supported - we recommend using interfaces instead.

They were largely equivalent to interfaces, but without typechecker support; this both increased complexity, and users reasonably assume there was typechecker support.

## Child Declarations

The `children (...)` syntax is no longer supported; XHP-Lib v4 supports a variant of [the approach introduced in v3.1](https://github.com/hhvm/xhp-lib/releases/tag/v3.1.0), however functions have been renamed to `lower_camel_case` for consistency with other common Hack libraries.

## Core APIs

There is now a clean separation between core APIs and HTML-specific APIs; we hope this will lead to more diverse uses of XHP in the future.

Core XHP classes and functions are now in the `Facebook\XHP\Core` namespace; child validation has been moved to `Facebook\XHP\ChildValidation`, and is no longer considered a core feature.

This also includes core elements and base classes; in particular:
- `:x:composable-element` is now `Facebook\XHP\Core\node`
- `:x:element` is now `Facebook\XHP\Core\element`, and `:x:frag` is now `Facebook\XHP\Core\frag`

## HTML Elements

These are now all in the `Facebook\XHP\HTML` namespace; they can be used:
- fully-qualified, e.g. `<:facebook:xhp:html:div>`
- with a `use type`, e.g. `use type Facebook\XHP\HTML\{code, div};` `$_ = <div />`
- with a `use namespace`, e.g. `use namespace Facebook\XHP\HTML as h;` `$_ = <h:div />`

Additionally:
- the categories have been updated to match the specification; in some cases, this has meant removing categories, which may mean markup must be restructured to be valid
- the categories are now interfaces in the `Facebook\XHP\HTML\Category` namespace

## Other changes

- `HasXHPAttributeClobbering_DEPRECATED` has been removed; use attribute splat instead
- `UnsafeAttributeValue` has been renamed to `UnsafeAttributeValue_DEPRECATED` as it bypassing the type system by design, and will need to be removed in a future release
- `forceAttribute()` has been renamed to `forceAttribute_DEPRECATED()` as it bypassing the type system by design, and will need to be removed in a future release
- it is now an error to render an element twice, or to mutate it after it has been rendered
- `asyncRender()` has been renamed to `renderAsync()`, for consistency with other popular Hack projects and the HSL
- `render()` has been removed; always use `renderAsync()` instead.
- the `XHPRoot` interface and `:xhp` classes have been removed as unnecessary; use `Facebook\XHP\Core\Node` or `XHPChild` instead.
- removed selectors from `getFirstChild()` and related functions; added `getFirstChildOfType<T as XHPChild>()` with improved typechecker support. An interface can be specified to replace previous category specifications.

## Thanks

It has been a very long path to get here, and much more involved than we
expected. I'd like to thank [our friends at Slack](https://slack.engineering) -
especially [Johan Oskarsson](https://github.com/johanoskarsson) - who made this
possible, and also [Lexidor Digital](https://github.com/lexidor) whose
contributions to type safety are greatly appreciated.
