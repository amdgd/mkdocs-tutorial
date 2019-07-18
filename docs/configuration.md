---
title: Markdown Cheatsheet
author: Ankit M
date: 2019-07-18
status: draft
---



# Configuration



### use_directory_urls

This setting controls the style used for linking to pages within the documentation.

The following table demonstrates how the URLs used on the site differ when setting `use_directory_urls` to `true` or `false`.

| Source file      | use_directory_urls: true | use_directory_urls: false |
| :--------------- | :----------------------- | :------------------------ |
| index.md         | /                        | /index.html               |
| api-guide.md     | /api-guide/              | /api-guide.html           |
| about/license.md | /about/license/          | /about/license.html       |

The default style of `use_directory_urls: true` creates more user friendly URLs, and is usually what you'll want to use.

The alternate style can occasionally be useful if you want your documentation to remain properly linked when opening pages directly from the file system, because it creates links that point directly to the target *file* rather than the target *directory*.

**default**: `true`

### strict

Determines how warnings are handled. Set to `true` to halt processing when a warning is raised. Set to `false` to print a warning and continue processing.

**default**: `false`

### dev_addr

Determines the address used when running `mkdocs serve`. Must be of the format `IP:PORT`.

Allows a custom default to be set without the need to pass it through the `--dev_addr` option every time the `mkdocs serve`command is called.

**default**: `'127.0.0.1:8000'`