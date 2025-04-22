# Command-Line Mode: Your Vim Command Center

So far, we've conquered moving around and editing text in Normal, Insert, and Visual modes. But how do you tell Vim to perform actions like saving files, searching and replacing across the entire project, running external commands, or configuring Vim itself? Enter **Command-Line Mode**.

Command-Line Mode is your control panel for Vim. You enter it by pressing `:` from Normal Mode. You'll see the colon appear at the bottom of your editor (or in a command palette in VSCode Vim), waiting for your command. After typing your command, press `Enter` to execute it.

This mode is incredibly powerful and essential for an efficient Vim workflow. Let's dive into some of the most common and useful commands.

> Remember you can find the solutions by searching for /Solutions. To come back use `<CTRL-O>`.

## File Operations: Saving, Quitting, Editing

These are the absolute basics, the bread and butter of file management.

- `:w` (`:write`): Save the current file. Like hitting `Ctrl+S` or `Cmd+S`.
- `:q` (`:quit`): Close the current file/window. Fails if there are unsaved changes.
- `:wq`: Write (save) and then quit. The classic combo.
- `:x`: Also writes and quits, but _only_ writes if the file has actually been modified. Slightly more efficient!
- `:q!`: Quit _without_ saving. Use this when you want to discard changes. Be careful!
- `:e {filename}` (`:edit {filename}`): Open a specified file for editing. If you have unsaved changes in the current file, Vim will warn you. Use `:e! {filename}` to discard changes and open the new file. (In VSCode, this often opens the file in a new tab).

```typescript
// 1. You've just drafted a new spell description for your grimoire. Save your work!
//    Then, imagine you accidentally scribbled nonsense and want to discard changes
//    without saving (though we won't actually execute the quit here, just practice typing it).
//    Finally, save and quit using the efficient method.

/**
 * Spell: Chrono-Shift Field
 * Description: Creates a localized field where time flows differently.
 * Warning: Unstable. May cause temporal paradoxes or summon time-wyrms.
 * Added by: Temporal Mage Eldrin - April 22, 2025
 */
function chronoShiftField(radius, duration) {
  console.log(
    `Warping time in a ${radius} meter radius for ${duration} seconds!`
  );
  // Safety protocols pending...
}

// Practice: Type :w<Enter>, then :q!<Enter> (mentally!), then :x<Enter>
```

## Running Shell Commands (`:!`)

Need to quickly consult the system clock or list your potion ingredients without leaving your Vim editor? Command-Line Mode has you covered. The `:!` command lets you execute any shell command.

- `:!{command}`: Executes the `{command}` in your shell. Output is displayed, then you press Enter to return to Vim.
- `:%!{command}`: Filters the entire file (`%`) through an external `{command}`. Useful for formatters or sorters (e.g., `:%!sort`).
- `:r !{command}` (`:read !{command}`): Reads the output of the `{command}` and inserts it below the current line.

```javascript
// 2. Let's check the files in our current enchanted forest directory using the shell's
//    `ls` command (or `dir` on Windows). Then, insert the current date and time
//    below the author line using the `date` command.

const scriptName = "forest_guardian_AI.js";
const author = "Dryad Coder Willow";
// Insert current date/time here

function patrolForest() {
  console.log("Scanning the woods for intruders...");
}

// First, run :!ls (or :!dir). Then, move to the line below 'author' and run :r !date
```

## The Mighty Search and Replace (`:s`)

This is one of the crown jewels of Command-Line Mode. The `:s` command (substitute) allows for powerful text replacement using regular expressions.

The basic syntax is: `:[range]s/{pattern}/{replacement}/[flags]`

- `[range]`: Specifies which lines to operate on.
  - (Omitted): Current line only.
  - `%`: The entire file. This is very common (`:%s/...`).
  - `1,10`: Lines 1 through 10.
  - `.`: The current line.
  - `$`: The last line.
  - `'<,'>`: The lines selected in the last Visual selection. (Vim automatically inserts this when you press `:` from Visual mode).
- `{pattern}`: The text or regular expression to search for.
- `{replacement}`: The text to replace the pattern with. You can use captured groups from the pattern (e.g., `\1`, `\2`).
- `[flags]`: Modify the command's behavior.
  - `g` (global): Replace all occurrences on each line within the range (without `g`, only the first occurrence per line is replaced).
  - `i` (ignore case): Makes the search case-insensitive.
  - `c` (confirm): Prompts you to confirm each replacement (`y/n/a/q/l`). Extremely useful!

```javascript
// 3. Replace the *first* occurrence of "goblin" with "hobgoblin" on the line below.

let enemyType = "goblin";
let enemyCount = 5; // A goblin! Another goblin!

function spawnEnemy() {
  // More goblin logic
}

// Practice: Type :s/goblin/hobgoblin/<Enter>
```

