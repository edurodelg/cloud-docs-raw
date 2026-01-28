---
source_url: https://google.github.io/styleguide/index
fetched_at: 2026-01-28T07:24:53.255678
---

# styleguide

Every major open-source project has its own style guide: a set of conventions (sometimes arbitrary) about how to write code for that project. It is much easier to understand a large codebase when all the code in it is in a consistent style.

“Style” covers a lot of ground, from “use camelCase for variable names” to
“never use global variables” to “never use exceptions.” This project
([google/styleguide](https://github.com/google/styleguide)) links to the style
guidelines we use for Google code. If you are modifying a project that
originated at Google, you may be pointed to this page to see the style guides
that apply to that project.

This project also contains [google-c-style.el](https://raw.githubusercontent.com/google/styleguide/gh-pages/google-c-style.el), an Emacs settings file
for Google style.

We used to host the cpplint tool, but we stopped making internal updates public. An open source community has forked the project, so users are encouraged to use https://github.com/cpplint/cpplint instead.

If your project requires that you create a new XML document format, the
[XML Document Format Style Guide](https://google.github.io/styleguide/xmlstyle.html) may be helpful. In addition to actual
style rules, it also contains advice on designing your own vs. adapting an
existing format, on XML instance document formatting, and on elements vs.
attributes.

The style guides in this project are licensed under the CC-By 3.0 License, which
encourages you to share these documents. See
[https://creativecommons.org/licenses/by/3.0/](https://creativecommons.org/licenses/by/3.0/) for more details.

The following Google style guide lives outside of this project:

Since projects are largely maintained in a [VCS](https://en.wikipedia.org/wiki/Version_control_system), writing good commit messages
is important to long term project health. Please refer to [How to Write a Git
Commit Message](https://cbea.ms/git-commit/) as an excellent resource. While it
explicitly refers to the Git [SCM](https://en.wikipedia.org/wiki/Source_control_management), its principles apply to any system, and many
Git conventions are trivial to translate to others.

With few exceptions, these style guides are copies of Google’s internal style
guides to assist developers working on Google owned and originated open source
projects. Changes to the style guides are made to the internal style guides
first and eventually copied into the versions found here. **External
contributions are not accepted.** Pull requests are regularly closed without
comment.

People can file [issues using the GitHub tracker](https://github.com/google/styleguide/issues). Issues that raise
questions, justify changes on technical merits, or point out obvious mistakes
may get some engagement and could in theory lead to changes, but we are
primarily optimizing for Google’s internal needs.