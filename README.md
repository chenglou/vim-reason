# Vim support for Reason/OCaml

**Note**: this is the _fallback_ [Reason](http://reasonml.github.io/) Vim editor integration for Vim 7 or Vim 8 without Python 3. If you're on NeoVim or Vim 8 with Python 3, please use [vim-reason-plus](https://github.com/reasonml-editor/vim-reason-plus) instead!

## Installing

If you are using a plugin manager, add a line such as the following to your `.vimrc`:

```
" If using NeoBundle
NeoBundle 'reasonml-editor/vim-reason'

" Or, if using Vundle
Bundle 'reasonml-editor/vim-reason'

" Or, if using Vim-Plug
Plug 'reasonml-editor/vim-reason'
```

## Formatting

The command `:ReasonPrettyPrint` invokes the binary `refmt` which must be available on your `PATH`.

You can set `g:vimreason_extra_args_expr_reason` to control the arguments
passed to `refmt` (such as `--print-width`). The contents of
`g:vimreason_extra_args_expr_reason` is a string that contains a `VimScript`
expression. This allows you do dynamically determine the formatting arguments
based on things like your window width.

```vim
" Always wrap at 90 columns
let g:vimreason_extra_args_expr_reason = '"--print-width 90"'

" Wrap at the window width
let g:vimreason_extra_args_expr_reason = '"--print-width " . ' .  "winwidth('.')"

" Wrap at the window width but not if it exceeds 120 characters.
let g:vimreason_extra_args_expr_reason = '"--print-width " . ' .  "min([120, winwidth('.')])"
```

## Key Mappings

You can create a custom function and map it to a keybinding (in your `.vimrc`)
to quickly trigger formatting, and control how the formatting occurs. To enable
keymappings *only* for `reason` files, your vim must have been compiled with
`+localmap` (`:echo has('localmap')` should output `1` if your vim supports it).

For example, the following maps `cmd + shift + m` to reformat only when editing
a `reason` file.

```vim
autocmd FileType reason map <buffer> <D-M> :ReasonPrettyPrint<Cr>
```

## Merlin

We come with [Merlin] support by default. You can check the features [here](https://github.com/ocaml/merlin/wiki/vim-from-scratch#discovering-the-shiny-features). Skip the installation procedure in that page; this plugin doesn't use it.

[Syntastic](https://github.com/vim-syntastic/syntastic) support is unobstructedly enabled here by default. [Neomake](https://github.com/neomake/neomake) support can be enabled by setting `let g:neomake_reason_enabled_makers = ['merlin']`.


## Contributing

Lots of content in the repo is copy pasted from https://github.com/ocaml/merlin/tree/v2.5.4/vim/merlin, with a few Reason-specific files added. We'll track master once Reason's global tooling uses the newest Merlin. Until then, since that release branch isn't adding retroactive fixes, there's nothing to sync anymore. You can always submit these Reason files to Merlin or something.

## LICENSE

Some files from vim-reason are based on the Rust vim plugin and so we are including that license.
