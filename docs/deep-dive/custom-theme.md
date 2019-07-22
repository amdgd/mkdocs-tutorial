---
title: Custom Theme
author: Ankit M
date: 2019-07-18
status: draft

---

# Custom Theme



The bare minimum required for a custom theme is a `main.html`a JinJa2 Template directory not a child of 'docs directory'.

Within mkdocs.yml, set the theme.custom_dir option to the path of the directory containing main.html. The path should be relative to the configuration file. 

For example, given this example project layout:

```
mkdocs.yml
docs/
    index.md
    about.md
custom_theme/
    main.html
    ...
```

... you would include the following settings in `mkdocs.yml` to use the custom theme directory:

```yaml
theme:
    name: null
    custom_dir: 'custom_theme/'
```

- Generally, when building your own custom theme, the theme.name configuration setting would be set to `null`. 
	However, if the `theme.custom_dir` configuration value is used in combination with an existing theme, the `theme.custom_dir` can be used to replace only specific parts of a built-in theme. 	- 
- For example, with the above layout and if you set `name: "mkdocs"` then the `main.html` file in the theme.custom_dir would replace the file of the same name in the `mkdocs` theme but otherwise the `mkdocs` theme would remain unchanged. 
- This is useful if you want to make small adjustments to an existing theme.



## Basic theme

The simplest `main.html` file is the following:

```jinja2
<!DOCTYPE html>
<html>
  <head>
    <title>
    
    {% if page.title %}
    	{{ page.title }} - 
     {% endif %}
     
     {{ config.site_name }}
     
     </title>
  </head>
  <body>
    
    {{ page.content }}
    
  </body>
</html>
```

the built-in themes are implemented in a `base.html` file, which `main.html` extends. Although not required, third party template authors are encouraged to follow a similar pattern and may want to define the same blocks as are used in the built-in themes for consistency.

####  Template Blocks

The built-in themes implement many of their parts inside template blocks which can be individually overridden in the `main.html`template. Simply create a `main.html` template file in your `custom_dir` and define replacement blocks within that file. Just make sure that the `main.html` extends `base.html`. For example, to alter the title of the MkDocs theme, your replacement `main.html`template would contain the following:

```
{% extends "base.html" %}

{% block title %}
<title>Custom title goes here</title>
{% endblock %}
```

In the above example, the title block defined in your custom `main.html` file will be used in place of the default title block defined in the parent theme. You may re-define as many blocks as you desire, as long as those blocks are defined in the parent. For example, you could replace the Google Analytics script with one for a different service or replace the search feature with your own. You will need to consult the parent theme you are using to determine what blocks are available to override. The MkDocs and ReadTheDocs themes provide the following blocks:

- `site_meta`: Contains meta tags in the document head.
- `htmltitle`: Contains the page title in the document head.
- `styles`: Contains the link tags for stylesheets.
- `libs`: Contains the JavaScript libraries (jQuery, etc) included in the page header.
- `scripts`: Contains JavaScript scripts which should execute after a page loads.
- `analytics`: Contains the analytics script.
- `extrahead`: An empty block in the `<head>` to insert custom tags/scripts/etc.
- `site_name`: Contains the site name in the navigation bar.
- `site_nav`: Contains the site navigation in the navigation bar.
- `search_box`: Contains the search box in the navigation bar.
- `next_prev`: Contains the next and previous buttons in the navigation bar.
- `repo`: Contains the repository link in the navigation bar.
- `content`: Contains the page content and table of contents for the page.
- `footer`: Contains the page footer.



## Template Variables

Each template in a theme is built with a template context. These are the variables that are available to themes. The context varies depending on the template that is being built. At the moment templates are either built with the global context or with a page specific context. 

The global context is used for HTML pages that don't represent an individual Markdown document, for example a 404.html page or search.html.



### Global Context

#### config

The `config` variable is an instance of MkDocs' config object generated from the `mkdocs.yml` config file. While you can use any config option, some commonly used options include:

config.site_name
config.site_url
config.site_author
config.site_description
config.extra_javascript
config.extra_css
config.repo_url
config.repo_name
config.copyright
config.google_analytics

#### nav 

The nav variable is used to create the navigation for the documentation. The nav object is an iterable of navigation objects as defined by the nav configuration setting.

#### Navigation Objects
Navigation objects contained in the nav template variable may be one of 
- section objects, 
- page objects, 
- link objects. 

While section objects may contain nested navigation objects, pages and links do not.

##### Page Objects
Page objects are the full page object as used for the current page with all of the same attributes available. Section and Link objects contain a subset of those attributes as defined below:

#####  Section
A section navigation object defines a named section in the navigation and contains a list of child navigation objects. Note that sections do not contain URLs and are not links of any kind. However, by default, MkDocs sorts index pages to the top and the first child might be used as the URL for a section if a theme choses to do so.

The following attributes are available on section objects:

| Atrribute | Description |
| ---- | ---- |
| section.title | The title of the section.  |
| section.parent | The immediate parent of the section or None if the section is at the top level. |
| section.children | An iterable of all child navigation objects. Children may include nested sections, pages and links. |
| section.active | When True, indicates that a child page of this section is the current page and can be used to highlight the section as the currently viewed section. Defaults to False. |
| section.is_section | Indicates that the navigation object is a "section" object. Always True for section objects. |
| section.is_page | Indicates that the navigation object is a "page" object. Always False for section objects. |
| section.is_link | Indicates that the navigation object is a "link" object. Always False for section objects. |

##### Link

A link navigation object contains a link which does not point to an internal MkDocs page. The following attributes are available on link objects:

| Atrribute | Description |
| ---- | ---- |
| link.title | The title of the link. This would generally be used as the label of the link.|
| link.url | The URL that the link points to. The URL should always be an absolute URLs and should not need to have base_url prepened. |
| link.parent | The immediate parent of the link. None if the link is at the top level. |
| link.children | Links do not contain children and the attribute is always None. |
| link.active | External links cannot be "active" and the attribute is always False. |
| link.is_section | Indicates that the navigation object is a "section" object. Always False for link objects. |
| link.is_page | Indicates that the navigation object is a "page" object. Always False for link objects. |
| link.is_link | Indicates that the navigation object is a "link" object. Always True for link objects. |

##### nav.homepage
The page object for the homepage of the site.

#####  nav.pages
A flat list of all page objects contained in the navigation. This list is not necessarily a complete list of all site pages as it does not contain pages which are not included in the navigation. This list does match the list and order of pages used for all "next page" and "previous page" links. For a list of all pages, use the pages template variable.

##### Nav Example

Following is a basic usage example which outputs the first and second level navigation as a nested list.

```jinja2
{% if nav|length>1 %}
    <ul>
    {% for nav_item in nav %}
        {% if nav_item.children %}
            <li>{{ nav_item.title }}
                <ul>
                {% for nav_item in nav_item.children %}
                    <li class="{% if nav_item.active%}current{% endif %}">
                        <a href="{{ nav_item.url|url }}">{{ nav_item.title }}</a>
                    </li>
                {% endfor %}
                </ul>
            </li>
        {% else %}
            <li class="{% if nav_item.active%}current{% endif %}">
                <a href="{{ nav_item.url|url }}">{{ nav_item.title }}</a>
            </li>
        {% endif %}
    {% endfor %}
    </ul>
{% endif %}
```