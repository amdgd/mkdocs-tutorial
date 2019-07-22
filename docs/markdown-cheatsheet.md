---
title: Markdown Cheatsheet
author: Ankit M
date: 2019-07-18
status: draft
---

# Markdown Cheatsheet

## Basic Elements

| Elements    |                                                              |
| --------------------- | ------------------------------------------------------------ |
| H1 to H6 Headings     |# Heading Text <br />## Heading Text <br />### Heading Text <br />#### Heading Text <br />##### Heading Text <br />###### Heading Text |
| Italics               | `*This text is italicized*`                                  |
| Bold                  | `**This text is bold**`                                      |
| Blockquote            | `> Blockquote paragraphs must have> a right-arrow bracket at the start> of every single line.`<br />`>> Use a blank line for multiple paragraphs.` |
| Unordered List        | `- Bullet list item`<br />`- Bullet list item`<br />`- Bullet list item`  <br />`- Use a two-space indent for nested lists` |
| Ordered List          | `1. Bullet list item` <br />`2. Bullet list item` <br />`3. Bullet list item  ` <br />`1. Ordered lists can also be nested` |
| Mixed List            | `1. Can you mix list types?  ` <br />`- Yes, you can!`         |
| Horizontal Line       | `---***___`  **Note:** Either three hyphens, asterisks, or underscores. |
| Hyperlink             | `This is an [example link](//www.makeuseof.com)`             |
| Image                 | `![Alt Text](http://example.com/image/path.png)`             |
| Ignore Markdown       | `Prefix Markdown characters with \*backslashes\* to ignore formatting.` |

## Extended Elements


|Elements |  |
|---|---|
| Code (Inline)         | ``This is inline code``                                      |
| Code (Block)          | ````This is a block of codeIt supports multiple lines````    |
| Strikethrough         | `~~This text is crossed out~~`                               |
| Hard Line Break       | `This is some text\This text is a new line, not a new paragraph` |
| Table                 | `| First Header | Second Header || ------------ | ------------- || Content cell 1 | Content cell 2 || Content column 1 | Content column 2 |`  **Note:** Preceding blank line is necessary. |
| Task Lists            | `- [x] Completed task item `<br /> `- [ ] Unfinished task item- ` <br />`[ ] \(Optional) Mark parentheses to be ignored` |
| Mention               | `You can mention @users and @teams on GitHub. Mainly useful when submitting or commenting on bugs and issues.` |
| Emoji                 | `:emojicode:`                                                |

## Footnote

```
Footnotes[^1] have a label[^@#$%] and the footnote's content.

[^1]: This is a footnote content.
[^@#$%]: A footnote on the label: "@#\$%".
```

A footnote label must start with a caret `^` and may contain any inline text (including spaces) between a set of square brackets `[]`. Only the first caret has any special meaning.

- A footnote content must start with the label followed by a colon and at least one space. 
- The label used to define the content must exactly match the label used in the body (including capitalization and white space). 
- The content would then follow the label either on the same line or on the next line. 
- The content may contain multiple lines, paragraphs, code blocks, blockquotes and most any other markdown syntax. The additional lines must be indented one level (four spaces or one tab).




