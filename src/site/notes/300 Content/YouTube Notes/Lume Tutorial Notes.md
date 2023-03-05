---
{"dg-publish":true,"permalink":"/300-content/you-tube-notes/lume-tutorial-notes/"}
---

- Make a website tutorial for Lume, the SSG that runs on Deno. 

# Script 
- Welcome to the my channel! Today I am recording my first tutorial and I am excited to bring you Lume, a static site generator for Deno - the easiest and most secure JavaScript runtime
	- I love Deno - it really is the best developer experience
		- No installing dependencies 
		- Runtime that's basically just like the web and uses browser apis that work on the server
		- There's Typescript out of the box, built in linting, code formatting, self-contained executable test runners, IDE integrations just to name a few
		- Hass free demployment wiht Deno Deploy
		- Fastest JavaScript web server ever built
		- Very secure with no I/O access and great for running untrusted code and auditing new third party code
		- And now you can even install NPM packages safely with less worry
	- Currently using it:
		- Slack 
		- Netlify 
		- GitHub
		- Supabase
	- ## Lume 
		- Inspired by Jekyll, Hugo, and Eleventy - but it's easier to use and configure with more flexibility
		- Supports multiple file formats like markdown, yaml, JavaScript, typescript, jsx and nunjucks
		- dHookk processors to manipulate html and assets like css or js
		- ## Installation
		- To get started
```
deno run -Ar https://deno.land/x/lume/init.ts
```
- Install the Lume CLI Script with:
```

deno install --allow-run --name lume --force --reload  https://deno.land/x/lume_cli/mod.ts
```
- lune init initializes in current directory

