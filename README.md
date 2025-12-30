# ThePrimeagen's init.lua - Neovim Configuration

A comprehensive Neovim configuration focused on developer productivity, featuring LSP support, powerful fuzzy finding, Git integration, and debugging capabilities.

## Prerequisites

**Required:**
- [Neovim](https://neovim.io/) (>= 0.9.0)
- [ripgrep](https://github.com/BurntSushi/ripgrep) - Required for Telescope fuzzy finding
- Git - For plugin management and Fugitive

**Optional (auto-installed by plugins):**
- Node.js - For some LSP servers
- Go - For Go language support
- Various language toolchains for LSP support

## Quick Start

1. Clone this repository to your Neovim config directory:
```bash
git clone <your-repo-url> ~/.config/nvim
```

2. Launch Neovim - [lazy.nvim](https://github.com/folke/lazy.nvim) will automatically install on first launch

3. Plugins will install automatically. Restart Neovim after installation completes.

[Video walkthrough of this configuration](https://www.youtube.com/watch?v=w7i4amO_zaE)

---

## 📁 Configuration Structure

```
init.lua                          # Entry point - loads theprimeagen module
lua/theprimeagen/
  ├── init.lua                    # Core config: autocommands, LSP keybinds, netrw
  ├── set.lua                     # Editor settings (line numbers, tabs, undo)
  ├── remap.lua                   # Custom keybindings
  ├── lazy_init.lua              # Plugin manager bootstrap
  └── lazy/                       # Plugin configurations
      ├── init.lua                # Core plugins (plenary, cellular-automaton)
      ├── lsp.lua                 # LSP, completion, formatting
      ├── telescope.lua           # Fuzzy finder
      ├── treesitter.lua          # Syntax highlighting
      ├── fugitive.lua            # Git integration
      ├── colors.lua              # Color schemes
      └── [other plugins...]
```

---

## ⚙️ Core Configuration Files

### `lua/theprimeagen/set.lua` - Editor Settings

**What it does:** Configures Neovim's core behavior and appearance.

**Key settings:**
- **Line numbers:** Absolute + relative line numbers for efficient navigation
- **Indentation:** 4 spaces, smart auto-indent
- **No line wrapping:** Keep long lines visible
- **Persistent undo:** Unlimited undo history saved to `~/.vim/undodir`
- **Search:** Incremental search without highlight persistence
- **Scrolloff:** Keep 8 lines visible above/below cursor
- **Color column:** Visual guide at 80 characters

**Keep if:** You want sensible defaults optimized for coding
**Remove if:** You prefer different indentation, line wrapping, or Vim defaults

---

### `lua/theprimeagen/remap.lua` - Custom Keybindings

**What it does:** Defines custom keyboard shortcuts for improved workflow.

**Notable mappings:**
- `<leader>pv` → File explorer (`:Ex`)
- `J`/`K` in visual mode → Move selected lines up/down
- `<C-d>`/`<C-u>` → Half-page jumps with cursor centering
- `<leader>y`/`<leader>Y` → Copy to system clipboard
- `<leader>d` → Delete without yanking to clipboard
- `<leader>s` → Find and replace word under cursor
- `<leader>x` → Make current file executable
- Error handling snippets: `<leader>ee`, `<leader>ef`, `<leader>el`

**Keep if:** You like these workflow optimizations and tmux integration
**Remove if:** You want standard Vim keybindings or have your own mappings

---

### `lua/theprimeagen/init.lua` - Core Autocommands & Settings

**What it does:** Sets up automatic behaviors and LSP keybindings.

**Features:**
- **Yank highlighting:** Brief flash when yanking text (visual feedback)
- **Auto-trim whitespace:** Removes trailing spaces on save
- **Color scheme switching:** Uses tokyonight for Zig files, rose-pine for others
- **LSP keybindings:** Activated when LSP attaches to buffer
  - `gd` → Go to definition
  - `K` → Hover documentation
  - `<leader>vca` → Code actions
  - `<leader>vrn` → Rename symbol
  - `[d`/`]d` → Navigate diagnostics
- **netrw settings:** Disables banner, sets window size
- **Templ filetype:** Registers `.templ` extension

**Keep if:** You want automatic code quality improvements and LSP integration
**Remove if:** You want manual control or different LSP keybindings

---

## 🔌 Plugins Overview

### Essential Plugins (Core Functionality)

#### **Telescope** - `lua/theprimeagen/lazy/telescope.lua`
**Purpose:** Fuzzy finder for files, text, and more  
**Why keep:** Essential for navigating large codebases quickly  
**Why remove:** If you prefer native file navigation or alternatives like fzf

**Keybindings:**
- `<leader>pf` → Find files
- `<C-p>` → Git files
- `<leader>ps` → Live grep
- `<leader>pws`/`<leader>pWs` → Grep word under cursor

---

#### **LSP (Language Server Protocol)** - `lua/theprimeagen/lazy/lsp.lua`
**Purpose:** Intelligent code completion, diagnostics, formatting  
**Why keep:** Core feature for modern development - provides IntelliSense, error checking, refactoring  
**Why remove:** If you prefer simpler text editing without IDE features

**Includes:**
- **nvim-lspconfig** - LSP client configuration
- **mason.nvim** - LSP server installer
- **nvim-cmp** - Completion engine
- **LuaSnip** - Snippet engine
- **conform.nvim** - Code formatting
- **fidget.nvim** - LSP progress notifications

**Pre-configured LSP servers:**
- `lua_ls` - Lua
- `rust_analyzer` - Rust
- `gopls` - Go
- `vtsls` - TypeScript/JavaScript
- `tailwindcss` - Tailwind CSS

**Keybindings:**
- `<leader>f` → Format buffer
- `<C-y>` → Confirm completion
- `<C-Space>` → Trigger completion

---

#### **Treesitter** - `lua/theprimeagen/lazy/treesitter.lua`
**Purpose:** Advanced syntax highlighting and code understanding  
**Why keep:** Dramatically improves syntax highlighting accuracy and enables structure-aware editing  
**Why remove:** If you have performance issues or prefer basic syntax highlighting

**Features:**
- **Parsers installed:** JavaScript, TypeScript, Lua, Rust, Go, C, Bash
- **treesitter-context:** Shows current function/class at top of screen
- **Smart disabling:** Disables for large files (>100KB) and HTML
- **Templ support:** Custom parser for Templ template language

---

#### **Fugitive** - `lua/theprimeagen/lazy/fugitive.lua`
**Purpose:** Git integration directly in Neovim  
**Why keep:** Best-in-class Git workflow without leaving editor  
**Why remove:** If you prefer command-line Git or GUI tools

**Keybindings:**
- `<leader>gs` → Git status
- `<leader>p` (in fugitive) → Git push
- `<leader>P` (in fugitive) → Git pull --rebase
- `gu`/`gh` → Accept changes in merge conflicts

---

### UI & Visual Plugins

#### **Colors** - `lua/theprimeagen/lazy/colors.lua`
**Purpose:** Color scheme options  
**Why keep:** For visual customization and eye comfort  
**Why remove:** To reduce clutter if you only use one theme

**Themes included:**
- **rose-pine** (default) - Warm, low-contrast theme
- **tokyonight** - Popular dark theme with variants
- **gruvbox** - Retro, warm theme
- **brightburn** - Alternative theme

**Customization:** Transparent background enabled for terminal transparency

---

#### **Zen Mode** - `lua/theprimeagen/lazy/zenmode.lua`
**Purpose:** Distraction-free writing mode  
**Why keep:** Great for focus during documentation or focused coding  
**Why remove:** If you never use distraction-free mode

**Keybindings:**
- `<leader>zz` → Toggle zen mode (90 chars width, line numbers)
- `<leader>zZ` → Full zen mode (80 chars, no line numbers)

---

#### **Undotree** - `lua/theprimeagen/lazy/undotree.lua`
**Purpose:** Visual undo history tree  
**Why keep:** Powerful for navigating complex editing history  
**Why remove:** If you rarely need complex undo operations

**Keybinding:** `<leader>u` → Toggle undo tree

---

#### **Trouble** - `lua/theprimeagen/lazy/trouble.lua`
**Purpose:** Pretty list for diagnostics, quickfix, location lists  
**Why keep:** Clean interface for viewing errors and warnings  
**Why remove:** If you prefer default quickfix window

**Keybindings:**
- `<leader>tt` → Toggle trouble
- `[t`/`]t` → Navigate trouble items

---

### Development Tools

#### **DAP (Debug Adapter Protocol)** - `lua/theprimeagen/lazy/dap.lua`
**Purpose:** Full debugging support with breakpoints, stepping, variables  
**Why keep:** Essential for complex debugging tasks  
**Why remove:** If you debug with print statements or external tools

**Keybindings:**
- `<F8>` → Continue
- `<F10>` → Step over
- `<F11>` → Step into
- `<F12>` → Step out
- `<leader>b` → Toggle breakpoint
- `<leader>dr` → Toggle REPL UI
- `<leader>ds` → Toggle stacks UI

**Includes:** nvim-dap-ui for visual debugging interface, mason-nvim-dap for debugger installation

---

#### **Neotest** - `lua/theprimeagen/lazy/neotest.lua`
**Purpose:** Test runner with debugging integration  
**Why keep:** Streamlined test execution and debugging from editor  
**Why remove:** If you run tests from command line

**Keybindings:**
- `<leader>tr` → Run nearest test
- `<leader>ts` → Run test suite
- `<leader>td` → Debug nearest test
- `<leader>tv` → Toggle test summary

**Note:** Currently configured for Go tests (neotest-golang adapter)

---

### Utilities & Extras

#### **Plenary** - `lua/theprimeagen/lazy/init.lua`
**Purpose:** Lua utility library (required by many plugins)  
**Why keep:** Dependency for Telescope and other plugins  
**Why remove:** Only if you remove all plugins that depend on it

---

#### **Cellular Automaton** - `lua/theprimeagen/lazy/init.lua`
**Purpose:** Fun animation effects  
**Why keep:** For entertainment value  
**Why remove:** If you want a minimal config

**Keybinding:** `<leader>ca` → Make it rain animation

---

#### **Cloak** - `lua/theprimeagen/lazy/cloak.lua`
**Purpose:** Hides sensitive values in .env files and secrets  
**Why keep:** Security - prevents accidentally leaking secrets on screen  
**Why remove:** If you don't work with environment files

**Files monitored:** `.env*`, `wrangler.toml`, `.dev.vars`

---

#### **Conform** - `lua/theprimeagen/lazy/conform.lua`
**Purpose:** Async formatting with format-on-save  
**Why keep:** Consistent code style without manual formatting  
**Why remove:** If you prefer manual formatting control

**Formatters configured:**
- C/C++ → clang-format
- Lua → stylua
- Go → gofmt
- JavaScript/TypeScript → prettier
- Elixir → mix

---

#### **LuaSnip & Snippets** - `lua/theprimeagen/lazy/snippets.lua`
**Purpose:** Code snippet expansion  
**Why keep:** Speeds up repetitive code patterns  
**Why remove:** If you don't use snippets

**Keybindings:**
- `<C-s>e` → Expand snippet
- `<C-s>;` → Jump forward
- `<C-s>,` → Jump backward

---

#### **Vim Be Good** - `lua/theprimeagen/lazy/vimbegood.lua`
**Purpose:** Vim motion practice game  
**Why keep:** Fun way to improve Vim skills  
**Why remove:** Once you're comfortable with motions

---

### Language-Specific Plugins

#### **Jai.vim** - `lua/theprimeagen/lazy/jai.lua`
**Purpose:** Syntax support for Jai programming language  
**Why keep:** If you write Jai code  
**Why remove:** If you don't use Jai

---

#### **Golf** - `lua/theprimeagen/lazy/golf.lua`
**Purpose:** Code golf plugin  
**Why keep:** For code golf competitions  
**Why remove:** If you don't do code golf

---

#### **PHP.nvim** - `lua/theprimeagen/lazy/tj.lua`
**Purpose:** Enhanced PHP support  
**Why keep:** If you work with PHP  
**Why remove:** If you don't use PHP

---

### Local Plugins (Optional)

#### `lua/theprimeagen/lazy/local.lua`
**Purpose:** Personal plugins loaded from local directories  
**Why keep:** If you develop these plugins or have them installed  
**Why remove:** These won't work without local plugin files

**Plugins referenced:**
- **Harpoon** - Quick file navigation (marks for files)
- **99** - Custom AI-powered coding assistant
- **the-stru** - Custom plugin

**Note:** These require local repositories at `~/personal/[plugin-name]`

---

### Disabled Plugins

#### **Supermaven** - `lua/theprimeagen/lazy/supermaven.lua`
**Status:** Commented out  
**Purpose:** AI code completion  
**To enable:** Uncomment the configuration block

---

#### **Peek** - `lua/theprimeagen/lazy/peek.lua`
**Status:** Commented out  
**Purpose:** Markdown preview  
**To enable:** Uncomment and install Deno

---

## 🎯 Customization Guide

### Adding Language Support

1. Add LSP server to `lua/theprimeagen/lazy/lsp.lua`:
```lua
ensure_installed = {
    -- ... existing
    "your_language_server",
}
```

2. Add Treesitter parser to `lua/theprimeagen/lazy/treesitter.lua`:
```lua
ensure_installed = {
    -- ... existing
    "your_language",
}
```

3. Add formatter to `lua/theprimeagen/lazy/conform.lua` (optional):
```lua
formatters_by_ft = {
    your_language = { "your_formatter" },
}
```

### Removing Unwanted Plugins

Simply delete or comment out the plugin file in `lua/theprimeagen/lazy/`. Lazy.nvim will automatically clean up unused plugins on next launch.

### Changing Leader Key

Currently set to `<Space>` in `lua/theprimeagen/remap.lua`. Change the first line:
```lua
vim.g.mapleader = " "  -- Change to your preferred key
```

---

## 🔧 Maintenance

- **Update plugins:** `:Lazy update`
- **Check plugin health:** `:checkhealth`
- **LSP info:** `:LspInfo`
- **Mason (LSP installer):** `:Mason`
- **Treesitter info:** `:TSInstallInfo`

---

## 📚 Additional Resources

- [Lazy.nvim Documentation](https://github.com/folke/lazy.nvim)
- [LSP Configuration Guide](https://github.com/neovim/nvim-lspconfig/blob/master/doc/server_configurations.md)
- [Original Setup Video](https://www.youtube.com/watch?v=w7i4amO_zaE)

---

## 💡 Philosophy

This configuration prioritizes:
1. **Productivity** - Powerful tools for professional development
2. **Speed** - Fast fuzzy finding and navigation
3. **Minimal** - Only include what's actively used
4. **Modern** - LSP, Treesitter, DAP over legacy Vim plugins
5. **Keyboard-driven** - All features accessible via keybindings

---

## Historical Change Log

* [33eee9ad](https://github.com/ThePrimeagen/init.lua/commit/33eee9ad0c035a92137d99dae06a2396be4c892e) initial commits
* [cb210006](https://github.com/ThePrimeagen/init.lua/commit/cb210006356b4b613b71c345cb2b02eefa961fc0) netrw, autogroups for yank highlighting, and auto remove whitespace
* [c8c0bf4a](https://github.com/ThePrimeagen/init.lua/commit/c8c0bf4aeacd0bd77136d9c5ee490680515a106b) zenmode.  i really like this plugin
* [81c770d2](https://github.com/ThePrimeagen/init.lua/commit/81c770d2d2e32e59916b39c7f5babbc8560f7a82) copilot testing
* [4a96e645](https://github.com/ThePrimeagen/init.lua/commit/4a96e6457b0a0241ca7361ce62177aa6b9a33a38) fugitive mappings for push and pull
* [a3bad06a](https://github.com/ThePrimeagen/init.lua/commit/a3bad06a4681c322538d609aa1c0bd18880f77c6) disabled eslint.  driving me crazy

