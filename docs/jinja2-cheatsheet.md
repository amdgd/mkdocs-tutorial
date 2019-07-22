---

---

# Jinja 2 Cheatsheet



## **Jinja 2 cheatsheet**

### Syntax

```jinja2
{% ... %}      # for Statements
{{ ... }}      # for Expressions to print to the template output
{# ... #}      # for Comments not included in the template output
#  ... ##      # for Line Statements. They have to be enabled. 
```



### Variables

```jinja2
{{ foo.bar }} 
# or
{{ foo['bar'] }}
```



### Loops

```jinja2
 {% for i in list %} ... {% endfor %}
```



### If

The if statement in Jinja is comparable with the Python if statement. In the simplest form, you can use it to test if a variable is defined, not empty and not false:

```jinja2
{% if users %}
<ul>
{% for user in users %}
    <li>{{ user.username|e }}</li>
{% endfor %}
</ul>
{% endif %}
```

For multiple branches, elif and else can be used like in Python. You can use more complex [Expressions](http://jinja.pocoo.org/docs/dev/templates/#expressions) there, too:

```jinja2
{% if kenny.sick %}
    Kenny is sick.
{% elif kenny.dead %}
    You killed Kenny!  You bastard!!!
{% else %}
    Kenny looks okay --- so far
{% endif %}
```



## Functions / Macros

Macros are comparable with functions in regular programming languages. They are useful to put often used idioms into reusable functions to not repeat yourself (“DRY”).

Here’s a small example of a macro that renders a form element

```jinja2
 {% macro myfunct(param1, param2) %}
 ...
 {% endmacro %}
 
 {% macro input(name, value='', type='text', size=20) -%}
    <input type="{{ type }}" name="{{ name }}" value="{{
        value|e }}" size="{{ size }}">
 {% endmacro %}
```

Using functions. The macro can then be called like a function in the namespace:

```jinja2
 {% myfunc(var, 5) %}
 
 <p>{{ input('username') }}</p>
<p>{{ input('password', type='password') }}</p>
```

If the macro was defined in a different template, you have to import it fist



### **Filters**

Filters can modify variables

- Filters are separated from the variable by a pipe symbol (|) and
- may have optional arguments in parentheses.
- Multiple filters can be chained. For example, {{ name|striptags|title }} will remove all HTML Tags from variable name and title-case the output will be in the form (title(striptags(name)))

For example, `{{ name|striptags|title }}` will remove all HTML Tags from variable name and title-case the output (`title(striptags(name))`).

Filters that accept arguments have parentheses around the arguments, just like a function call. For example: `{{ listx|join(', ') }}` will join a list with commas (`str.join(', ', listx)`).



### Tests

Beside filters, there are also so-called “tests” available. Tests can be used to test a variable against a common expression. To test a variable or expression, you add is plus the name of the test after the variable. For example, to find out if a variable is defined, you can do `name is defined`, which will then return true or false depending on whether name is defined in the current template context.

Tests can accept arguments, too. If the test only takes one argument, you can leave out the parentheses. For example, the following two expressions do the same thing:

```
{% if loop.index is divisibleby 3 %}
{% if loop.index is divisibleby(3) %}
```

#### Built-in Tests

`defined`(*value*)

Return true if the variable is defined:

```jinja2
{% if variable is defined %}
    value of variable: {{ variable }}
{% else %}
    variable is not defined
{% endif %}
```



## Inheritance

The most powerful part of Jinja is template inheritance. Template inheritance allows you to build a base “skeleton” template that contains all the common elements of your site and defines **blocks** that child templates can override.  *It’s the job of “child” templates to fill the empty blocks with content:*

You can build base skeleton templates containing blocks that can be used by child templates.

### Base HTML

```jinja2
<!-- base.html -->
<html lang="en">
<head>
    <title>
			{% block title %}{% endblock title%}
		</title>
 </head>

<body> 
	{% block body %}{% endblock body%}
	
	 <div id="footer">
 <!-- Footer block -->
        {% block footer %}
        &copy; Copyright 2008 by <a href="http://domain.invalid/">you</a>.
        {% endblock %}
   </div>
</body>
</html>
```

In this example, the `{% block %}` tags define four blocks that child templates can fill in. All the block tag does is tell the template engine that a child template may override those placeholders in the template.

### Child HTML

```jinja2
<!-- child.html -->
{% extends "base.html" %}

<!-- Title block -->
{% block title %}
	Index
{% endblock title%}

<!-- Body block -->
{% block content %}
    <h1>Index</h1>
    <p class="important">
      Welcome to my awesome homepage.
    </p>
{% endblock content%}

## child template doesn’t define the footer block, the value from the parent template is used instead.

```

- The `{% extends %}` tag is the key here. It tells the template engine that this template “extends” another template.
- When the template system evaluates this template, it first locates the parent. The extends tag should be the first tag in the template.
-  It’s the job of “child” templates to fill the empty blocks with content:
- Note that since the if the child template doesn’t define any  block, the value from the parent template is used instead.



### Repeated Blocks

If you want to print a block multiple times, you can, however, use the special self variable and call the block with that name:

```jinja2
<title>{% block title %}{% endblock %}</title>
<h1>{{ self.title() }}</h1>
{% block body %}{% endblock %}
```



### Super Blocks

It’s possible to render the contents of the parent block by calling super. This gives back the results of the parent block:

It’s possible to render the contents of the parent block by calling super. This gives back the results of the parent block:

```
{% block sidebar %}
    <h3>Table Of Contents</h3>
    ...
    {{ super() }}
{% endblock %}
```



### Named Block End-Tags

Jinja2 allows you to put the name of the block after the end tag for better readability:

```
{% block sidebar %}
    {% block inner_sidebar %}
        ...
    {% endblock inner_sidebar %}
{% endblock sidebar %}
```

However, the name after the endblock word must match the block name.



## Jinja Tips & Tricks

## Alternating Rows

If you want to have different styles for each row of a table or list you can use the cyclemethod on the loop object:

```jinja2
<ul>
{% for row in rows %}
  <li class="{{ loop.cycle('odd', 'even') }}">{{ row }}</li>
{% endfor %}
</ul>
```

cycle can take an unlimited amount of strings. Each time this tag is encountered the next item from the list is rendered.



## Highlighting Active Menu Items

Often you want to have a navigation bar with an active navigation item. This is really simple to achieve. Because assignments outside of blocks in child templates are global and executed before the layout template is evaluated it’s possible to define the active menu item in the child template:

```
{% extends "layout.html" %}
{% set active_page = "index" %}
```

The layout template can then access active_page. Additionally it makes sense to define a default for that variable:

```jinja2
{% set navigation_bar = [
    ('/', 'index', 'Index'),
    ('/downloads/', 'downloads', 'Downloads'),
    ('/about/', 'about', 'About')
] -%}
{% set active_page = active_page|default('index') -%}
...
<ul id="navigation">
{% for href, id, caption in navigation_bar %}
  <li{% if id == active_page %} class="active"{% endif
  %}><a href="{{ href|e }}">{{ caption|e }}</a></li>
{% endfor %}
</ul>
...
```