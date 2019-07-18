---
title: Markdown Cheatsheet
author: Ankit M
date: 2019-07-18
status: draft
---



# Github Pages

- Ability to host any static files in a github repository.

- Similar to S3 but free

- Several Options:

- Use `gh-pages` branch

- Use `master` branch

- Use `docs` directory on `master` branch

- URL format is:

  ```
  https://<username or organization>.github.io/<project name>
  ```

- Allowed to have custom domain easily - just point your DNS

- Can put stuff at

  ```
  https://<username or organization>.github.io/
  ```

  by creating a project named after the organization or user.



### How it works (option 1)

One-time setup of github pages (Easiest to create the `gh-pages` branch. Autodetected by github). Then:

1. Write source material in markdown
2. Check source material into the `master` branch
3. Run a build on the source material to render material
4. Check in rendered material into the `gh-pages` branch
5. Rinse, Repeat

