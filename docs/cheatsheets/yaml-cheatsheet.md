---
title: YAML Cheatsheet
author: Ankit M
date: 2019-07-18
status: draft
---

# YAML CheatSheet

**YAML** ("**YAML** Ain't Markup Language") is a human-readable data-serialization language. It is commonly used for configuration files, but could be used in many applications where data is being stored 

``` yaml
# YAML
name: Jon
```

``` yaml
# YAML
object:
  attributes:
    - attr1
    - attr2
    - attr3
  methods: [ getter, setter ]
```
parses to this `json`

``` json
{"object": {"attributes": ["attr1", "attr2", "attr3"], ...
```

``` yaml
# YAML
sonnet: |
  I wish I could
  write a poem
  but I can"t
```
parses to:

``` json
{"sonnet": "I wish I could\nwrite a poem\nbut I can't\n"}
```

``` yaml
# YAML
---
document: this is doc 1
---
document: this is doc 2
...
```

```yaml
name: SomeObject
attributes:
  - attr1
  - attr2
  - attr3
methods: [ getter, setter ]
---
name: MyPrettyObject
attributes:
  - attr1
  - attr2
  - attr3
methods: [ getter, setter ]
```
parses to:

``` json
{"attributes": ["attr1", "attr2", "attr3"],
 "methods": ["getter", "setter"],
 "name": "SomeObject"}
{"attributes": ["attr1", "attr2", "attr3"],
 "methods": ["getter", "setter"],
 "name": "MyPrettyObject"}
```
YAML also supports variables, or **repeated nodes**. The simplest explanation is that you define something as a variable by preceding it with "&NAME value" and you can refer to it with "*NAME" e.g.:

``` yaml
# YAML
some_thing: &NAME foobar
other_thing: *NAME
```
Parses to:
``` json
{"other_thing": "foobar", "some_thing": "foobar"}
```