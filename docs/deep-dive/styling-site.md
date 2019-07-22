---
title: Styling Site
author: Ankit M
date: 2019-07-18
status: draft
---

# Styling Content

MkDocs includes a couple built-in themes as well as various third party themes, all of which can easily be customized with extra CSS or JavaScript or overridden from the theme's custom_dir. 

You can also create your own custom theme from the ground up for your documentation. 

To use a theme that is included in MkDocs, simply add this to your mkdocs.yml config file. 

```yaml
theme: readthedocs 
```

Replace readthedocs with any of the built-in themes listed below.

## Build in Themes

- mkdocs
- readthedocs



## Third Party Themes

A list of third party themes can be found in the MkDocs [community wiki](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes).



## Attributes

Using attributes it is possible to set the various HTML element's attributes for output. An example attribute list might look like this:

```
{: #someid .someclass somekey='some value' }
```

This shows the possible definitions:

- A word which starts with `#` will set the id of an element.
- A word which starts with `.` will be added to the list of classes assigned to an element.
- A key/value pair `somekey='some value'` will assign that pair to the element.

This can be set on block level elements if defined on the last line of the block by itself.

```
This is a paragraph.
{: #an_id .a_class }
```

The one exception is headers, as they are only ever allowed on one line. So there you neet to write:

```
### A hash style header ### {: #hash }
```

If used on inline elements the attributes are defined immediately after the element without any separation:

```
[link](http://example.com){: class="foo bar" title="Some title!" }
```

> If classes are used you may define them in an additional CSS file



### Customising a Theme

If you would like to make a few tweaks to an existing theme, there is no need to create your own theme from scratch. For minor tweaks which only require some CSS and/or JavaScript, you can use the custom `docs` directory.

For more complex customizations, including overriding templates, you will need to use the theme custom directory. 

#### Using the `docs` directory

##### extra_css

The `extra_css` and `extra_javascript` configuration options can be used to make tweaks and customizations to existing themes. To use these, you simply need to include either CSS or JavaScript files within your documentation directory.

For example, to change the colour of the headers in your documentation, create a file called `extra.css` and place it next to the documentation Markdown. In that file add the following CSS.

```css
h1 {
  color: red;
}
```

##### extra_javascript

Set a list of JavaScript files in your `docs_dir` to be included by the theme. 

##### extra_templates

Set a list of templates in your `docs_dir` to be built by MkDocs. 

##### extra

A set of key value pairs, where the values can be any valid YAML construct, that will be passed to the template. This allows for great flexibility when creating custom themes.

For example, if you are using a theme that supports displaying the project version, you can pass it to the theme like this:

```
extra:
    version: 1.0
```