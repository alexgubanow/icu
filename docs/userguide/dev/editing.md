---
layout: default
title: User Guide Editing
parent: Contributors
---
<!--
© 2020 and later: Unicode, Inc. and others.
License & terms of use: http://www.unicode.org/copyright.html
-->

# Editing the ICU User Guide
{: .no_toc }

## Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

This version of the ICU User Guide is generated directly from the Markdown
files in the `/docs` directory of the main repository. In particular, the
Markdown files are customized to work with the Jekyll static site generator,
which benefits from [GitHub's built-in support](https://docs.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll)
for Jekyll sites.

## How to Contribute

Because ICU User Guide source files are now contained within the main
repository, changes can now be made through the same process for contributing 
code patches. See [Contributions to the ICU Library](constributions.md) for the
current process of filing an issue and submitting a pull request.

In the case of a single file edit (ex: typo correction), a convenient way to
create the pull request is to follow the "Edit this page on Github" link at
the bottom of the page and [use GitHub to edit the file](https://docs.github.com/en/github/managing-files-in-a-repository/editing-files-in-your-repository)
and create the new pull request.

After the source branch for a potential pull request is made, the changes can 
be previewed using the fork repository that contains the source branch.  The
fork repository must be [configured to serve GitHub Pages](https://docs.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#choosing-a-publishing-source)
from the branch and the Markdown pages root directory (`/docs`).
> :point_right: **Note**:  there is a
latency of several minutes before GitHub Pages renders new changes, and 
[errors](https://docs.github.com/en/github/working-with-github-pages/about-jekyll-build-errors-for-github-pages-sites)
prevent the changes from being rendered.

## Jekyll Theme Configuration

Jekyll site-wide configurations are stored
in the `_config.yml` file. The current theme being used is
[Just the Docs](https://pmarsceill.github.io/just-the-docs/).

Due to incompatibilities between this theme and GitHub’s built-in implementation of the
CommonMark Markdown parser, the default Jekyll Markdown parser, Kramdown, is
used.

## Document Structure

Major chapters have Introduction pages, and further sections in a chapter are
subpages of that main chapter page. The navigation bar is generated from the
information provided in the header section of the Markdown file according to
the theme's [navigation annotations](https://pmarsceill.github.io/just-the-docs/docs/navigation-structure/).

## Syntax

[Markdown](https://kramdown.gettalong.org/syntax.html) should be preferred over custom
HTML to create content wherever possible.

## Common Styles

Styles are provided by the theme's settings, which can be modified in `_config.yml`.

## Code

Use the markdown notation of [single backtick](https://kramdown.gettalong.org/quickref.html#inline-code)
code spans (inline) and [tilde line-demarcated](https://kramdown.gettalong.org/quickref.html#code-blocks)
fenced code blocks (multi-line).

Unlike Github-flavored Markdown, in multi-line fenced code
blocks, the programming language in the [info string](https://spec.commonmark.org/0.29/#info-string)
should be lowercased.

## Notes

> :point_right: **Note**: Notes should be made by starting the line with the
following Markdown:

~~~
> :point_right: **Note**:
~~~

## TODOs

"TODO" items should be marked by starting the line with the
following Markdown:

~~~
> :construction: **TODO**:
~~~

This will result in a "TODO" item like this:

> :construction: **TODO**: Adjust this page for use of GitHub Markdown (since 2020)

## Emoji

GitHub-flavored emoji are enabled using the
[Jemoji](https://github.com/jekyll/jemoji) Ruby gem.

## Bookmarks & Links

For internal links, please used relative paths to the corresponding Markdown 
file as the Markdown link path rather than specifying the full URL.

Anchors are generated by Jekyll for sections using the section header text in
lowercase with hyphens instead of spaces.

> :construction: **TODO**: search our pages for "(§)" and fix the links.

## Previewing Changes Locally

Because of the latency in GitHub Pages rendering changes, it can be useful to 
run a Jekyll instance locally to preview changes.

### Setup

GitHub Pages provides a list of
[dependency versions](https://pages.github.com/versions/) used in order
to allow local environments to match exactly. Since Jekyll is a Ruby project,
setup details depend on gems (code packages), Bundler (dependency management for
execution), and the version of Ruby.

[rbenv](https://www.ruby-lang.org/en/documentation/installation/#rbenv) is one
of the few different ways to install and control the version of Ruby.  To 
install it and the required `ruby-build` plugin:
```bash
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
cd ~/.rbenv && src/configure && make -C src # Optional but greatly speeds up certain operations
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
```
```bash
mkdir -p "$(rbenv root)"/plugins
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build
```

To install specific Ruby version that GitHub Pages uses:
```bash
rbenv versions  # list all Ruby versions available
rbenv install <version-num>  # install GH Pages Ruby version
rbenv versions  # list all Ruby versions after installing
```

To activate the version of Ruby:
```bash
rbenv init  # OR:  eval "$(rbenv init -)"
rbenv shell <version-num>
rbenv versions  # verify the specified version is in use
```

To install [Bundler](https://bundler.io/):
```bash
gem install bundler
```

The simplest way to ensure that
transitive dependency versions are included correctly is to just specify the
`github-pages` gem. This is already configured in `Gemfile` in the root
directory. Thus, to ensure that the Ruby shell has the correct versions of
dependencies downloaded and cached, in the root directory (`/docs`), run:
```bash
cd <ICU>/docs  # change to User Guide docs root directory
bundle update
```

### Running

Ensure that the specific version of Ruby has been activated. Then use Bundler
to ensure that the dependencies are downloaded in the current Ruby "shell"
instance.  Then use Bundler to execute the Jekyll server.
```bash
rbenv init  # OR:  eval "$(rbenv init -)"
rbenv shell <version-num>
cd <ICU>/docs  # change to User Guide docs root directory
bundle update
bundle exec jekyll server
```

Jekyll will take several seconds to generate HTML from the Markdown, so the
Jekyll server will wait for that before being ready. Then, the rendered pages
will be available at <http://localhost:4000/icu/>.

## Previous version

The previous version of the ICU User Guide has been maintained via Google Sites. The Site
address is <http://sites.google.com/site/icuprojectuserguide/>