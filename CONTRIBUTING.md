This provides guidance on how to contribute various content to `hhvm.com`.

## Landing page

Modify `index.md` with your new or updated content.

If you want a `GridBlock` as part of your content, you can do so directly with HTML:

```
<div class="gridBlock">
  <div class="blockElement twoByGridBlock alignLeft">
    <div class="blockContent">
      <h3>HHVM Features</h3>
      <ul>
        <li>The <a href="http://hacklang.org/">Hack Language</a></li>
        <li><a href="http://www.hhvm.com/blog/2027/faster-and-cheaper-the-evolution-of-the-hhvm-jit">JIT Compilation</a></li>
        <li><a href="https://github.com/facebook/hhvm/wiki/Extension-API">HNI</a></li>
        <li><a href="http://docs.hhvm.com/hhvm/basic-usage/proxygen">Proxygen</a> and <a href="http://docs.hhvm.com/hhvm/advanced-usage/fastCGI">FastCGI support</a></li>
        <li><code>hphpd</code> debugger</li>
        <li>... and <a href="http://docs.hhvm.com/hhvm/">more</a></li>
      </ul>
    </div>
  </div>

  <div class="blockElement twoByGridBlock alignLeft">
    <div class="blockContent">
      <h3>The JIT Compiler</h3>
      <p>
        Rather than directly interpret or <a href="https://en.wikipedia.org/wiki/HipHop_for_PHP#History_Before_HHVM">compile PHP code directly to C++</a>, HHVM compiles Hack and PHP into an intermediate bytecode. This bytecode is then translated into <a href="https://en.wikipedia.org/wiki/X64">x64</a> machine code dynamically at runtime by a just-in-time (<a href="https://en.wikipedia.org/wiki/Just-in-time_compilation">JIT</a>) compiler. This compilation process allows for all sorts of optimizations that cannot be made in a statically compiled binary, thus enabling higher performance of your Hack and PHP programs.
      </p>
    </div>
  </div>
</div>
```

or with a combination of changing `./_data/features.yml` and adding some Liquid to `index.md`, such as:

```
{% include content/gridblocks.html data_source=site.data.features imagealign="bottom"%}
```

## Blog

Adding a new blog post is a four-step process.

> Some posts have a `permalink` and `comments` in the blog post YAML header. You will not need these for new blog posts. These are an artifact of migrating the blog from Wordpress to gh-pages.

1. Create your blog post in `./_posts` in markdown (file extension `.md` or `.markdown`). See current posts in that folder or `2016-04-07-blog-post-example.md` for an example of the YAML format. **If the `./_posts` directory does not exist, create it**.
  - You can add a `<!--truncate-->` tag in the middle of your post such that you show only the excerpt above that tag in the main `/blog` index on your page.
1. If you have not authored a blog post before, modify the `./_data/authors.yml` file with the `author` id you used in your blog post, along with your full name and Facebook ID to get your profile picture.
1. [Run the site locally](./README.md) to test your changes. It will be at `http://127.0.0.1/blog/your-new-blog-post-title.html`
1. Push your changes to GitHub.

## Docs

To modify docs, edit the appropriate markdown file in `./_docs`.

To add docs to the site, ....

1. Add your markdown file to the `./_docs` folder. See `./docs-hello-world.md` for an example of the YAML header format. **If the `./_docs` directory does not exist, create it**.
  - You can use folders in the `./_docs` directory to organize your content if you want.
1. Update `_data/nav_docs.yml` to add your new document to the navigation bar. Use the `id` you put in your doc markdown in ad the id in the `_data/nav_docs.yml` file.
1. [Run the site locally](./README.md) to test your changes. It will be at `http://127.0.0.1/docs/your-new-doc-permalink.html`
1. Push your changes to GitHub.

## Header Bar

To modify the header bar, change `./_data/nav.yml`.

## Top Level Page

If you want a top-level page (e.g., http://hhvm.com/top-level.html) -- not in `/blog` or `/docs` -- then you can create a markdown file in the root `./`. See `./top-level-example.md` for more information.

## Other Changes

- CSS: `./css/main.css` or `./_sass/*.scss`.
- Images: `./static/images/[docs | posts]/....`
- Main Blog post HTML: `./_includes/post.html`
- Main Docs HTML: `./_includes/doc.html`
