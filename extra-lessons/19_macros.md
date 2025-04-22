# Reusable Editing with Macros: Record, Replay, Repeat!

You've learned motions, commands, splits, and even multiple cursors. But what if you have a complex, multi-step editing task that you need to perform repeatedly, perhaps on multiple lines or in different files? Manually repeating those steps is slow and error-prone. This is where **Macros** shine!

A Vim macro allows you to record a sequence of keystrokes (Normal mode commands, Insert mode text, movements, etc.) into a register and then replay that exact sequence on demand. It's like creating your own temporary, custom command on the fly.

> **VSCode Context:** Macros work very well in VSCode Vim! The recording and playback mechanisms are generally the same as in traditional Vim.

Let's learn how to record and unleash these editing automatons!

> Remember you can find the solutions by searching for /Solutions. To come back use <CTRL-O>.

## Recording a Macro (`q`)

Recording a macro involves three steps:

1.  Press `q` followed by the register you want to record into (e.g., `a`, `b`, `c`...). Registers `a-z` are available. You'll see "recording @{register}" appear at the bottom.
2.  Perform the sequence of Vim commands exactly as you want them recorded. Every keystroke (in Normal, Insert, or Visual mode) is captured.
3.  Press `q` again (while in Normal mode) to stop recording.

The entire sequence is now stored in the register you chose.

## Replaying a Macro (`@`)

To replay the macro stored in a register:

1.  Position your cursor where you want the macro to start.
2.  Press `@` followed by the register name (e.g., `@a`, `@b`).

Vim will execute the exact sequence of keystrokes you recorded.

## Replaying the Last Macro (`@@`)

Often, you'll want to replay the _most recently executed_ macro again. Vim provides a handy shortcut:

- `@@`: Replays the last macro that was invoked with `@`.

This is incredibly useful for applying the same change line after line.

Let's practice recording and replaying.

````javascript
// 1. We have a list of constants that need to be exported.
//    On the first line (`const MAX_HEALTH`), record a macro into register 'a' that:
//    - Goes to the start of the line (`0`)
//    - Inserts the text `export ` (`Iexport <Esc>`)
//    - Moves down to the next line (`j`)
//    Stop recording. Then, replay the macro using `@a` on the second line.
//    Finally, use `@@` to apply it to the third line.

//  start here
//   /
//  /
// v
const MAX_HEALTH = 100;
const MAX_MANA = 50;
const BASE_DAMAGE = 10;

function calculateAttack() {
  // uses BASE_DAMAGE
}
Macros are perfect for applying consistent formatting or changes across multiple lines.Appending to a MacroWhat if you recorded a macro but forgot a step or want to add more commands later? You can append to an existing macro:Press q followed by the UPPERCASE version of the register you want to append to (e.g., A to append to register a).Perform the additional commands you want to add.Press q again to stop recording.The new commands will be added to the end of the sequence already stored in that register.Using Counts with Macros ({count}@)You can execute a macro multiple times in succession by prefixing the @ command with a count:3@a: Executes the macro in register a three times.10@@: Executes the last-run macro ten times.This is extremely powerful for applying changes to a known number of subsequent lines or items.Let's try a more complex example using counts.# 2. We have tuples representing items, but we want to format them as
#    dictionary entries like `'name': {'cost': cost, 'weight': weight},`.
#    On the first item line (`("Sword", 50, 5)`), record a macro into register 'w' that:
#    - Deletes the surrounding parentheses `ds(` (requires vim-surround) OR manually delete `x` `f)` `x`
#    - Changes the inner word (the name) to be quoted `'Sword'` (`ciw'<C-R>"'<Esc>`)
#      (Note: <C-R>" pastes the text that was just changed/deleted)
#    - Appends `: {'cost': ` (`A: {'cost': <Esc>`)
#    - Moves to the first number (`f,w`)
#    - Appends `, 'weight': ` (`,a, 'weight': <Esc>`)
#    - Moves to the second number (`f,w`)
#    - Appends `},` (`a},<Esc>`)
#    - Moves down to the start of the next line (`j0`)
#    Stop recording. Then, execute this macro for the remaining 2 lines using a count.

#  start here
#   /
#  /
# v
items_data = [
    ("Sword", 50, 5),
    ("Shield", 30, 10),
    ("Potion", 5, 1),
]

# Processed items should look like:
# 'Sword': {'cost': 50, 'weight': 5},
# 'Shield': {'cost': 30, 'weight': 10},
# 'Potion': {'cost': 5, 'weight': 1},
Macros truly shine when dealing with structured, repetitive text transformations. They might seem complex at first, but mastering them unlocks a new level of editing automation. Think of them as your personal editing robots!Solutions// 1. We have a list of constants that need to be exported.
//    On the first line (`const MAX_HEALTH`), record a macro into register 'a' that:
//    - Goes to the start of the line (`0`)
//    - Inserts the text `export ` (`Iexport <Esc>`)
//    - Moves down to the next line (`j`)
//    Stop recording. Then, replay the macro using `@a` on the second line.
//    Finally, use `@@` to apply it to the third line.

//  start here
//   /
//  /
// v (on first const line) qa 0 Iexport <Esc> j q j@aj@@
const MAX_HEALTH = 100;
const MAX_MANA = 50;
const BASE_DAMAGE = 10;

function calculateAttack() {
  // uses BASE_DAMAGE
}
```python
# 2. We have tuples representing items, but we want to format them as
#    dictionary entries like `'name': {'cost': cost, 'weight': weight},`.
#    On the first item line (`("Sword", 50, 5)`), record a macro into register 'w' that:
#    - Deletes the surrounding parentheses `ds(` (requires vim-surround) OR manually delete `x` `f)` `x`
#    - Changes the inner word (the name) to be quoted `'Sword'` (`ciw'<C-R>"'<Esc>`)
#      (Note: <C-R>" pastes the text that was just changed/deleted)
#    - Appends `: {'cost': ` (`A: {'cost': <Esc>`)
#    - Moves to the first number (`f,w`)
#    - Appends `, 'weight': ` (`,a, 'weight': <Esc>`)
#    - Moves to the second number (`f,w`)
#    - Appends `},` (`a},<Esc>`)
#    - Moves down to the start of the next line (`j0`)
#    Stop recording. Then, execute this macro for the remaining 2 lines using a count.

#  start here
#   /
#  /
# v (on Sword line) qw ds( ciw'<C-R>"'<Esc> A: {'cost': <Esc> f,w ,a, 'weight': <Esc> f,w a},<Esc> j0 q j2@w
items_data = [
    ("Sword", 50, 5),
    ("Shield", 30, 10),
    ("Potion", 5, 1),
]

# Processed items should look like:
# 'Sword': {'cost': 50, 'weight': 5},
# 'Shield': {'cost': 30, 'weight': 10},
# 'Potion': {'cost': 5, 'weight': 1},
````