- creates:
	-   `_config.ts` or `_config.js`: The [Lume configuration file](https://lume.land/docs/configuration/config-file/), where you can customize the site build.
	- `deno.json`: The [Deno's configuration file](https://deno.land/manual/getting_started/configuration_file). It includes the path of the import map file and some tasks to run Lume. You can also configure other features of Deno like TypeScript, formatter, linter, etc.

	-   `import_map.json`: The [import map file](https://deno.land/manual/node/import_maps#using-import-maps) with the import URL of Lume. Here you can add the dependencies of your project and update Lume by editing the version number.
- ## Start server and build
	- `deno task serve`
	- ## Runs lume and open local web server
	- `deno task lume` 

## Config options I'll use (maybe)

```
const site = lume({
	src: "./src",
})
```

# Tutorial

- We'll just start with a basic markdown file to make sure things are working 
- Ok now we can create a quick layout to make our page include meta tags and all tha tlovely jazz
```
<!DOCTYPE html> 
<html lang="en"> 
<head> 
	<meta charset="UTF-8"> 
	<title>My first page</title> 
</head> 
	<body> 
		{{ content | safe }} 
	</body> 
</html>
```
- Go ahead and assign it to the page
- ## adding data
	- One way to do it is by including it in your front matter
```
---
layout: layout.njk
title: Website of the year
---
# My webbie website

Hello world whatsup
```
- we can also access it in our layout so add it in your


```
<!DOCTYPE html> 
<html lang="en"> 
<head> 
	<meta charset="UTF-8"> 
	<title>{{ title }}</title> 
</head> 
	<body> 
		{{ content | safe }} 
	</body> 
</html>
```
# Shared Data
- we can create a `_data.yml` file
```
layout: layout.njk
```

## Trying out page formats
```
--- 
title: Welcome to my page 
layout: layout.njk links: 
  - text: My Twitter 
    url: https://twitter.com/misteroom 
    - text: My GitHub profile 
      url: https://github.com/oscarotero 
--- 
<article> 
	<header> 
		<h1>{{ title }}</h1> 
	</header> 
	<ul> 
		{% for link in links %} 
		<li> 
			<a href="{{ link.url }}"> {{ link.text }} </a> 
		</li> 
		{% endfor %} 
	</ul> 
</article>
```
tHAT SAME one in javascript:

```
export const title = "Welcome to my page"; 
export const layout = "layout.njk"; 
export const links = [ 
{ 
text: "My Twitter", 
url: "https://twitter.com/misteroom" 
}, { 
text: "My GitHub profile", 
url: "https://github.com/oscarotero" 
} 
]; 
export default function ({ title, links }) { 
return ` 
<article> 
<header> 
<h1>${ title }</h1> 
</header> 
<ul> 
${ links.map((link) => 
`<li><a href="${ link.url }">${ link.text }</a></li>` 
).join("") } 
</ul> 
</article>`; 
}
```

## [Page date](https://lume.land/docs/creating-pages/page-files/#page-date)

All pages have a `date` variable with the file creation date. This value can be used to order the pages (in a blog, for example). If you want to define a different date, you can prepend it to the filename using the `yyyy-mm-dd` syntax followed by an underscore `_` (or `yyyy-mm-dd-hh-ii-ss` if you also need the time). Note that this part is removed in generating the final url:

```txt
.
├── index.md                          => /index.html
└── posts
    └── 2020-06-21_hello-world.md     => /posts/hello-world/index.html
    └── 2020-06-22_my-second-post.md  => /posts/my-second-post/index.html
```

Dates can be defined in folders, so it's shared by all pages inside:

```txt
.
├── index.md                          => /index.html
└── posts
    └── 2020-06-21_hello-world/
        └── index.md     => /posts/hello-world/index.html
        └── other.md     => /posts/hello-world/other/index.html
```
# Page data

Assign custom data to the pages

1.  [Standard variables](https://lume.land/docs/creating-pages/page-data/#standard-variables)
    -   [url](https://lume.land/docs/creating-pages/page-data/#url)
    -   [date](https://lume.land/docs/creating-pages/page-data/#date)
    -   [layout](https://lume.land/docs/creating-pages/page-data/#layout)
    -   [tags](https://lume.land/docs/creating-pages/page-data/#tags)
    -   [templateEngine](https://lume.land/docs/creating-pages/page-data/#templateengine)
    -   [renderOrder](https://lume.land/docs/creating-pages/page-data/#renderorder)
    -   [mergedKeys](https://lume.land/docs/creating-pages/page-data/#mergedkeys)

Pages can contain arbitrary data. In Markdown files, the data is defined in the **front matter** block, a block delimited by two triple-dashed lines containing [YAML](https://yaml.org/) code. There are other formats that can have front matter or store the data in different ways. Let's see some examples:

-   page.md
-   page.yml
-   page.njk
-   page.json
-   page.tmpl.js

```yaml
title: This is the title
url: custom-url.html
content: This is the page content
```

In the examples above, all pages contain two variables: `title` and `url`.

In the formats with front matter (like Markdown and Nunjucks), the content is defined below the front matter. Formats that don't use front matter export the content as the `content` variable or, optionally, as a default export (like in `page.tmpl.js`).

## [Standard variables](https://lume.land/docs/creating-pages/page-data/#standard-variables)

There are some special variables that **Lume** understands:

### [url](https://lume.land/docs/creating-pages/page-data/#url)

The `url` variable contains the public URL of the page, useful to create links and configure the output filename. If it doesn't exist, it's generated automatically by lume. See [URL docs](https://lume.land/docs/creating-pages/urls/)

### [date](https://lume.land/docs/creating-pages/page-data/#date)

If it's not defined, Lume automatically uses the file creation date. This variable can be defined in the filename [See Page date](https://lume.land/docs/creating-pages/page-files/#page-date) or in the front matter. The accepted values are:

-   Any `IS0 8601` compatible date, like `2021-01-01`, `2021-01-01 03:10:10`, `2021-01-01T03:10:10Z`, `2021-01-01Y03:10:10-0700`, etc.
-   The special value `Git Created` to get the first time this file was added to the Git history. It uses the creation date as fallback.
-   The special value `Git Last Modified` to get the last time this file has changed in the Git history. It uses the last modified date as fallback.

### [layout](https://lume.land/docs/creating-pages/page-data/#layout)

To define the layout that is used to render the page. See [Layouts](https://lume.land/docs/creating-pages/layouts/) for more info.

### [tags](https://lume.land/docs/creating-pages/page-data/#tags)

Tags are used to group pages. See [Tags](https://lume.land/docs/creating-pages/tags/)

### [templateEngine](https://lume.land/docs/creating-pages/page-data/#templateengine)

To override the template engine used to render the page. See [Template engine](https://lume.land/docs/core/multiple-template-engines/)

### [renderOrder](https://lume.land/docs/creating-pages/page-data/#renderorder)

To customize the order in which the page is rendered. See [Render Order](https://lume.land/docs/core/render-order/)

### [mergedKeys](https://lume.land/docs/creating-pages/page-data/#mergedkeys)

To customize how some data is merged. See [Merged Keys docs](https://lume.land/docs/core/merged-keys/)

-   Front matter
-   JavaScript
-   JavaScript (alternative)

```yaml
---
url: /welcome.html
date: 2021-01-01
layout: layouts/post.njk
draft: true
tags: post
---
```
# Shared Data

In addition to the variables defined in the pages and layouts, you can store data accessible by some or all pages. Shared data must be saved in the `_data` directory or `_data.*` files with extensions like `.json`, `.yaml`, `.js` or `.ts`.

The formats `.json` and `.yaml` are useful for static data. `.js` and `.ts` fit better for dynamic data (for example, data fetched from an API or a database):

-   _data.json
-   _data.yml
-   _data.ts

```json
{
  "people": [
    {
      "name": "Oscar Otero",
      "color": "black",
    },
    {
      "name": "Laura Rubio",
      "color": "blue",
    },
  ]
}
```

## [The `_data.*` files](https://lume.land/docs/creating-pages/shared-data/#the-_data.*-files)

Any file named as `_data.*` is loaded and its content is accessible by all pages in the same directory or subdirectory.

```sh
├── _data.yaml      # Data shared with all pages
├── index.md
└── documentation
    └── _data.json  # Shared with pages in this directory and subdirectories
    └── doc1.md
    └── doc2.md
    └── examples
        └── _data.json  # Shared with pages in this directory and subdirectories
        └── example1.md
        └── example2.md
```

As you can see, the shared data is propagated in a cascade following the directory structure. A typical use case is to store those variables that are common to all pages in the same directory so you don't have to repeat it for every page.

## [The `_data` directories](https://lume.land/docs/creating-pages/shared-data/#the-_data-directories)
`_data` directories are similar to `_data` files, but instead of using only one file, the data is stored in several files inside that directory. The _basename_ of each file determines the variable name used to access the data. Let's see an example:

```txt
└── _data
    └── users.json
    └── documents
        └── one.js
        └── two.js
        └── three.js
```

In this example, the data stored in the file `_/data/users.json` can be accessed via `users` variable and documents via `documents.one`, `documents.two` and `documents.three`. To use this data in your pages:
-   page.njk
-   page.jsx

```html
<h2>Documents</h2>

<ul>
{% for doc in documents %}
  <li>
      {{ doc.title }}
  </li>
{% endfor %}
</ul>
```

Like `_data.*` files, you can have `_data` directories in different locations so they are shared only with all pages in the same directory or subdirectories.
# Tags

Use tags to group and organize pages

1.  [Tags in _data](https://lume.land/docs/creating-pages/tags/#tags-in-_data)

You can assign one or multiple tags to pages using the `tags` variable. Tags allows you to group content in interesting ways.

For example, in a blog site, you may want to group posts of different categories:

```yaml
---
title: The history of the static site generators
tags:
  - post
  - ssg
---
```

This post has two tags, one used to identify the type of page (post) and another with the topic (ssg). To collect all pages tagged as `post` in the layouts, use the `search` object:

```html
<ul>
  {% for post in search.pages("post") %}
  <li>{{ post.data.title }}</li>
  {% endfor %}
</ul>
```

And to get all pages tagged as `post` and `ssg` add the two tags names separated with a space:

```html
<ul>
  {% for post in search.pages("post ssg") %}
  <li>{{ post.data.title }}</li>
  {% endfor %}
</ul>
```

## [Tags in `_data`](https://lume.land/docs/creating-pages/tags/#tags-in-_data)

Unlike other values, when you define `tags` in a `_data.*` file and in the pages, the value is not overridden, but aggregated. In other words: the page will have all tags defined in `_data.*` **and** in the page. In the previous example, instead of assigning the "post" tag to all pages manually, you could define it in a `_data.*` file in the directory where all posts are stored and use the front matter to assign the other tags individually.

## [The `url` variable](https://lume.land/docs/creating-pages/urls/#the-url-variable)

The variable `url` defined in a page allows customizing the output file individually. For example:

```yml
---
title: My first post
url: /posts/welcome/
---
```

In this example, the `url` value changes the output file name:

```txt
/posts/my-first-post.md  =>  /posts/welcome/index.html
```

Note that manually defining the URL of a page means that the `prettyUrls` option **won't have any effect.** For example:

```yml
# Use a trailing / to create pretty urls.
# For example, this outputs /posts/welcome/index.html
url: /posts/welcome/

# This outputs /posts/welcome (a file without extension)
url: /posts/welcome

# This outputs /posts/welcome.html
url: /posts/welcome.html
```

## [Relative URLs](https://lume.land/docs/creating-pages/urls/#relative-urls)

If you only want to change the last part of the URL, you can use relative paths. For example:

```yml
---
title: My first post
url: ./welcome/
---
```

In this example, the page will be saved using the directory path where the source file is saved but adding `welcome` in the last part of the URL.

```txt
/posts/my-first-post.md  =>  /posts/welcome/index.html
```

Using `../welcome/` as URL will also remove the last directory.

```txt
/posts/my-first-post.md  =>  /welcome/index.html
```

## [URLs as functions](https://lume.land/docs/creating-pages/urls/#urls-as-functions)

The variable `url` also accepts a function to generate the final value dynamically. This function has the current page object as the first argument.

For example, let's say that we want to automatically generate all URLs of our posts using the title value. We can create a `_data.js` file in the `/posts/` directory with the following code:

```js
export function url(page) {
  return `./${page.data.title}/`;
}
```

Now, all pages in this directory share the same `url` function. The function returns the title of the page as a relative URL, for example ,`./My first post/` (See [Shared data](https://lume.land/docs/creating-pages/shared-data/)).

Because the URL is relative, the current directory is appended automatically (it will be resolved to `/post/My first post/`). And if you are using the `slugify_urls` plugin, all output paths are slugified automatically, so the final URL would be `/post/my-first-post/`.

Using functions as URLs gives a lot of flexibility to generate the URLs as you want.

## [Setting url to `false`](https://lume.land/docs/creating-pages/urls/#setting-url-to-false)

Setting the `url` variable to `false` prevents the page being saved into the dest folder (although it is still visible by other pages, for example, in paginations).

```yml
---
title: This is a title
url: false # Don't output this page yet
---
```

# General Concepts

The way Lume works is simple: it just read files in your `src` directory, process the content and save the final files into the `dest` folder.

There are different types of files:

## [Page files](https://lume.land/docs/core/concepts/#page-files)

A page file is a file that is loaded, processed and saved to the `dest` folder generating one or more pages. In Lume, there are two different types of pages:

### [Regular pages](https://lume.land/docs/core/concepts/#regular-pages)

Are files intended to generate HTML pages. Let's take `my-page.md` as an example:

1.  Load the content of the file.
2.  Change the output file from `/my-page.md` to `/my-page/index.html`.
3.  Run preprocessors
4.  Render the page content and layouts
5.  Run processors
6.  Save the output file as `/my-page/index.html`.

By default, Lume interprets the following formats as regular page files, so they are loaded, processed and exported to `dest` folder: `.md`, `.njk`, `.tmpl.json`, `.tmpl.js`, `.tmpl.ts` and `.yaml`. Use `site.loadPages()` to add additional extensions:
### [Asset pages](https://lume.land/docs/core/concepts/#asset-pages)

Are pages intended to output assets, like `.css` files, `.js` or images. They are very similar to regular pages but with a couple of differences. Let's take `my-styles.css` as an example:

1.  Load the content of the file.
2.  Run preprocessors
3.  Run processors
4.  Save the output file as `/my-styles.css`.

Lume doesn't load any asset by default. Use the function `site.loadAssets()` to configure Lume to load some extensions as page assets. For example:
## [Data files](https://lume.land/docs/core/concepts/#data-files)

Data files are the files saved as `_data.*` or in `_data/` directories and contain data shared to the page files. The following files are interpreted as data files: `_data.yaml`, `_data.ts`, `_data.js`, `_data.json`. If you want to load additional data formats, use `site.loadData()` function:
## [Static files](https://lume.land/docs/core/concepts/#static-files)

They are files that are exported to the `dest` folder but don't need to be processed, so Lume doesn't load the content, only copies them. They are copied as is using the `site.copy()` function. [See more about copy](https://lume.land/docs/configuration/copy-static-files/).

## [Includes](https://lume.land/docs/core/concepts/#includes)

Are files loaded by the pages, for example, the layouts or templates. By default, they are placed in the `_includes` folder, but you can configure it.
## [Components](https://lume.land/docs/core/concepts/#components)

By default are saved in the `_components` folder and store reusable pieces of code that you can use in your templates. You can load additional components with `site.loadComponents()` function. [See more about components](https://lume.land/docs/core/components/)

Components are template pieces that you can use in other templates. Some template engines like Nunjucks, Pug or Liquid have ways to reuse codes (like includes, macros, etc). The Lume components have the following advantages:

-   They are template engine agnostic. For example, you can create your components in JSX or JavaScript and use them in Nunjucks.
-   They can generate not only the HTML code but also the CSS and JavaScript code needed on the client side.
-   They are automatically available everywhere; no need to import them manually.
-   For module-based components (like JavaScript, TypeScript, JSX or TSX) it's the only way to hot-reload components without stopping and restarting the local server.
- ## [Create your own components](https://lume.land/docs/core/components/#create-your-own-components)

Components are stored in the `_components` directory. Like with `_data`, you can create `_components` directories in different sub-directories to make them available only to specific pages. To create a new component, just create a file in this directory with the name of your component and the extension of the template engine you want to use. For example, a component in Nunjucks that renders a button could be stored in `_components/button.njk`:

```html
<button class="button">{{ text }}</button>
```

This component is available in your layouts under the `comp` variable (you can configure a different variable name in `_config.ts`). It's a global variable that contains all components. In our example, we can render the button component with the `comp.button()` function:

```html
<h1>Welcome to my site.</h1>
{{ comp.button({ text: "Login" }) | safe }}
```

Note that the component accepts an object with the properties. This component is available in any other template engine. For example, JavaScript:

```js
export default function ({ comp }) {
  return `
  <h1>Welcome to my site.</h1>
  ${comp.button({ text: "Login" })}
`;
}
```

Eta templates:

```html
<h1>Welcome to my site.</h1>
<%= comp.button({ text: "Login" }) %>
```

Lume components can be used like React components if you're using the JSX plugin:

```jsx
export default function ({ comp }) {
  return (
    <>
      <h1>Welcome to my site.</h1>
      <comp.Button text="Login" />
    </>
  );
}
```

### [Nested components in Nunjucks](https://lume.land/docs/core/components/#nested-components-in-nunjucks)

In Nunjucks you can nest components in this way:

```html
{% comp "Container" %}
  Content of the Container component

  {% comp "Button" %}
  This is a button inside the Container component
  {% endcomp %}
{% endcomp %}
```

The content of the components are passed in the `content` key:

-   _components/container.njk
-   _components/button.njk

```html
<section class="container">{{ content | safe }}</section>
```

## [Component assets](https://lume.land/docs/core/components/#component-assets)

Components can export CSS and JS code. To do that, the component needs to export `css` or `js` variables.

In our example, we may want to apply some styles to the button. In a Nunjucks template, the way to export data is using a front matter:

```html
---
css: |
  .button {
    background-color: blue;
    color: white;
  }
---
<button class="button">{{ text }}</button>
```

This CSS code will be exported in your `dest` folder in the `/components.css` file together with the CSS code of other used components. Note that if the component is not used, the CSS code won't be exported. This is an interesting feature that allows having a library of many components and only exporting the CSS and JS code that you only need.

## [Organize your components](https://lume.land/docs/core/components/#organize-your-components)

Components can be saved in subdirectories. For example, the `button` component could be saved in the `ui` subdirectory (`_components/ui/button.njk` in your `src` folder). In this case, you can access this component with `comp.ui.button()`.

## [Components inside components](https://lume.land/docs/core/components/#components-inside-components)

Components can use other components internally. Let's say we want to create the `search` component that uses `button` internally. Let's see an example using a JS template:

```js
// _components/search.js

export const css = `
.search {
  background: gray;
  padding: 20px;
}
`;

export const js = `
import from "js/search.js"
`;

export default function ({ comp }) {
  return `
<form class="search">
  <label>
    Search:
    <input type="search" name="q">
  </label>
  ${comp.button({ text: "Submit" })}
</form>
`;
}
```

In this example, the component exports CSS and JS code in addition to the HTML code.

## [Register components from the _config file](https://lume.land/docs/core/components/#register-components-from-the-_config-file)

In addition to the `_components` folder, you can register components dynamically in the `_config` file with the function `site.component()`. This function takes two arguments: the component context and the component object:

```ts
site.component("ui", {
  name: "button",
  css: ".btn { background: blue; color: white }",
  render({ text }) {
    return `<button class="btn">${text}</button>`;
  },
});
```

Now, you can use the component as always:

```html
{{ comp.ui.button({ text: "Login" }) | safe }}
```

## [Plugins](https://lume.land/docs/core/concepts/#plugins)

Everything in Lume is a plugin. Even the support of core formats like `.md`, `.yaml`, `.json` etc is provided by some [plugins that **enabled by default**](https://lume.land/plugins/?status=enabled)

# Create multiple pages

Generators allows to create multiple pages from an unique source file

1.  [Basic example](https://lume.land/docs/core/multiple-pages/#basic-example)
2.  [Multiple pages with layouts](https://lume.land/docs/core/multiple-pages/#multiple-pages-with-layouts)
3.  [Generate pages from other sources](https://lume.land/docs/core/multiple-pages/#generate-pages-from-other-sources)

It's possible with Lume to generate more than one page from the same source file. This is useful to generate pages programmatically using an external source like a database or an API.

## [Basic example](https://lume.land/docs/core/multiple-pages/#basic-example)

To generate pages the source file must return a [generator function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*). Every element yielded by the generator is a new page and must contain, at least, the `url` property.

```js
export default function* () {
  yield {
    url: "/page-1/",
    content: "This is the first page",
  };
  yield {
    url: "/page-2/",
    content: "This is the second page",
  };
  yield {
    url: "/page-3/",
    content: "This is the third page",
  };
}
```

In the example above, this page generates three pages. It's important that the URLs of the pages be unique.

## [Multiple pages with layouts](https://lume.land/docs/core/multiple-pages/#multiple-pages-with-layouts)

Every page is an object with the page data. In the previous example, every page has the `url` and `content` properties,to define the content and URL of every page. If you want to use a layout to generate the page content, you have to export the `layout` keyword with the layout name and the data that will be used in the layouts:

-   pages.tmpl.js
-   _includes/layouts/article.njk

```js
export default function* () {
  yield {
    url: "/page-1/",
    layout: "layouts/article.njk",
    title: "Article 1",
    body: "Welcome to the article 1"
  };
  yield {
    url: "/page-2/",
    layout: "layouts/article.njk",
    title: "Article 2",
    body: "Welcome to the article 2"
  };
  yield {
    url: "/page-3/",
    layout: "layouts/article.njk",
    title: "Article 3",
    body: "Welcome to the article 3"
  };
}
```

Because the layout is the same for all pages, we can use a named export to define it once instead of duplicating it in every yielded page:

-   pages.tmpl.js
-   _includes/layouts/article.njk

```js
export const layout = "layouts/article.njk";

export default function* () {
  yield {
    url: "/page-1/",
    title: "Article 1",
    body: "Welcome to the article 1"
  };
  yield {
    url: "/page-2/",
    title: "Article 2",
    body: "Welcome to the article 2"
  };
  yield {
    url: "/page-3/",
    title: "Article 3",
    body: "Welcome to the article 3"
  };
}
```

## [Generate pages from other sources](https://lume.land/docs/core/multiple-pages/#generate-pages-from-other-sources)

This simple concept of using generators to generate pages is very flexible and can be used for many use cases. For example, we can generate pages from a Database or an API:

```js
import database from "./my-database.ts";

export const layout = "layouts/article.njk";

export default function* () {
  const articles = database.query("select * from articles");

  for (const article of articles) {
    yield {
      url: `/articles/${article.slug}/`,
      ...article,
    };
  }
}
```

In this example, we use a database to get all articles and a generator to generate a new page per article. Each yielded article contains the URL and other properties you like (title, category, tag, body, etc.). We are exporting the `layout` value so all pages will use the same layout to render.

Another common use case is for pagination. Go to [Search and paginate](https://lume.land/docs/core/searching/) for more info.
# Search and paginate

Using the search and paginate helper to create dynamic pages.

1.  [Searching pages](https://lume.land/docs/core/searching/#searching-pages)
2.  [Pagination](https://lume.land/docs/core/searching/#pagination)

The variables `search` and `paginate` are global functions that allow searching other pages and paginating the result.

## [Searching pages](https://lume.land/docs/core/searching/#searching-pages)

The function `search.pages()` returns an array of pages you can filter and sort. For example, to search pages having the variable `category` set to `music`, use the following code:

```html
<ul>
  {% for page in search.pages("category=music") %}
  <li>{{ page.data.title }}</li>
  {% endfor %}
</ul>
```

Each `page` is an object with all info related with this page. The property `data` contains all data assigned to this page (like variables in the front matter, or in the _data.* files). In the example above, we use the title of every page to build the list.

The `search` helper is very powerful and has more interesting features. [Go to the Search plugin documentation](https://lume.land/plugins/search/) for more info.

## [Pagination](https://lume.land/docs/core/searching/#pagination)

You can combine the `search` helper with `paginate` helper to group the result under different pages. For example:

```js
export const layout = "layouts/post-list.njk";

export default function* ({ search, paginate }) {
  const musicPages = search.pages("category=music");
  const pagination = paginate(musicPages);

  for (const page of pagination)) {
    yield page;
  }
}
```

[Go to the Paginate plugin documentation](https://lume.land/plugins/paginate/) to see more info and available configuration.
# Server

Set up a server for your site.

1.  [Events](https://lume.land/docs/core/server/#events)
2.  [Middlewares](https://lume.land/docs/core/server/#middlewares)
    -   [basic_auth](https://lume.land/docs/core/server/#basic_auth)
    -   [cache_busting](https://lume.land/docs/core/server/#cache_busting)
    -   [expires](https://lume.land/docs/core/server/#expires)
    -   [logger](https://lume.land/docs/core/server/#logger)
    -   [no_cache](https://lume.land/docs/core/server/#no_cache)
    -   [not_found](https://lume.land/docs/core/server/#not_found)
    -   [on_demand](https://lume.land/docs/core/server/#on_demand)
    -   [redirects](https://lume.land/docs/core/server/#redirects)
    -   [reload](https://lume.land/docs/core/server/#reload)
    -   [www](https://lume.land/docs/core/server/#www)

Lume includes a `Server` class used to start a local HTTP server when running `lume --serve`. You can use this class to start your own server, for example, to serve the static files in **Deno Deploy**. Let's see a basic example of a server:

```ts
import Server from "https:/deno.land/x/lume/core/server.ts";

const server = new Server({
  port: 8000,
  root: `${Deno.cwd()}/_site`,
});

server.start();

console.log("Listening on http://localhost:8000");
```

This code starts a local server on the port `8000` and serves the static files in the `_site` folder.

## [Events](https://lume.land/docs/core/server/#events)

You can assign event listeners to the server:

```ts
server.addEventListener("start", () => {
  console.log("Server started successfully");
});
```

## [Middlewares](https://lume.land/docs/core/server/#middlewares)

To customize how the server handles the requests and responses, there's a simple middleware system with the following signature:

```js
server.use(async (request, next) => {
  // Here you can modify the request before being passed to next middlewares
  const response = await next(request);

  // Here you can modify the response before being returned to the previous middleware
  return response;
});
```

The request and response objects are standard [`Request`](https://developer.mozilla.org/docs/Web/API/Request) and [`Response`](https://developer.mozilla.org/docs/Web/API/Response) classes, no magic here.

Lume provides some middlewares for common use cases:

```ts
import Server from "https:/deno.land/x/lume/core/server.ts";
import expires from "https:/deno.land/x/lume/middlewares/expires.ts";

const server = new Server({
  port: 8000,
  root: `${Deno.cwd()}/_site`,
});

server.use(expires());

server.start();

console.log("Listening on http://localhost:8000");
```

### [basic_auth](https://lume.land/docs/core/server/#basic_auth)

Implements the [basic access authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) method to access to the site:

```js
server.use(basicAuth({
  users: {
    "user": "password",
  },
}));
```

### [cache_busting](https://lume.land/docs/core/server/#cache_busting)

Cache busting is a way to tell the browser that some static files like CSS styles or JavaScript code have changed, in order to use the new version instead of the locally cached version. It consists of including the number version in the file path. For example `/styles.css` becomes `/v234/styles.css`. [More info](https://www.keycdn.com/support/what-is-cache-busting).

This middleware implements cache busting, so all requests with paths starting with `/v{numbers}` will remove this part so the real file will be served.

### [expires](https://lume.land/docs/core/server/#expires)

It's a middleware to include the `Expires` header in the response for better caching. See the [available options in Deno Doc](https://doc.deno.land/https://deno.land/x/lume/middlewares/expires.ts/~/Options).

### [logger](https://lume.land/docs/core/server/#logger)

To show in the console the HTTP requests/responses served. It's used by Lume in the `--serve` mode.

### [no_cache](https://lume.land/docs/core/server/#no_cache)

Modify the responses to disable the browser cache. It's used by Lume in the `--serve` mode.

### [not_found](https://lume.land/docs/core/server/#not_found)

To show a not-found page on 404 errors. Optionally it can create a directoryIndex for folders. It's used by Lume in the `--serve` mode. See the [available options in Deno Doc](https://doc.deno.land/https://deno.land/x/lume/middlewares/not_found.ts/~/Options).

### [on_demand](https://lume.land/docs/core/server/#on_demand)

To build and serve dynamic pages on demand. See the [available options in Deno Doc](https://doc.deno.land/https://deno.land/x/lume/middlewares/on_demand.ts/~/Options).

### [redirects](https://lume.land/docs/core/server/#redirects)

Middleware to configure a list of redirects of some paths. Example:

```js
server.use(redirects({
  redirects: {
    "/from/": "/to/",
    "/from2/": "/to2/",

    // Use an object to configure the status code. (301 by default)
    "/from3/": {
      to: "/to2/",
      code: 302,
    },
  },
}));
```

### [reload](https://lume.land/docs/core/server/#reload)

To implement a live-reload in the browser after file changes. It's used by Lume in the `--serve` mode. See the [available options in Deno Doc](https://doc.deno.land/https://deno.land/x/lume/middlewares/reload.ts/~/Options).

### [www](https://lume.land/docs/core/server/#www)

This middleware redirects from `www.` domains to non-www domain (or viceversa).

```js
server.use(www({
  add: false, // false to remove, true to add it.
}));
```

See the [available options in Deno Doc](https://doc.deno.land/https://deno.land/x/lume/middlewares/www.ts/~/Options).

# Scripts

A guide to use Lume as a script runner

1.  [Running multiple commands](https://lume.land/docs/core/scripts/#running-multiple-commands)
2.  [Compose scripts](https://lume.land/docs/core/scripts/#compose-scripts)
3.  [Custom functions](https://lume.land/docs/core/scripts/#custom-functions)
4.  [Running scripts from JavaScript](https://lume.land/docs/core/scripts/#running-scripts-from-javascript)

Lume includes a simple script runner that you can use to execute commands or custom functions. To create a new script, use the function `script()` in your `_config.js` file:

```js
site.script("deploy", "rsync -r _site/** user@server.com:/var/www/");
```

Now, you can run this script from the CLI with `lume run deploy`.

## [Running multiple commands](https://lume.land/docs/core/scripts/#running-multiple-commands)

You can create a script to execute multiple commands, **one after another.** There are two ways to do that: by adding more arguments or joining the different commands with `&&`. For example:

```js
site.script(
  "save-site",
  "gzip -r _site site.gz",
  "scp site.gz user@host.com:/home/user/archive",
);

// Alternative way using "&&"
site.script(
  "save-site",
  "gzip -r _site site.gz && scp site.gz user@host.com:/home/user/archive",
);
```

Now, by running `lume run save-site`, these two commands will be executed.

If you don't need to execute the commands in series but in **parallel**, use an array of commands or the character `&`:

```js
site.script(
  "compress-assets",
  [
    "gzip -r _site/images images.gz",
    "gzip -r _site/videos videos.gz",
  ],
);

// Alternative way using the character "&"
site.script(
  "compress-assets",
  "gzip -r _site/images images.gz & gzip -r _site/videos videos.gz",
);
```

## [Compose scripts](https://lume.land/docs/core/scripts/#compose-scripts)

Scripts can execute other scripts: just use the name of a registered script as a command in another script. For example:

```js
// Create two scripts
site.script("compress", "gzip -r _site site.gz");
site.script("upload", "scp site.gz user@host.com:/home/user/archive");

// Create a third script that runs the two previous scripts
site.script("compress-and-upload", "compress", "upload");
```

## [Custom functions](https://lume.land/docs/core/scripts/#custom-functions)

Scripts not only can execute CLI commands but also JavaScript functions. For example:

```js
site.script("add-date-published", () => {
  Deno.writeTextFileSync(
    site.dest("published.txt"),
    `Site published at: ${Date.now()}`,
  );
});
```

## [Running scripts from JavaScript](https://lume.land/docs/core/scripts/#running-scripts-from-javascript)

To run a script from JavaScript instead of the CLI, use the `site.run()` function:

```js
// Create the script
site.script("compress", "gzip -r _site site.gz");

// Run it
site.run("compress");
```

# Merged keys

Configure how the data is merged

1.  [Object mode merging](https://lume.land/docs/core/merged-keys/#object-mode-merging)
2.  [array mode](https://lume.land/docs/core/merged-keys/#array-mode)
3.  [stringArray mode](https://lume.land/docs/core/merged-keys/#stringarray-mode)

As explained in [Shared data](https://lume.land/docs/creating-pages/shared-data/), the data assigned to every page is the result of merging the data directly assigned to the page (like the front matter) with the data of the parent folders (stored in the `_data` files and folders).

```txt
├── _data.yaml
├── ...
└── documents
    └── _data.json
    └── ...
    └── examples
        └── _data.json
        └── my-page.md
```

In this example the `/documents/examples/my-page.md` file contains all data from the page front matter, merged with the data from `/documents/examples/_data.json`, `documents/_data.json` and `/_data.yaml` files, **in this order of priority**.

## [Object mode merging](https://lume.land/docs/core/merged-keys/#object-mode-merging)

On merging variables, **the complete value is overridden**. But you may want to merge some values in a different way. For example, let's say we have the following two data files, one in the root and the other in a subfolder. Both files have a `site` variable with different values:

-   /_data.yml
-   /subfolder/_data.yml

```yml
site:
  title: My humble site
  author: Oscar Otero
```

All pages in the subfolder (and sub-subfolders) will have the latest version of the variable that has the `author` subkey but missing the `title` value, because the whole variable is overridden. You can change this behaviour using the special value `mergedKeys`. This value indicates to Lume how to merge some keys:

-   /_data.yml
-   /subfolder/_data.yml

```yml
mergedKeys:
  site: object

site:
  title: My humble site
  author: Oscar Otero
```

In this example, we are indicating to Lume that the variable `site` must be merged using the `object` mode. Now, the result of the variable `site` is an object including the properties of the parent variable and only overrides the properties with the same name. So the result will be something like this:

```yml
site:
  title: My humble site
  author: Laura Rubio
```

The `object` merge mode is not recursive; it only works with the first-level properties. A recursive option may be added in the future.

The `mergedKeys` variable is also merged with other `mergedKeys` variables in subfolders and pages and using always the `object` mode. This means that you can define this variable in the root `_data` file of the site and override it in specific subfolders.

## [array mode](https://lume.land/docs/core/merged-keys/#array-mode)

There's another merge mode for arrays. In this mode, the merge result is an array with all values found in all `_data` levels. For example:

-   /_data.yml
-   /subfolder/_data.yml

```yml
mergedKeys:
  category: array

category:
  - programming
  - deno
  - javascript
```

The result of this merge is:

```yml
category:
  - programming
  - deno
  - javascript
  - typescript
```

It's an array with all values present in all parent `_data` contexts. The result includes only unique values: if the same value is repeated in different `_data` contexts, it's included only once in the result.

## [stringArray mode](https://lume.land/docs/core/merged-keys/#stringarray-mode)

There's a special case in which you want to make sure that all values of the array are strings. Let's see the following example:

-   /_data.yml
-   /subfolder/_data.yml

```yml
mergedKeys:
  category: array

category:
  - errors
  - 404
```

The result of this merge is:

```yml
category:
  - errors
  - 404
  - "404"
```

As you can see, the value `404` is duplicated, once as a number and again as a string. To prevent this behavior, you may want to convert all values to strings to remove duplicates. Instead of `array`, use the `stringArray` mode:

```yml
mergedKeys:
  category: stringArray
```

Now, the result of this merge is:

```yml
category:
  - errors
  - "404"
```

# Render order

Configure the rendering order of the pages

In Lume all pages are rendered at the same time. This works well in most cases, but sometimes you want to make sure a page is rendered before or after others. The most typical example is with auto-generated pages. Let's say you have a page that generates multiple pages dynamically using data from an external API:

```js
export const layout = "layouts/api.njk";

const response = await fetch("https://my-api.com/data.json");
const data = await response.json();

export default function* () {
  for (const item of data.items) {
    yield {
      url: `item-${item.id}`,
      title: item.title,
      type: "api",
      content: item.text,
    };
  }
}
```

This script will generate one page for every item returned by the api. Note that we have added the variable `type` to all pages with the value `"api"`. This will help us to select these new pages later.

To list and paginate all these auto-generated pages, you may want to create something like this:

```js
export const layout = "layouts/api-pagination.njk";

export default function* ({ search, paginate }) {
  const items = search.pages("type=api");

  for (const page of paginate(items)) {
    yield page;
  }
}
```

In this script, we are using the [search](https://lume.land/plugins/search/) helper to search all pages with the variable `type=api` and paginate them with the [paginate](https://lume.land/plugins/paginate/) helper. But we have a problem: because all pages are executed at the same time, it's possible that the `type=api` pages didn't exist when we went to paginate them, so the pagination won't work. What we really need is create all dynamic pages **before** paginating them.

To control this, lume has the `renderOrder` variable, to configure the order in which every page is rendered. By default this value is `0`, so if you change it to a negative value (like `-1`, `-2` etc) the page will be rendered **before** the others, and changing it to a positive value (`1`, `2`, etc) will cause the page to be rendered **after**. So, to fix our example, the solution could be to change the `renderOrder` of the pagination script to a value greater than 0, for example, `1`:

```js
export const layout = "layouts/api-pagination.njk";

// Changed this to render this page after the others
export const renderOrder = 1;

export default function* ({ search, paginate }) {
  const items = search.pages("type=api");

  for (const page of paginate(items, { url: (n) => `/page/${n}/`, size: 10 })) {
    yield page;
  }
}
```

This ensures that this script will be run **after** the `type=api` pages are created. An alternative solution is change the `renderOrder` of the API script to a negative value, like `-1`.

# Multiple template engines

Overriding the behavior of a template engine

By default, the template engine used to render a file is decided according to the file extension. For example, an `.md` file uses Markdown, `.njk` file uses Nunjucks and so on.

You can override this default behaviour with the `templateEngine` option. Any page having this variable will use it to decide the template engine instead of the extension.

The following example is an `.md` file but it is configured to use Nunjucks to render (instead of Markdown).

```yml
---
title: My post
templateEngine: njk
---

# Hello world
```

A typical example is a file using Markdown to render HTML but Nunjucks to insert variables or includes. To do that, you can use an array to add several engines:

```yml
---
title: My post
templateEngine: [njk, md]
---

# Hello, this is the post title {{ title }}
```

In the example above, the page will be rendered using Nunjucks first and then Markdown.

# Loaders and engines

How to add custom loaders and template engines to Lume.

1.  [Creating a loader](https://lume.land/docs/core/loaders/#creating-a-loader)
2.  [Register a data loader](https://lume.land/docs/core/loaders/#register-a-data-loader)
3.  [Register a page loader](https://lume.land/docs/core/loaders/#register-a-page-loader)
4.  [Template engines](https://lume.land/docs/core/loaders/#template-engines)

Loaders are functions that read and return the content of files. There are different loaders for different formats, like `json`, `yaml`, JavaScript modules or plain text.

## [Creating a loader](https://lume.land/docs/core/loaders/#creating-a-loader)

Creating a custom loader is really easy: you only have to create a function that reads the content of a file and returns an object with that content.

Let's say you want to add support for the `toml` format, using the [encoding/toml](https://deno.land/std/encoding#toml) Deno std module:

```js
import { parse } from "https://deno.land/std/encoding/toml.ts";

async function tomlLoader(path) {
  const content = await Deno.readTextFile(path);
  return parse(content);
}
```

## [Register a data loader](https://lume.land/docs/core/loaders/#register-a-data-loader)

If you want to use the TOML loader to load data files, use the `site.loadData()` method in the `_config.ts` file:

```js
site.loadData([".toml"], tomlLoader);
```

Now you can use the TOML format to save data files (`_data.toml` or `_data/*.toml`).

## [Register a page loader](https://lume.land/docs/core/loaders/#register-a-page-loader)

To generate pages using TOML format, use the `loadPages` function:

```js
site.loadPages([".toml"], tomlLoader);
```

Now, any `*.toml` file in your site will be loaded and used to render a page. For example, the file `/about-us.toml` would be loaded and saved as `/about-us/index.html`.

You could have realized that `loadPage()` is intended to generate `.html` pages. So the `.toml` extension is removed and replaced by `.html` (or `/index.html` for pretty urls).

You may want to load TOML files, process them and export as `.toml` files, not `.html` files. To do that, you can use `loadAssets()`:

```js
site.loadAssets([".toml"], tomlLoader);
```

Now, the `*.toml` files are loaded and saved as `toml`. The function `loadAssets` is useful to load assets files, like `css`, `js`, `svg`, that you want to transform (bundle, minify...) and save them while keeping the same extension, instead of renaming them to `html`.

**Note:** you can't use the same extension to generate pages and assets, so a way to have support for both is adding a sub-extension (like `tmpl`) for pages. Example:

```js
// Use *.html.toml extension for pages
site.loadPages([".html.toml"], tomlLoader);

// And any other *.toml files for assets
site.loadAssets([".toml"], tomlLoader);
```

This is the same strategy used for JavaScript/TypeScript modules (`*.tmpl.js` for pages and `*.js` for JavaScript assets).

## [Template engines](https://lume.land/docs/core/loaders/#template-engines)

Lume supports several template engines to render your pages, like Nunjucks, Pug or Eta. It's easy to extend this support for more template engines: you only need to create a class extending the [`Engine` interface](https://doc.deno.land/https://deno.land/x/lume/core.ts/~/Engine). Let's see an example using [handlebars](https://github.com/handlebars-lang/handlebars.js):

```ts
import HandlebarsJS from "https://dev.jspm.io/handlebars@4.7.6";
import { Data, Engine } from "lume/core.ts";

export default class HandlebarsEngine implements Engine {
  /** Render the content (sync or async) */
  render(content: string, data: Data): string {
    return this.renderSync(content, data, filename);
  }

  /** Render sync (used only for components) */
  renderSync(content: string, data: Data): string {
    const template = HandlebarsJS.compile(content);
    return template(data);
  }

  /** Register helpers */
  addHelper() {}

  /** Delete cache */
  deleteCache() {}
}
```

To use this template engine, pass it as the third argument of the `loadPages` function:

```ts
import textLoader from "lume/loaders/text.ts";
import HandlebarsEngine from "./handlebars-engine.ts";

site.loadPages([".hbs"], textLoader, new HandlebarsEngine(site));
```

Now, all files with the `.hbs` extension will be loaded using the `textLoader` and rendered using the Handlebars engine.

# Processors

A guide on extending Lume with custom processors

1.  [The page object](https://lume.land/docs/core/processors/#the-page-object)
2.  [Using the DOM API](https://lume.land/docs/core/processors/#using-the-dom-api)
3.  [Process assets](https://lume.land/docs/core/processors/#process-assets)
4.  [Preprocess](https://lume.land/docs/core/processors/#preprocess)
5.  [Create or remove pages dynamically](https://lume.land/docs/core/processors/#create-or-remove-pages-dynamically)
    -   [Remove pages dynamically](https://lume.land/docs/core/processors/#remove-pages-dynamically)
6.  [How processors and preprocessors work](https://lume.land/docs/core/processors/#how-processors-and-preprocessors-work)
7.  [Global (pre)processors](https://lume.land/docs/core/processors/#global-(pre)processors)
8.  [Process all pages](https://lume.land/docs/core/processors/#process-all-pages)

A processor is a function to transform the content of pages just **after the page is rendered**. Let's see an example of a processor to minify HTML pages:

```js
function minifyHTML(page) {
  page.content = minify(page.content);
}
```

If you want to use this processor to build your site, you can register it in the `_config.js` file:

```js
site.process([".html"], minifyHTML);
```

Now, all HTML pages are minified.

## [The page object](https://lume.land/docs/core/processors/#the-page-object)

As you can see in the previous example, the function receives an object with the page (or asset). This object has not only the page content but much more data:

```js
function process(page) {
  page.content; // The content of the page
  page.document; // The parsed HTML code, to use the DOM API
  page.src; // The info about the source file of this page
  page.data; // All data available for this page (front matter merged with _data)
}
```

For example, let's say you only want to minify the pages where the value `minify` is `true`:

```js
site.process([".html"], (page) => {
  if (page.data.minify) {
    page.content = minify(page.content);
  }
});
```

## [Using the DOM API](https://lume.land/docs/core/processors/#using-the-dom-api)

You can use the **DOM API** (provided by [deno-dom](https://github.com/b-fuze/deno-dom)) with methods like `querySelector`, `setAttribute`, etc to modify HTML code. For example, let's create a processor to add automatically the `alt` attribute to all images:

```js
site.process([".html"], (page) => {
  page.document?.querySelectorAll("img").forEach((img) => {
    if (!img.hasAttribute("alt")) {
      img.setAttribute("alt", "This is a random alt");
    }
  });
});
```

## [Process assets](https://lume.land/docs/core/processors/#process-assets)

For non-HTML pages (like CSS or JavaScript files), you can use the processors to compile CSS, minify JavaScript code or minify images.

```js
site.process([".js"], function (page) {
  page.content = myBundler(page.content);

  // Append .min to the filename
  // so it will be saved as example.min.js
  page.data.url = page.data.url.replace(/\.js$/, ".min.js");
});
```

## [Preprocess](https://lume.land/docs/core/processors/#preprocess)

If you need to execute a function **before rendering** (for example, to configure a custom template engine or add extra data to some pages), you can use a **preprocessor**. Preprocessors work like processors, but with they are executed before rendering.

Let's create a preprocessor to include a variable with the source filename:

```js
site.preprocess(
  [".html"],
  (page) => page.data.filename = page.src.path + page.src.ext,
);
```

## [Create or remove pages dynamically](https://lume.land/docs/core/processors/#create-or-remove-pages-dynamically)

Some processors can generate additional pages (or remove them). The second argument of the (pre)processors contains an array with all pages that are being processed. You can modify this array to add pages dynamically. For example:

```js
import { Page } from "lume/core/filesystem.ts";

site.process([".css"], (page, pages) => {
  // Minify the css content
  const { code, map } = myCssMinifier(page.content);

  // Update the page content
  page.content = code;

  // Create a new page with the source map
  const url = page.data.url + ".map";
  pages.push(Page.create(url, map));
});
```

### [Remove pages dynamically](https://lume.land/docs/core/processors/#remove-pages-dynamically)

If a processor returns `false`, the page is removed from the build process. This allows to creating a processor to filter only some pages:

```ts
// Remove all html pages with the language = "en"
site.process([".html"], (page) => {
  const language = page.data.lang;

  if (language === "en") {
    return false;
  }
});
```

## [How processors and preprocessors work](https://lume.land/docs/core/processors/#how-processors-and-preprocessors-work)

Both processors and preprocessors are tied to file extensions (`.html`, `.js` etc). To decide if a page must use a registered processor or preprocessor, Lume searches the extension of the input file (like `.md` or `.njk`) or the output file (like `.html` or `.css`).

Another interesting thing is they are executed in the same order as they are defined. This allows chaining different processors to the same file extension. For example: two processors for the `.css` extension, one to compile the code and another to minify.

## [Global (pre)processors](https://lume.land/docs/core/processors/#global-(pre)processors)

If you want to run a processor or preprocessor for all pages, use `*` in the first argument:

```js
site.process("*", processAllPages);
```

## [Process all pages](https://lume.land/docs/core/processors/#process-all-pages)

`site.process` and `site.preprocess` functions works at page level. They only process a page each time. If you need to run the processor only once to all pages, there's the `site.processAll` and `site.preprocessAll`. They are very similar but they are executed only once and receives an array of all pages in the first argument:

```js
site.processAll([".html"], (pages) => {
  pages.forEach((page) => my_processor(page));
  console.log(`Processed ${pages.length} HTML pages!`);
});
```

# Remote files

Load remote files as fallback of missing local files

1.  [Remote layouts](https://lume.land/docs/core/remote-files/#remote-layouts)
2.  [Override remote files](https://lume.land/docs/core/remote-files/#override-remote-files)
3.  [Limits of the remote files](https://lume.land/docs/core/remote-files/#limits-of-the-remote-files)
    -   [Including templates](https://lume.land/docs/core/remote-files/#including-templates)
    -   [Import modules](https://lume.land/docs/core/remote-files/#import-modules)
    -   [Asset processors](https://lume.land/docs/core/remote-files/#asset-processors)

From Lume `v1.10.0` it's possible to use remote files as if they were local files. To configure a remote file, you must set a local name and a remote URL in your `_config.ts` file using the `remoteFile()` function. For example:

```ts
import lume from "lume/mod.ts";

const site = lume();

site.remoteFile("styles.css", "https://example.com/theme/styles.css");

export default site;
```

This indicates to Lume that if the file `styles.css` **doesn't exist locally** the remote URL must be used. Note that the file **wont be saved in the project folder**, but it's in memory.

If you want to copy this file statically:

```js
site.copy("styles.css");
```

Because the file doesn't exist in your local folder, Lume will download the file from the URL and save it in the dest folder.

The `postcss` plugin supports Lume's remote files, so you can import this file in your CSS with:

```css
@import "./styles.css";
```

## [Remote layouts](https://lume.land/docs/core/remote-files/#remote-layouts)

Remote files can be used for layouts. Let's say you have several websites using the same layout. Instead of repeating the same file in every project, you can load it remotely:

```ts
site.remoteFile(
  "_includes/layouts/main.njk",
  "https://example.com/theme/layouts/main.njk",
);
```

Now, you can use this layout in all your files:

```md
---
title: This is a page
layout: layouts/main.njk
---

Page content
```

## [Override remote files](https://lume.land/docs/core/remote-files/#override-remote-files)

If a remote file exists locally (in the previous examples: `styles.css` and `_includes/layouts/main.njk`) the local file will be used instead of the remote one. This is useful for creating themes with all templates and assets loaded remotely but allowing overriding some files locally in order to customize the theme. As an example, see the [Simple blog theme](https://github.com/lumeland/theme-simple-blog).

## [Limits of the remote files](https://lume.land/docs/core/remote-files/#limits-of-the-remote-files)

Remote files work fine in the following cases:

-   To copy static files (with `site.copy()`)
-   To load pages and assets.
-   To load layouts defined with the `layout` property of the pages.
-   To load `_data` files and folders.
-   To load `_components` files.
-   Some processors like `esbuild` and `postcss` have support for remote files.

But there are some scenarios that remote files don't work or work in a limited way:

### [Including templates](https://lume.land/docs/core/remote-files/#including-templates)

Some template engines have their own way of loading templates. For example, Pug uses `extends "filename"`, Liquid and Nunjucks use `{% include "filename" %}`, etc.

Some engines allow configuring how to load these files (so they can use the Lume reader), but others don't. At this moment, **only Nunjucks supports remote files**. Keep in mind that Lume reader is asynchronous, meaning that the remote files loaded by Nunjucks must use the async API (`asyncEach` instead of `for` etc). More info about [Asynchronous support for Nunjucks](https://mozilla.github.io/nunjucks/api.html#asynchronous-support).

### [Import modules](https://lume.land/docs/core/remote-files/#import-modules)

JavaScript/TypeScript modules imported as `import foo from "./filename.ts"` are not managed by Lume reader, but you can use import maps for a similar behavior.

### [Asset processors](https://lume.land/docs/core/remote-files/#asset-processors)

Some processors like `SASS` don't allow customizing how to load imported resources, so they cannot use the Lume reader. For styles, only the `postcss` plugin supports remote files. And to bundle JavaScript use `esbuild`.

# Other Resources
- https://lume.land/docs/advanced/order-of-operations/
- https://lume.land/docs/advanced/migrate-from-11ty/
- https://lume.land/docs/advanced/deployment/
- https://lume.land/docs/advanced/plugins/