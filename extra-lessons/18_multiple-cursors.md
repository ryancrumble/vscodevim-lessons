# Multiple Cursors: Edit Everywhere at Once!

Imagine needing to rename a variable that appears multiple times, add the same attribute to several HTML tags, or change the formatting of similar lines. Doing these one by one is tedious. **Multiple Cursors** let you make the same edit in many places simultaneously.

> **VSCode Context:** VSCode has excellent built-in multiple cursor support. The VSCode Vim extension cleverly integrates with this. While traditional Vim doesn't have native multiple cursors in the same way, VSCode Vim provides commands to leverage VSCode's functionality while staying in a Vim-like workflow.

Let's learn how to command this multi-cursor magic!

> Remember you can find the solutions by searching for /Solutions. To come back use <CTRL-O>.

## Adding Cursors with `gb`

The primary VSCode Vim command for creating multiple cursors based on your selection is `gb`.

1.  Place your cursor on an occurrence of the word/text you want to select.
2.  Press `gb`. This selects the current word and adds a _second_ cursor at the _next_ occurrence of that same word.
3.  Press `gb` again to add a _third_ cursor at the _next_ occurrence, and so on.
4.  Once you have cursors at all desired locations, you can use Vim commands (like `c` to change, `i` to insert, `a` to append, `x` to delete, etc.) to edit all locations at once.
5.  Press `<Esc>` **twice** (usually) to exit multiple cursor mode and return to a single cursor in Normal mode.

Let's try it out.

````javascript
// 1. We need to rename the variable `oldVar` to `newVar` everywhere it appears.
//    Place your cursor on the first `oldVar`. Use `gb` repeatedly to select
//    all three occurrences. Then use `c` (change) to rename them all to `newVar`.

//  start here
//   /
//  /
// v
function processLegacyData() {
  let oldVar = fetchData();
  if (oldVar.status === 'valid') {
    transformData(oldVar);
  }
  return oldVar;
}

function fetchData() { return { status: 'valid', value: 10 }; }
function transformData(data) { console.log("Transforming:", data); }
gb is fantastic for quickly selecting multiple instances of the same word.Editing with Multiple CursorsOnce you have multiple cursors active, you can perform many standard Vim operations simultaneously:c{motion} or ciw, caw, etc.: Change text at all cursors.i or a: Enter Insert mode at all cursors. Type your text, and it appears everywhere.x, dw, d$, etc.: Delete text at all cursors.I or A: Insert at the beginning/end of the line for all selected lines (if cursors are on different lines).<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>

<script>
  // Some script logic
</script>
VSCode Native Multi-Cursor CommandsRemember, VSCode Vim leverages VSCode's features. You can also use VSCode's native ways to create multiple cursors, and Vim commands will often work as expected:Alt+Click (or Option+Click on Mac): Place additional cursors manually wherever you click.Ctrl+Alt+Down/Up (or Cmd+Option+Down/Up on Mac): Create a column of cursors above or below the current line.Ctrl+D (or Cmd+D on Mac): Select the current word, then press again to select the next occurrence (very similar to gb).Try using Ctrl+D / Cmd+D for this next exercise.# 3. Refactor the print statements. We want to change `print("Log:")` to
#    `logger.info(`. Place your cursor on the first `print`. Use `Ctrl+D` (Cmd+D)
#    twice to select all three `print` occurrences. Then use `c` to change
#    them to `logger.info`, add the opening parenthesis, and press `<Esc>` twice.
#    (You'll need to fix the closing parenthesis separately).

#  start here
#   /
#  /
# v
class TaskRunner:
  def run_task_alpha(self):
    print("Log: Starting Alpha")
    # ... task alpha logic ...
    print("Log: Alpha finished")

  def run_task_beta(self):
    print("Log: Starting Beta")
    # ... task beta logic ...

# Assume logger is defined elsewhere
# import logging
# logger = logging.getLogger(__name__)
Exiting Multi-Cursor ModeAs mentioned, pressing <Esc> usually returns you to Normal mode at each cursor location. Pressing <Esc> a second time typically collapses all cursors back into a single cursor at the primary location (where you started or the last one added).Multiple cursors, especially combined with Vim's editing power, provide an incredibly efficient way to handle repetitive edits across your codebase. Experiment with gb and VSCode's native commands to find the workflows that suit you best!Solutions// 1. We need to rename the variable `oldVar` to `newVar` everywhere it appears.
//    Place your cursor on the first `oldVar`. Use `gb` repeatedly to select
//    all three occurrences. Then use `c` (change) to rename them all to `newVar`.

//  start here
//   /
//  /
// v (on first 'oldVar') gbgb c newVar <Esc><Esc>
function processLegacyData() {
  let oldVar = fetchData();
  if (oldVar.status === 'valid') {
    transformData(oldVar);
  }
  return oldVar;
}

function fetchData() { return { status: 'valid', value: 10 }; }
function transformData(data) { console.log("Transforming:", data); }
```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>

<script>
  // Some script logic
</script>
```python
# 3. Refactor the print statements. We want to change `print("Log:")` to
#    `logger.info(`. Place your cursor on the first `print`. Use `Ctrl+D` (Cmd+D)
#    twice to select all three `print` occurrences. Then use `c` to change
#    them to `logger.info`, add the opening parenthesis, and press `<Esc>` twice.
#    (You'll need to fix the closing parenthesis separately).

#  start here
#   /
#  /
# v (on first 'print') <Cmd-D><Cmd-D> c logger.info(<Esc><Esc>
class TaskRunner:
  def run_task_alpha(self):
    print("Log: Starting Alpha")
    # ... task alpha logic ...
    print("Log: Alpha finished")

  def run_task_beta(self):
    print("Log: Starting Beta")
    # ... task beta logic ...

# Assume logger is defined elsewhere
# import logging
# logger = logging.getLogger(__name__)
````
