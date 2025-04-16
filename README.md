# joplin.vim

This is a plugin to use [joplin.app](https://joplinapp.org/) in Neovim.

## Requirements

1. joplin.app ([installation instructions](https://joplinapp.org/help/install/))

2. python3 with the `neovim` module installed

```bash
pip3 install neovim
```

## Install

- [vim-plug](https://github.com/junegunn/vim-plug)
```vim
Plug 'tenfyzhong/joplin.vim'
```

- [packer.nvim](https://github.com/wbthomason/packer.nvim)
```
use {'Hegghammer/joplin.nvim'}
```

- [lazy.nvim](https://github.com/folke/lazy.nvim)
```lua
require("lazy").setup({
  {
    'Hegghammer/joplin.nvim', 
  },
})
```

## Setup

1. Enable your joplin.app's Web Clipper service (Tools > Options > Web Clipper) and copy the token.
   
2. Create a `secrets.lua` file somewhere it won't get exposed and add the token.

```secrets.lua
vim.g.joplin_token = "TOKEN"
```

3. Source the secrets file in `init.lua`:

```init.lua
dofile("/path/to/your/secrets.lua")
```

After you enable the Web Clipper service, it will listen on port 41184 by default. This plugin will connect to the default port when the plugin start. If your joplin.app listen on other port, you should set the port to `g:joplin_port`.

## Launch

Note that your joplin.app must be open and running for the plugin to work. 

Run command `Joplin` or `JoplinWinOpen` to open the `tree.joplin` window. It
contains all notebooks and notes.

Get a wider pane by adding the `CTRL + w >` sequence to the `:Joplin` command, for example like so:

```lua
vim.keymap.set("n", "<leader>j", ":Joplin<cr>50<c-w>>", { noremap = true, silent = true, desc = "Open [J]oplin" })
```

Or launch directly from the command line with a specific width:

```bash
nvim -c "Joplin" -c "vertical resize +50"
```

## Usage

Main keybindings:
- Toggle open notebook with `ENTER` or `o`  
- Open note with `ENTER` or `o` or `s`
- `R`: refresh
- `an`: add note
- `?`: see all commands.

## Reference

```
----------------------------
Note node mappings~
double-click: open in prev window
<CR>: open in prev window
o: open in prev window
t: open in new tab
i: open split
s: open vsplit
ct: switch between note and todo type
cc: switch todo completed

----------------------------
Notebook node mappings~
double-click: open & close notebook
<CR>: open & close notebook
o: open & close notebook
O: recursively open notebook
x: close parent of node
X: close all child notebooks of current notebook recursively
r: refresh current notebook
R: refresh current root

----------------------------
Tree navigation mappings~
P: go to root
p: go to parent
K: go to first child
J: go to last child
<C-j>: go to next sibling
<C-k>: go to prev sibling

----------------------------
Other mappings~
ab: add a notebook
an: add a note
at: add a todo
dd: delete a node
cp: copy a node
mv: move a node
rn: rename a node
q: close the tree.joplin window
?: toggle help
```
