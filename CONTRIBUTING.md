This provides guidance on how to contribute various content to `hhvm.com`.

## Blog

To modify a blog post, edit the appropriate markdown file in `./_posts/`.

Adding a new blog post is a four-step process.

> Some posts have a `permalink` and `comments` in the blog post YAML header. You will not need these for new blog posts. These are an artifact of migrating the blog from Wordpress to gh-pages.

1. Create your blog post in `./_posts/` in markdown (file extension `.md` or `.markdown`). See current posts in that folder or `./doc-type-examples/2016-04-07-blog-post-example.md` for an example of the YAML format. **If the `./_posts` directory does not exist, create it**.
  - You can add a `<!--truncate-->` tag in the middle of your post such that you show only the excerpt above that tag in the main `/blog` index on your page.
1. If you have not authored a blog post before, modify the `./_data/authors.yml` file with the `author` id you used in your blog post, along with your full name and Facebook ID to get your profile picture.
1. [Run the site locally](./README.md) to test your changes. It will be at `http://127.0.0.1/blog/your-new-blog-post-title.html`
1. Push your changes to GitHub.

## Docs

To modify docs, edit the appropriate markdown file in `./_docs/`.

To add docs to the site....

1. Add your markdown file to the `./_docs/` folder. See `./doc-type-examples/docs-hello-world.md` for an example of the YAML header format. **If the `./_docs/` directory does not exist, create it**.
  - You can use folders in the `./_docs/` directory to organize your content if you want.
1. Update `_data/nav_docs.yml` to add your new document to the navigation bar. Use the `docid` you put in your doc markdown in as the `id` in the `_data/nav_docs.yml` file.
1. [Run the site locally](./README.md) to test your changes. It will be at `http://127.0.0.1/docs/your-new-doc-permalink.html`
1. Push your changes to GitHub.

## Header Bar

To modify the header bar, change `./_data/nav.yml`.

## Top Level Page

To modify a top-level page, edit the appropriate markdown file in `./top-level/`

If you want a top-level page (e.g., http://your-site.com/top-level.html) -- not in `/blog/` or `/docs/`....

1. Create a markdown file in the root `./top-level/`. See `./doc-type-examples/top-level-example.md` for more information.
1. If you want a visible link to that file, update `_data/nav.yml` to add a link to your new top-level document in the header bar.

   > This is not necessary if you just want to have a page that is linked to from another page, but not exposed as direct link to the user.

1. [Run the site locally](./README.md) to test your changes. It will be at `http://127.0.0.1/your-top-level-page-permalink.html`
1. Push your changes to GitHub.

## Other Changes

- CSS: `./css/main.css` or `./_sass/*.scss`.
- Images: `./static/images/[docs | posts]/....`
- Main Blog post HTML: `./_includes/post.html`
- Main Docs HTML: `./_includes/doc.html`
