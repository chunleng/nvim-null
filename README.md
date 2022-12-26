# Neovim Null

This project is used to resolve Packer dependencies.

When using Packer, sometime 2 groups of totally unrelated plugins might have to
share a certain resource (e.g. common key like `<cr>` or `<tab>`) and it can be
hard to understand if we just include in one of the plugin.

Using this plugin, we can resolve it nicely by specifying codes such as below.

```lua
use {'a/snippet'}
use {'b/autopair'}
use {
    'chunleng/nvim-null'
    config = function()
        -- Resolve imap <cr>
        vim.keymap.set('i', '<cr>', function()
            local a = require('snippet')
            local b = require('autopair')
            if a.has_snippet() then
                a.expand()
            else
                b.pair()
            end
        end)
    end,
    after = {'snippet', 'autopair'},
    as = 'resolve_cr'
}
```