```python
# 4. Our alchemist apprentice consistently misspells "potion" as "postion".
#    Replace *all* occurrences of "postion" with "potion" across the *entire file* (%).
#    Make it case-insensitive (`i`) just in case, and use confirmation (`c`)
#    to check each change before applying it.

def brew_health_postion():
  ingredients = ["moonpetal", "spring water", "ruby dust"]
  print("Mixing a potent health postion...")
  return "Health Potion" # Correct spelling here

def identify_postion(flask_contents):
  if "glowing green" in flask_contents:
    return "Maybe a toxic Postion?" # Misspelled here too
  return "Unknown liquid"

# Practice: Type :%s/postion/potion/gic<Enter> (Press y or n for each match)
```

```css
/* 5. We have a block of CSS selected in Visual Mode defining styles for treasure chests.
      Let's say we selected the `.treasure-chest` block below. We want to replace all
      occurrences of "gold" with "brass" *only within the selection*, and do it globally
      (`g`) on each line without confirmation this time. */

.wooden-box {
  border: 2px solid brown;
}

.treasure-chest {
  border: 3px solid gold; /* Change this gold */
  background-color: lightgoldenrodyellow;
  box-shadow: 0 0 10px gold; /* And this gold */
  padding: 15px;
}

.mimic {
  border: 3px solid grey;
}

/* Practice: Select the lines from .treasure-chest { to the closing } in Visual Line mode (V).
   Then press : to enter Command-Line mode. Vim automatically fills in the range '<,'>.
   Complete the command to substitute 'gold' with 'brass' globally within the selection. */
```

## Working with Multiple Files (Buffers/Tabs)

Vim can handle multiple files open simultaneously. In traditional Vim, these are called "buffers". In VSCode, this often maps closely to your open editor tabs.

- `:ls` or `:buffers`: List all open buffers/tabs, showing their number/ID, status, and filename. (Behavior might vary slightly in VSCode Vim).
- `:b {number_or_name}` (`:buffer {number_or_name}`): Switch to the buffer/tab with the given number or partial name (use Tab for completion!).
- `:bn` (`:bnext`): Go to the next buffer/tab in the list.
- `:bp` (`:bprevious`): Go to the previous buffer/tab in the list.
- `:bd` (`:bdelete`): Close the current buffer/tab (like closing a tab with Ctrl+W or Cmd+W). Fails if there are unsaved changes (`:bd!`).

```bash
# 6. Imagine you have multiple dungeon maps open in different tabs/buffers:
#    1: dungeon_level_1.map
#    2: goblin_barracks.map
#    3: treasury_vault.map
#    List your open maps (buffers/tabs). Then, practice the command to switch
#    directly to the 'treasury_vault.map'. Finally, go to the next map in the list.

# Practice: Type :ls<Enter>, then :b treas<Tab><Enter>, then :bn<Enter>
```

## Setting Vim Options (`:set`)

Command-Line Mode is also where you configure Vim's behavior using the `:set` command. Many of these settings have equivalents in VSCode's `settings.json` under the `"vim.*"` namespace, but you can often set them temporarily using `:set`.

- `:set {option}`: Enable a boolean option (e.g., `:set number`).
- `:set no{option}`: Disable a boolean option (e.g., `:set nonumber`).
- `:set {option}!`: Toggle a boolean option.
- `:set {option}={value}`: Set an option that takes a value (e.g., `:set tabstop=4`).
- `:set {option}?`: Show the current value of an option.

Some common useful options (check VSCode Vim docs for corresponding `settings.json` keys):

- `number` (`nu`): Show line numbers.
- `relativenumber` (`rnu`): Show relative line numbers (useful for vertical motion).
- `ignorecase` (`ic`): Ignore case in searches.
- `smartcase` (`sc`): Override `ignorecase` if your search pattern contains uppercase letters.
- `hlsearch` (`hls`): Highlight all search matches.
- `incsearch` (`is`): Show search matches incrementally as you type.
- `wrap`: Enable line wrapping. `nowrap`: Disable line wrapping.

```javascript
// 7. Let's temporarily tweak the editor settings for this session.
//    Turn on relative line numbers. Then, check the current value of the
//    'ignorecase' setting. Finally, disable search highlighting (`hlsearch`).

function configureMagicOrb() {
  const orbSettings = {
    crystalType: "Quartz",
    powerLevel: 9,
    focusTarget: null,
  };
  // Try searching for 'settings' before and after disabling hlsearch
  return orbSettings;
}

// Practice: Run :set relativenumber<Enter>, then :set ignorecase?<Enter>, then :set nohlsearch<Enter>
```

## Solutions

### Solution 1: Save Your Work

```typescript
:w<CR> (then type :q! but don't press Enter), then :x<CR>
```

### Solution 2: Run Shell Commands

```javascript
:!ls<CR> (or :!dir<CR>) j :r !date<CR>
```

### Solution 3: Replace First Occurrence

```javascript
:s/goblin/hobgoblin/<CR>
```

### Solution 4: Replace All Occurrences

```python
:%s/postion/potion/gic<CR> (Press y or n for each match)
```

### Solution 5: Replace Within Selection

```css
:'<,'>s/gold/brass/g<cr> ;
```

### Solution 6: Manage Buffers

```bash
:ls<CR> :b treas<TAB><CR> :bn<CR>
```

### Solution 7: Configure Vim Options

```javascript
:set relativenumber<CR> :set ignorecase?<CR> :set nohlsearch<CR>
```
