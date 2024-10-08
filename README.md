# Pretty Quickfix windows for NeoVim

nvim-pqf makes your quickfix and location list windows look nicer, thanks to a
combination of a custom `quickfixtextfunc` function and custom syntax rules for
quickfix/location list buffers.

Without nvim-pqf, your quickfix window looks like this:

![Without nvim-pqf](https://github.com/yorickpeterse/nvim-pqf/assets/86065/6635fdf3-49f0-4585-9495-34fcaffba065)

With nvim-pqf, it looks like this (colours depend on your theme of course);

![With nvim-pqf](https://github.com/yorickpeterse/nvim-pqf/assets/86065/a4098631-b2ad-424a-9990-16f2bcbe5dea)

## Features

- Better highlights for line and column numbers
- Highlights for the item type (error, warning, etc), using the same highlights
  as NeoVim's diagnostics
- File paths are aligned so messages always start at the same column, making
  them easier to read
- Works for both quickfix and location list windows
- Items (by default) only display the first line in case they contain multiple
  lines

## Requirements

- NeoVim 0.8 or newer

## Installation

First install this plugin using your plugin manager of choice. For example, when
using vim-plug use the following:

    Plug 'yorickpeterse/nvim-pqf'

Once installed, add the following Lua snippet to your `init.lua`:

    require('pqf').setup()

And that's it!

## Configuration

Each item in the quickfix list starts with a sign that indicates the type of
item, if this information is available. For example, when displaying diagnostics
an item may start with `E` for an error, and `W` for a warning.

You can configure these signs (and various other settings) as follows:

```lua
require('pqf').setup({
  signs = {
    error = { text = 'E', hl = 'DiagnosticSignError' },
    warning = { text = 'W', hl = 'DiagnosticSignWarn' },
    info = { text = 'I', hl = 'DiagnosticSignInfo' },
    hint = { text = 'H', hl = 'DiagnosticSignHint' },
  },

  -- By default, only the first line of a multi line message will be shown.
  -- When this is true, multiple lines will be shown for an entry, separated by
  -- a space
  show_multiple_lines = false,

  -- How long filenames in the quickfix are allowed to be. 0 means no limit.
  -- Filenames above this limit will be truncated from the beginning with
  -- `filename_truncate_prefix`.
  max_filename_length = 0,

  -- Prefix to use for truncated filenames.
  filename_truncate_prefix = '[...]',

  -- By default column numbers will be shown.
  -- When this is true, only line numbers will be shown
  hide_column_numbers = false,
})
```

## Tweaking the highlights

Depending on your theme, you may need to tweak the highlights used by nvim-pqf.
The following highlight groups are used:

| Group                 | Use
|:----------------------|:--------------------------
| `Directory`           | The file path
| `Number`              | Line and column numbers
| `DiagnosticSignError` | The default highlight group for error signs
| `DiagnosticSignWarn`  | The default highlight group for warning signs
| `DiagnosticSignInfo`  | The default highlight group for info signs
| `DiagnosticSignHint`  | The default highlight group for hint signs

## License

All source code in this repository is licensed under the Mozilla Public License
version 2.0, unless stated otherwise. A copy of this license can be found in the
file "LICENSE".
