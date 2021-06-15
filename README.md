# eLearning Modules Framework


## Objective

Build an e-learning framework that allows the creation of modules each having unique content and color palette.

## Approach

The approach is to build a "Static Site Generator" framework.  This should allow for a very small footprint requiring almost no infrastructure with the goal of delivering the modules as zip files. The statically generated sites should be able to be hosted in just about any server environment or local machine. The framework will not hold any of the content. That will be stored separately, with the framework used only to generate the final packaged product.

## Assumptions

Without more specifications from the client this solution is being developed with the following assumptions.

1. Modules are made up of one or more sections. A section should be a generic content type that can be customized to generate a variety of topics (Intros, Lessons, Summaries, etc. )

1. Client is expecting the deliverables, and will not be directly using the application.  

1. Future modules will be developed using this framework.

1. When we are referring to localization, we mean to translate a module into one more other languages than English.


## Proposed Technology

The framework will be built utilizing the following main components:

* [Next.js](https://nextjs.org/)
* [Tailwind.css](https://tailwindcss.com/)
* [Markdown](https://www.markdownguide.org/)

### Additional Packages

Since Next.js is a javascript project and leverages Node Package Manager we can add additional functionality though packages.
While the following might not be the only packages available to use to complete this task, these do provide the basic functionality we would need as a starting point:

* [remark](https://www.npmjs.com/package/remark)
* [git-clone](https://www.npmjs.com/package/git-clone)
* [archiver](https://www.npmjs.com/package/archiver)
* [next-translate](https://www.npmjs.com/package/next-translate)

### Markdown Data Storage

Modules will be stored as Markdown documents in Git repositories. Each module will be stored in its own repository. Markdown is excellent for storing static page data. Additionally is is extremely portable as many frameworks and libraries offer support for parsing it, should the need arise to migrate this content in the future.


## Theming

A base theme will be developed using the Tailwind.css framework, pegged to a version that specifically supports IE11. This framework should allow for "design tokens." The exact implementation of these tokens is still to be determined, but the basic idea is that through configuration the colors defined in the base theme can be overwritten.

### IE support

The client requires that IE 11 is supported. We will choose a front end framework that specifically supports that browser version. Additionally, to support IE 11 the developers should also do the following:

* Avoid using Flexbox. While it is officially supported in IE11, it is buggy.

* Only use HTML5 elements supported by IE11. If elements are supported by using polyfills, they should be avoided due to possible performance issues.

* When writing Javascript write in the ES5 standard. If you must use ES6 features transpile code to ES5


## Module Development

### Page Structure / Navigation
Module sections will be organized through the markdown file structure. Additionally the navigation will be generated through the page structure. Metadata like Tiles, Navigation Labels, etc., can be configured through the markdown headers. (Markdown headers may require additional packages not yet defined, TBD).

### Localization

In order to provide support for Localization in future modules or future versions of the initial modules we will need to take advantage first of the Next.js internationalized routing and a translation package for everything else. Markdown documents can be provided for each language version of the module. Through the next-translate package tokens will need to be used for items that are not stored in language specific markdown documents.

### Configuration

It *should* be simple...

Provide the location of the Module git repository (and auth info if not public) and any design token overrides. Simply change which content repository is used to generate the output for a different module.


### Build / Delivery

Since the client is expecting the modules to be developed as .zip files. We can use the [export function in Next.js](https://nextjs.org/docs/advanced-features/static-html-export) paired with the archiving npm package  

When the build command is run, the fully localized output of a static site containing all of the module content should be created and automatically archived.


## Terminology

**Static Site Generator**  - A static site generator is a tool that generates a full static HTML website based on raw data and a set of templates. Essentially, a static site generator automates the task of coding individual HTML pages and gets those pages ready to serve to users ahead of time. Because these HTML pages are pre-built, they can load very quickly in users' browsers. [Source](https://www.cloudflare.com/learning/performance/static-site-generator/)

**Transpile**  - Converts code from one language to another or one version or another. (ES6 and ES5 are different versions or generations of the JavaScript language)
