---
source_url: https://google.github.io/styleguide/docguide/READMEs.html
fetched_at: 2026-02-02T16:06:10.523243
---

# styleguide

About README.md files.

A README is a short summary of the contents of a directory. The contents of the file are displayed in GitHub and Gitiles when you view the contents of the containing directory. README files provide critical information for people browsing your code, especially first-time users.

This document covers how to create README files that are readable with GitHub and Gitiles.

**README files must be named README.md.** The file name

`.md`

extension and is case sensitive.For example, the file /README.md is rendered when you view the contents of the containing directory:

https://github.com/google/styleguide/tree/gh-pages

Also `README.md`

at `HEAD`

ref is rendered by Gitiles when displaying repository
index:

https://gerrit.googlesource.com/gitiles/

Unlike all other Markdown files, `README.md`

files should not be located inside
your product or library’s documentation directory. `README.md`

files should be
located in the top-level directory for your product or library’s actual
codebase.

All top-level directories for a code package should have an up-to-date
`README.md`

file. This is especially important for package directories that
provide interfaces for other teams.

At a minimum, your `README.md`

file should contain a link to your user- and/or
team-facing documentation.

Every package-level `README.md`

should include or point to the following
information:

`bazel run`

or `bazel test`

commands, etc.