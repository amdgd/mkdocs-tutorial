---
title: Home
author: Ankit M
date: 2019-07-17
description: A brief tutorial to get your started with MkDocs.
status: completed
---

# Welcome to MkDocs

## Installation

Some basic steps. Creating Local git repo, adding remote, creating virtualenv etc. 
This is prior to installing Mkdocs

```shell
# Install Mkdocs Tutorial Directory
$ mkdir mkdocs-tutorial && cd mkdocs-tutorial

# check python version
$ python --version
> 
Python 3.7.4

# Creating a virtualenv for mkdocs and its dependencies
$ virtualenv mkdocs-env
$ source mkdocs-env/bin/activate

# Installing MkDocs
$ pip install mkdocs

# Checking if installation went smooth
$ mkdocs --version
> 
mkdocs, version 1.0.4

# Go back to the parent directory of your current mkdocs project folder
$ mkdocs new mkdocs-tutorial
$ cd mkdocs-tutorial 
```

`mkdocs.yml`, and a folder named `docs` that will contain your documentation source files. Right now the `docs` folder just contains a single documentation page, named `index.md`.

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.



## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
