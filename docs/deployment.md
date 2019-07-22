---
title: Deployment
author: Ankit M
date: 2019-07-19
status: draft
---


# Deployment

## Deployment to GitHub Pages

### Direct Deployment

To publish the project to **GitHub Pages** as a subdomain, e.g. `/mdocs` of the main website, you need first to create a repository with that name, e.g. `mdocs` and add it to your project as a remote.

Next make sure you have a **gh-pages** branch that exists. If it doesn’t:

```shell
git checkout -b gh-pages
git rm -rf .
git push --set-upstream origin gh-pages
```
Now, open the command prompt in the root directory (on the `master` branch) and type:

```shell
mkdocs gh-deploy 
```

This will push the **master** branch to the remote **gh-pages**. After that, the project website is available at `your-github-login.github.io/mdocs`.

### Travis CI Deployment

Go to your GitHub account and create a new **Personal access token** in your Developer settings. Copy the hash string.

Keep well the hash string!

You will see it only once when you create it.

In the Travis CI settings of your project add a new **GITHUB_TOKEN** environment variable with the value of the hash string your have just copied. Don’t forget to turn in **ON** and to **ADD**.

Configure the `.travis.yml` file. You may start with something like this:
```shell
sudo: false
language: python
python: '3.6'
install:
- pip install -U pip
- pip install -r requirements.txt
- pip install https://github.com/bmcorser/fontawesome-markdown/archive/master.zip
script:
- git config credential.helper "store --file=.git/credentials"
- echo "https://${GITHUB_TOKEN}:@github.com" > .git/credentials
- mkdocs build --verbose --clean --strict
- if [ $TRAVIS_TEST_RESULT == 0 ]; then
    mkdocs gh-deploy --force;
  fi
```

The credentials here are necessary for the Travis agent to be able to connect to your Github repository and perform the necessary actions with it. Note that the credentials are based on the **Personal access token** you have created.

Also, I have put deployment inside the **script** fase instead of **after_success** as a workaround (see the tip of Chronial on this [Travis issue #758](https://github.com/travis-ci/travis-ci/issues/758)). Otherwise, the batch succeeds with a successful build even if deploy **fails**after it.

Next, you need to have **travis** Rubygem installed on your local machine. If not, install it:

```shell
gem install travis 
```

Using **travis**, add the encrypted token to `.travis.yml`:

```shell
travis encrypt GITHUB_TOKEN="the-token-from-github" --add ` 
```

This will add the following block at the end of the file:

```shell
env:   
    global:   
        - secure: "lots-of-seemingly-random-characters"
```

Now, when you push your changes to the remote **master**, Travis CI should publish the compiled website to **GitHub Pages** if the build succeeds.



http://madrus4u.com/mdocs/engine/start/