# Splitting Windows: Multiply Your View

Working on complex code often requires looking at multiple files or different sections of the same file at once. Maybe you need to compare a function definition with its usage, consult documentation while writing code, or view a test file alongside the implementation. Vim's window splitting capabilities make this a breeze!

In Vim, you can divide your editor view into multiple independent windows (often called viewports or splits), each displaying a buffer.

> **VSCode Context:** In VSCode, Vim splits often correspond to VSCode's own split editor groups. The commands generally work as expected, manipulating these editor groups.

Let's learn how to slice and dice your view!

> Remember you can find the solutions by searching for /Solutions. To come back use `<CTRL-O>`.

## Creating Splits

There are two main ways to split your window:

- `:split` (or `:sp`): Creates a **horizontal** split. The current window is divided into two, one above the other. Both windows initially show the same file.
- `:vsplit` (or `:vs`): Creates a **vertical** split. The current window is divided into two, side-by-side. Both windows initially show the same file.

You can also combine splitting with opening a file:

- `:sp {filename}`: Opens `{filename}` in a new horizontal split.
- `:vs {filename}`: Opens `{filename}` in a new vertical split.

Alternatively, use these Normal mode commands (often quicker!):

- `Ctrl-W s`: Equivalent to `:sp`. (Think 's' for split).
- `Ctrl-W v`: Equivalent to `:vs`. (Think 'v' for vertical).
- `Ctrl-W n`: Equivalent to `:new`, which creates a new empty buffer in a horizontal split.

### Example 1: Viewing Multiple Files

```typescript
function fireball(target, powerLevel) {
  console.log(`Casting Fireball at ${target} with power ${powerLevel}!`);
  applyBurn(target);
  if (target.hasManaShield) {
    // interactWithManaShield(target.manaShield, powerLevel);
  }
}

function applyBurn(target) {
  // Burn logic...
}

// Practice: Type Ctrl-W s. Then (in the bottom window) type :e mana_shield.ts<Enter>.
// Then move back to the top window and type Ctrl-W v.
```

## Navigating Between Splits

Once you have multiple splits, you need to move between them. The primary way is using `Ctrl-W` followed by a direction key:

- `Ctrl-W h`: Move to the split to the left.
- `Ctrl-W j`: Move to the split below.
- `Ctrl-W k`: Move to the split above.
- `Ctrl-W l`: Move to the split to the right.
- `Ctrl-W w` (or `Ctrl-W Ctrl-W`): Cycle through the splits.

### Example 2: Navigating Splits

```javascript
// ==========================================
//        Scroll of Ancient Wisdom
//   Know thyself, know thy Vim commands.
// ==========================================
// ------------------------------------------
// potion_recipe.txt | map_fragment.txt
// (Bottom Left)     | (Bottom Right)
// ------------------------------------------

// Practice: Ctrl-W j (to potion), Ctrl-W l (to map), Ctrl-W k (to wisdom).
```

## Resizing Splits

Sometimes the default split sizes aren't ideal. You can resize them:

- `Ctrl-W +`: Increase height (horizontal split) or width (vertical split).
- `Ctrl-W -`: Decrease height (horizontal split) or width (vertical split).
- `Ctrl-W >`: Increase width (vertical split).
- `Ctrl-W <`: Decrease width (vertical split).
- `Ctrl-W =`: Equalize the size of all splits (very handy!).

You can also prefix these with a count (e.g., `5 Ctrl-W +` increases size by 5 lines/columns).

### Example 3: Resizing Splits

```css
/* .container {                         | <!DOCTYPE html>             */
/* width: 80%;                       | <html>                      */
/* Practice: (In left split) Type 10 Ctrl-W >. Then type Ctrl-W = */
```

## Closing Splits

Finished with a split? Close it easily:

- `:q` or `:close`: Close the current split (like closing a file). Fails on unsaved changes (`:q!`).
- `:only`: Close all other splits, leaving only the current one.
- `Ctrl-W c`: Equivalent to `:close`.
- `Ctrl-W q`: Equivalent to `:q`.
- `Ctrl-W o`: Equivalent to `:only`. (Think 'o' for only).

### Example 4: Closing Splits

```python
# import utils                            | import unittest
# def main():                             | class TestSuite(unittest.TestCase):
# Practice: Navigate to utils.py (Ctrl-W j). Type Ctrl-W c (or :q).
# Then navigate back to main_script.py (Ctrl-W k). Type Ctrl-W o (or :only).
```

## Solutions

### Solution 1: Viewing Multiple Files

```typescript
<Ctrl-W>s<Ctrl-W>j:e mana_shield.ts<CR><Ctrl-W>k<Ctrl-W>v
```

### Solution 2: Navigating Splits

```javascript
<Ctrl-W>j<Ctrl-W>l<Ctrl-W>k
```

### Solution 3: Resizing Splits

```css
10<Ctrl-W>><Ctrl-W>=
```

### Solution 4: Closing Splits

```python
<Ctrl-W>j<Ctrl-W>c<Ctrl-W>k<Ctrl-W>o
```
