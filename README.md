# hexo-theme-bootstrap-blog

A simple [Bootstrap] v3 blog theme for [Hexo].

Based on the [official Bootstrap Blog example template](http://getbootstrap.com/examples/blog/).

[Demo site](http://cgmartin.github.io/hexo-theme-bootstrap-blog/) | [More Information](https://cgmartin.com/2016/01/05/bootstrap-blog-hexo-theme/)

## Setup Instructions

### Install

**This theme requires Hexo 2.4 and above.**

1) Install theme:

```bash
$ git clone https://github.com/cgmartin/hexo-theme-bootstrap-blog.git themes/bootstrap-blog
```

2) (optional) Install [hexo-tag-bootstrap](https://github.com/wzpan/hexo-tag-bootstrap) for more Bootstrap tags (textcolors, buttons, labels, badges, etc.):

```bash
$ npm install hexo-tag-bootstrap --save
```

3) (optional) Install [hexo-tag-fontawesome](https://github.com/akarzim/hexo-tag-fontawesome) for placing Font Awesome icons in your Markdown:

```bash
$ npm install hexo-tag-fontawesome --save
```

### Enable

Modify the `theme` setting in `_config.yml` to `bootstrap-blog`.

### Update

```bash
cd themes/bootstrap-blog
git pull
```

## Configuration

```yml
# File: themes/bootstrap-blog/_config.yml

# Header
navbar_brand: false
menu:
  Home: index.html
  Archives: archives/
rss: /atom.xml

# Content
excerpt_link: Read More
fancybox: true

# Sidebar
widgets:
- about         # See also: `about_content`
- category
- tag
- tagcloud
- archives
- recent_posts
about_widget_content: >
  <p>Etiam porta <em>sem malesuada magna</em> mollis euismod.
  Cras mattis consectetur purus sit amet fermentum. Aenean
  lacinia bibendum nulla sed consectetur.</p>

# Miscellaneous
google_analytics:
# DOC:
  # https://business.twitter.com/en/help/campaign-setup/campaign-targeting/tailored-audiences-from-web.html
# EXAMPLE: twitter_pixel_id: 'xx11x'
twitter_pixel_id:
# EXAMPLE: twitter_std_event: 'PageView'
twitter_std_event:
favicon:
twitter_id:
google_plus:
fb_admins:
fb_app_id:
disqus_sitename:
twitter:
instagram:
github:
```

- **navbar_brand** - The HTML content for an optional ["navbar-brand"](http://getbootstrap.com/components/#navbar-brand-image). Can be text or an image. `false` to hide.
- **menu** - Navigation menu (map of Titles to URLs)
- **rss** - RSS link (ie. "/atom.xml")
- **excerpt_link** - "Read More" link at the bottom of excerpted articles. `false` to hide the link.
- **fancybox** - Enable [Fancybox] for images
- **widgets** - Enable sidebar widgets ([more info below](#sidebar))
- **about_widget_content** - The HTML content for the "About" sidebar widget ([more info below](#sidebar))
- **google_analytics** - Google Analytics ID
- **favicon** - Favicon path (ie. '/favicon.ico')
- **twitter_id** - Twitter ID of the author (ie. `@c_g_martin`)
- **google_plus** - Google+ profile link
- **fb_admins** - MISSING DOC
- **fb_app_id** - MISSING DOC
- **disqus_sitename** - `www._disqus_sitename_.disqus.com`
### For social media icons
- **twitter** - https://twitter.com/YOUR_NAME
- **instagram** - https://instagram.com/YOUR_NAME
- **github** - https://github.com/YOUR_NAME

Instead of editing the layout's configuration file directly, you can override the theme settings from your project's root `_config.yml`, ie.:
```yml
theme_config:
  # Header
  navbar_brand: <img src="/navbrand.png">
  menu:
    Home: index.html
    Archives: archives/
    'Another Page': page/index.html
  widgets:
   - about
   - category
   - archive
   - recent_posts
   - tag
  about_widget_content: >
    <p>This is <strong>custom content</strong> for the
    "about" sidebar widget.</p>
```

## Features

### :tada: :confetti_ball: NEW: :tada: :confetti_ball: Twitter Universal Website Tag

You can add your twitter pixel ID and it will handle your conversation tracking.
Just follow [`_config.yml`](_config.yml) documentation.

### Social Media Icons

You can add your social media accounts links to your navigation bar with icons. Just you have to edit `_config` file.

```yml
twitter:
instagram:
github:
```

### Vanilla javascript Disqus add-on

You just add your disqus sitename to under the theme folder's `_config.yml` that's it.

```yml
disqus_sitename: your_sitename
```

### Hexo's I18N Compatibility

You can manage your website with multiple-languages. You just add your language yml files, that's it.

### Front-Matter Extras

Optional settings in the front-matter can be added for various effects:
```yml
---
author: Author Name   # displays the post's author
photos:               # displays a Bootstrap thumbnail gallery
- images/HNCK0537.jpg
- images/HNCK6173.jpg
---
```

### Fancybox

This theme uses [Fancybox] to showcase your photos. You can use the image Markdown syntax or fancybox tag plugin to add your photos.

Usage:
```
![img caption](img url)

~or~

{% fancybox img_url [img_thumbnail] [img_caption] %}
```

### Callouts

A custom tag for the [Bootstrap "callout" style](http://cpratt.co/twitter-bootstrap-callout-css-styles/) is available for use.

Usage:
```
{% callout [type:default|primary|success|info|warning|danger] %}
...content...
{% endcallout %}
```

Example:
```
{% callout info %}
#### {% fa info-circle %} Info tip
This is some callout content
{% endcallout %}
```

### Sidebar

This theme provides 6 built-in widgets that can be displayed in the sidebar:

- [about](./layout/_widget/about.ejs) \*
- [category](./layout/_widget/category.ejs)
- [tag](./layout/_widget/tag.ejs)
- [tagcloud](./layout/_widget/tagcloud.ejs)
- [archives](./layout/_widget/archives.ejs)
- [recent_posts](./layout/_widget/recent_posts.ejs)

All widgets are enabled and displayed by default. You can toggle them on/off with the `widgets` setting in the theme's [_config.yml](./config.yml).

\* **NOTE**: The "about" widget contains static Lorem Ipsum text by default. You'll want to edit the `about_widget_content` setting for your site or disable the widget in the [theme config](./config.yml). You can also modify the widget file itself to include contents from a Markdown page:
```html
<!-- file: ./layout/_widget/about.ejs -->
<div class="sidebar-module sidebar-module-inset">
  <h4>About</h4>
  <%- site.pages['data'].find(function(p) { return p.path === 'about/index.html'; }).content %>
</div>
```
...then run `hexo new page about` to create the Markdown page.

### Bootstrap Paginator Helper

A custom `bs_paginator()` helper is used to produce [Bootstrap-compatible pagination markup](http://getbootstrap.com/components/#pagination). It is a drop-in replacement for Hexo's built-in `paginator()`.

```
<%- bs_paginator({
  prev_text: '<i class="fa fa-chevron-left"></i> Prev',
  next_text: 'Next <i class="fa fa-chevron-right"></i>'
}) %>
```

## Development

The [default Landscape Hexo theme](https://github.com/hexojs/hexo-theme-landscape) was used as the starting point and heavily edited for this theme.

The Landscape Stylus styles have been replaced with standard CSS files which override `bootstrap.min.css`. Stylus is used only for [bundling the CSS files](./source/css/styles.styl). Feel free to convert the CSS to your pre-processor of choice (Stylus, LESS, Sass, etc.).

## TODO

- [X] Add i18n functionality to template.
- [X] Edit disqus_shortname to disqus_sitename. Because If person who have many disqus sites, will show first disqus sites/comments.
- [ ] Add disqus comment counter for home page. For example, "Comments (121)".
- [X] Add RSS feed functionality.

## License

[MIT License](http://cgm.mit-license.org/)

Copyright © 2016 Christopher Martin

[Hexo]: http://zespia.tw/hexo/
[Fancybox]: http://fancyapps.com/fancybox/
[Font Awesome]: http://fontawesome.io/
[Bootstrap]: http://getbootstrap.com/
