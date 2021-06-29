<div align="center">
  <h1>repro-vim-ale-bin-fixers-extra-exec</h1>
  <strong>This repo is to reproduce a bug I noticed while using the vim-ale plugin</strong>
</div>

<hr>

# Bug

The bug occurs when you use this [ `vim-ale` ](https://github.com/dense-analysis/ale) plugin configuration:

```vim
let g:ale_fixers = {
    \ 'javascript': ['prettier', 'eslint'],
\}

```

In a JS project, if you have the configuration above while one of your dependency have a dependency on a fixer you defined in your Vim configuration but that is not directly a dependency of your own project it is still getting run even though that's not your project configuration. I'd expect `vim-ale` to run only the enabled fixers that are present but also that are either available globally in your system or mentioned in your `package.json` dependencies.
