---
source_url: https://google.github.io/styleguide/vimscriptguide.xml
fetched_at: 2026-01-25T15:24:01.333327
---

Revision 1.1

Nate Soares
This is a casual version of the vimscript style guide, because
vimscript is a casual language. When submitting vim plugin code, you
must adhere to these rules. For clarifications, justifications, and
explanations about the finer points of vimscript, please refer to the
[heavy guide](vimscriptfull.xml).

It's hard to get vimscript right. Many commands depend upon the user's settings. By following these guidelines, you can hope to make your scripts portable.

Double quoted strings are semantically different in vimscript, and you probably don't want them (they break regexes).

Use double quoted strings when you need an escape sequence (such as
`"\n"`

) or if you know it doesn't matter and you need to
embed single quotes.

`=~#`

or `=~?`

operator families over the
`=~`

family.
The matching behavior depends upon the user's ignorecase and smartcase
settings and on whether you compare them with the `=~`

,
`=~#`

, or `=~?`

family of operators. Use the
`=~#`

and `=~?`

operator families explicitly
when comparing strings unless you explicitly need to honor the user's
case sensitivity settings.

`\m\C`

.
In addition to the case sensitivity settings, regex behavior depends
upon the user's nomagic setting. To make regexes act like nomagic and
noignorecase are set, prepend all regexes with `\m\C`

.

You are welcome to use other magic levels (`\v`

) and case
sensitivities (`\c`

) so long as they are intentional and
explicit.

Avoid using `:s[ubstitute]`

as it moves the cursor and
prints error messages. Prefer functions (such as
`search()`

) better suited to scripts.

For many vim commands, functions exist that do the same thing with
fewer side effects. See `:help functions()`

for a list of
built-in functions.

Always use `normal!`

instead of `normal`

. The
latter depends upon the user's key mappings and could do anything.

Avoid `:s[ubstitute]`

, as its behavior depends upon a
number of local settings.

The same applies to other commands not listed here.

Error text may be locale dependent.

Loud scripts are annoying. Message the user only when:

Vimscript has unsafe, unintuitive behavior when dealing with some
types. For instance, `0 == 'foo'`

evaluates to true.

Use strict comparison operators where possible. When comparing against
a string literal, use the `is#`

operator. Otherwise, prefer
`maktaba#value#IsEqual`

or check `type()`

explicitly.

Check variable types explicitly before using them. Use functions from
`maktaba#ensure`

, or check `maktaba#value`

or
`type()`

and throw your own errors.

Use `:unlet`

for variables that may change types,
particularly those assigned inside loops.

Use python only when it provides critical functionality, for example when writing threaded code.

Avoid using other scripting languages such as ruby and lua. We can not guarantee that the end user's vim has been compiled with support for non-vimscript languages.

maktaba removes boilerplate, including:

Group your functionality as a plugin, unified in one directory (or
code repository) which shares your plugin's name (with a "vim-" prefix
or ".vim" suffix if desired). It should be split into plugin/,
autoload/, etc. subdirectories as necessary, and it should declare
metadata in the addon-info.json format (see the
[VAM documentation](https://github.com/MarcWeber/vim-addon-manager/blob/master/doc/vim-addon-manager-additional-documentation.txt) for details).

`[!]`

and
`[abort]`

.
Autoloading allows functions to be loaded on demand, which makes startuptime faster and enforces function namespacing.

Script-local functions are welcome, but should also live in autoload/ and be called by autoloaded functions.

Non-library plugins should expose commands instead of functions. Command logic should be extracted into functions and autoloaded.

`[!]`

allows developers to reload their functions
without complaint.

`[abort]`

forces the function to halt when it encounters
an error.

`[!]`

.
General commands go in `plugin/commands.vim`

.
Filetype-specific commands go in `ftplugin/`

.

Excluding `[!]`

prevents your plugin from silently
clobbering existing commands. Command conflicts should be resolved by
the user.

Place all autocommands in augroups.

The augroup name should be unique. It should either be, or be prefixed with, the plugin name.

Clear the augroup with `autocmd!`

before defining new
autocommands in the augroup. This makes your plugin re-entrable.

`plugin/mappings.vim`

, using
`maktaba#plugin#MapPrefix`

to get a prefix.
All key mappings should be defined in
`plugin/mappings.vim`

.

Partial mappings (see :help using-<Plug>.) should be defined in
`plugin/plugs.vim`

.

Use `:setlocal`

and `&l:`

instead of
`:set`

and `&`

unless you have explicit
reason to do otherwise.

Follow google style conventions. When in doubt, treat vimscript style like python style.

This does not apply to arguments to commands.

You need not go out of your way to remove it.

Trailing whitespace is allowed in mappings which prep commands
for user input, such as
"`noremap <leader>gf :grep -f `

".

In general, use
`plugin-names-like-this`

,
`FunctionNamesLikeThis`

,
`CommandNamesLikeThis`

,
`augroup_names_like_this`

,
`variable_names_like_this`

.

Always prefix variables with their scope.

Keep them short and sweet.

Prefix script-local functions with `s:`


Autoloaded functions may not have a scope prefix.

Do not create global functions. Use autoloaded functions instead.

Prefer succinct command names over common command prefixes.

Augroup names count as variables for naming purposes.

`g:`

`s:`

`a:`

`l:`

`v:`

`b:`

`g:`

, `s:`

, and `a:`

must always
be used.

`b:`

changes the variable semantics; use it when you
want buffer-local semantics.

`l:`

and `v:`

should be used for consistency,
future proofing, and to avoid subtle bugs. They are not strictly
required. Add them in new code but don’t go out of your way to add
them elsewhere.

Revision 1.1

Nate Soares