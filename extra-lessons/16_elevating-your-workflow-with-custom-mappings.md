# Custom Mappings: Forging Your Own Vim Shortcuts

You've learned Vim's built-in commands, but what if you could create your _own_ commands? What if a complex sequence of keystrokes could be triggered by a simple shortcut? Welcome to the world of **custom mappings**!

Mappings allow you to assign a sequence of commands to a key or combination of keys. This is one of Vim's most powerful features for tailoring the editor to your exact needs and boosting your speed.

> **VSCode Context:** In VSCode Vim, persistent custom mappings are typically defined in your `settings.json` file within the `vim.normalModeKeyBindings`, `vim.visualModeKeyBindings`, and `vim.insertModeKeyBindings` arrays (or their non-recursive counterparts like `vim.normalModeKeyBindingsNonRecursive`). Temporary mappings for the current session can sometimes be set using the `:map` family of commands, but `settings.json` is the standard way for lasting changes.

Let's explore how to create these custom shortcuts.

> Remember you can find the solutions by searching for /Solutions. To come back use `<CTRL-O>`.

## Basic Mapping (`:map` and friends)

The fundamental command is `:map`. However, `:map` works in multiple modes (Normal, Visual, Operator-pending) and can sometimes lead to unexpected recursive behavior (a mapping triggering itself or another mapping unintentionally).

Therefore, it's **highly recommended** to use mode-specific, **non-recursive** mappings:

- `:noremap` (Normal Mode): Maps keys only in Normal mode, non-recursively. **This is usually what you want for Normal mode mappings.**
- `:vnoremap` (Visual Mode): Maps keys only in Visual mode, non-recursively.
- `:inoremap` (Insert Mode): Maps keys only in Insert mode, non-recursively.
- `:nnoremap` (Normal Mode): Alias for `:noremap`. Often preferred for clarity.

**Why non-recursive (`noremap`)?** Imagine you map `x` to `d`. If you then map `d` to something else using `:map`, pressing `x` might trigger the `d` mapping unexpectedly. `:noremap` prevents this chain reaction, ensuring your mapping does exactly what you typed. **Always prefer `noremap` unless you specifically need recursion.**

The syntax is: `:{mode}noremap {shortcut} {command_sequence}`

- `{mode}`: `n`, `v`, `i` (for `nnoremap`, `vnoremap`, `inoremap`).
- `{shortcut}`: The key or key sequence you want to press.
- `{command_sequence}`: The Vim commands that should execute when you press the shortcut. Special keys are often written within angle brackets (e.g., `<CR>` for Enter, `<Esc>` for Escape, `<Space>` for Spacebar).

### Example 1: Save Work Quickly

Constantly saving your work is crucial! Let's map the sequence `<Space>w` in Normal mode to execute the save command `:w<CR>` (write and press Enter).

```vim
:nnoremap <Space>w :w<CR>
```

### Example 2: Running Tests

Running tests frequently is good practice. Let's map `<Leader>t` (Space + t) in Normal mode to execute a command that runs your tests. We'll simulate this by using `:!echo "Running tests..."<CR>`.

```vim
:nnoremap <Leader>t :!echo "Running tests..."<CR>
```

### Example 3: Surrounding Text in Visual Mode

In Visual mode, you might want a quick way to surround the selection with parentheses. Map `<Leader>p` (Space + p) in Visual mode to execute the surround command `S(`. Remember `S` in Visual mode adds surrounds.

```vim
:vnoremap <Leader>p S(
```

### Example 4: Closing Splits Quickly

Imagine you often open a split and want to close it quickly. Map `<Leader>c` in Normal mode to close the current split/buffer (`:q<CR>`).

```vim
:nnoremap <Leader>c :q<CR>
```

Or, for consistency with split commands, map it to `Ctrl-W c`:

```vim
:nnoremap <Leader>c <C-W>c
```

## Useful Mapping Ideas

Think about repetitive actions you perform and consider mapping them:

- **Saving/Quitting**: `<Leader>w` for `:w<CR>`, `<Leader>q` for `:q<CR>`.
- **Splitting Windows**: `<Leader>sv` for `:vs<CR>`, `<Leader>sh` for `:sp<CR>`.
- **Navigating Splits**: `<Leader>h/j/k/l` for `Ctrl-W h/j/k/l`.
- **Running Linters/Formatters**: `<Leader>f` for `:%!prettier<CR>` or similar.
- **Toggling Settings**: `<Leader>n` for `:set number!<CR>`.
- **Executing Current File**: `<Leader>r` for `:!python %<CR>` (for Python).

## Solutions

### Solution 1: Save Work Quickly

```vim
:nnoremap <Space>w :w<CR>
```

### Solution 2: Running Tests

```vim
:nnoremap <Leader>t :!echo "Running tests..."<CR>
```

### Solution 3: Surrounding Text in Visual Mode

```vim
:vnoremap <Leader>p S(
```

### Solution 4: Closing Splits Quickly

```vim
:nnoremap <Leader>c :q<CR>
```

Or:

```vim
:nnoremap <Leader>c <C-W>c
```
