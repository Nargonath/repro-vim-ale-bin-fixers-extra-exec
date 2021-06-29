<div align="center">
  <h1>repro-vim-ale-bin-fixers-extra-exec</h1>
  <strong>This repo is to reproduce a bug I noticed while using the vim-ale plugin</strong>
</div>

<hr>

# Bug

The bug occurs when you use this [ `vim-ale` ](https://github.com/dense-analysis/ale) plugin configuration:

```vim
let g:ale_fixers = {
    \ 'javascript': ['prettier'],
\}

```

In a JS project, if you have the configuration above while one of your dependency have a dependency on a fixer you defined in your Vim configuration but that is not directly a dependency of your own project it is still getting run even though that's not your project configuration. I'd expect `vim-ale` to run only the enabled fixers that are present but also that are either available globally in your system or mentioned in your `package.json` dependencies.

## Test case

I included a test file in this project: `index.js`. If you open this file with a vim instance using the above configuration and run `:ALEFix` the content of the file will be fixed to:

![image](https://user-images.githubusercontent.com/583657/123845330-598e3f80-d914-11eb-967c-afba7bd796d9.png)

I don't have a global `prettier` executable available:

![image](https://user-images.githubusercontent.com/583657/123845458-7fb3df80-d914-11eb-8781-d09ec06aef90.png)

Here the result of `npm ls prettier` in the project:

![image](https://user-images.githubusercontent.com/583657/123845680-c3a6e480-d914-11eb-869b-98a9d761d880.png)

For this case I would expect `vim-ale` to not fix the file since no `prettier` executable are intentionally added to the project or globally available.
