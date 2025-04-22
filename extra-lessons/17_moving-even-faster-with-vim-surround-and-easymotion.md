# Moving Even Faster with Vim-Sneak

You've mastered basic motions (`hjkl`, `w`, `b`, `e`), jumping with `f`/`t`, and searching with `/`. But what if you want to jump _directly_ to a spot defined by two specific characters, even if it's far away on the line or screen? Enter **Vim-Sneak**.

Vim-Sneak (and similar plugins/features) allows you to type a trigger command followed by two characters. It then highlights all occurrences of that two-character sequence visible on the screen and lets you jump directly to the one you want.

> **VSCode Context:** The VSCode Vim extension includes the Sneak functionality! You need to enable it in your `settings.json`:
> `"vim.sneak": true`
> By default, the trigger keys are `s` (forward sneak) and `S` (backward sneak). Some users remap these if they conflict with other desired mappings (like surround). For this lesson, we'll assume the default `s` and `S` triggers are active.

Let's learn how to leap across your code!

> Remember you can find the solutions by searching for /Solutions. To come back use <CTRL-O>.

## Sneaking Forward (`s`) and Backward (`S`)

The core idea is simple:

1.  Press `s` (to sneak forward) or `S` (to sneak backward) from Normal mode.
2.  Type the **two** characters you want to jump to.
3.  Vim highlights all occurrences of these two characters ahead of (for `s`) or behind (for `S`) the cursor. Each match gets a label (like `a`, `b`, `c`...).
4.  Type the label character corresponding to your desired destination.

If there's only one match, Vim jumps immediately without needing a label. If there are multiple matches after the first, you can press `;` to jump to the next match or `,` to jump to the previous one (similar to how `f`/`t` work).

Let's practice sneaking.

````javascript
// 1. You are editing a configuration object. Your cursor is at the beginning
//    of the file. Jump directly *forward* to the 'tr' in 'trackerUrl'.
//    Then, from that position, jump *backward* to the 'na' in 'analyticsEnabled'.

//  start here
//   /
//  /
// v
const configurationSettings = {
  apiKey: "xyz789-abc123-def456",
  analyticsEnabled: true, // Jump backward to 'na' from 'trackerUrl'
  featureFlags: ["newDashboard", "betaReporting"],
  serverAddress: "[https://api.example.com/v2](https://api.example.com/v2)",
  trackerUrl: "[https://tracker.example.com](https://tracker.example.com)", // Jump forward to 'tr'
  retryAttempts: 3,
};

function applyConfiguration(settings) {
  if (settings.analyticsEnabled) {
    initializeAnalytics(settings.trackerUrl);
  }
  console.log("Configuration applied.");
}
Sneak is incredibly efficient for precise jumps, especially when f/t would require too many ; presses or when / feels too heavy for a quick jump.Sneaking Across LinesSneak isn't limited to the current line! It searches across the visible portion of the screen.# 2. Your cursor is on the `import` statement. You need to jump directly to
#    the 'el' in the word 'else' within the `process_data` function several
#    lines below. Then, from 'else', jump backward to the 'rt' in 'important'.

#  start here
#   /
#  /
# v
import os
import sys

class DataProcessor:
  def __init__(self, source_file):
    self.source = source_file
    self.data = None

  def load_data(self):
    # This is an important loading step
    print(f"Loading from {self.source}") # Jump backward to 'rt' from 'else'
    # ... file reading logic ...
    self.data = [1, 5, 3, 8, 2]

  def process_data(self):
    if not self.data:
      print("No data loaded.")
      return None
    if len(self.data) > 5:
      # Complex processing for larger datasets
      processed = sorted(self.data, reverse=True)
    else: # Jump forward to 'el'
      # Simpler processing
      processed = sorted(self.data)
    return processed

# Entry point
if __name__ == "__main__":
  processor = DataProcessor("data.txt")
  processor.load_data()
  results = processor.process_data()
  print(f"Results: {results}")

Being able to jump across lines directly to a two-character target saves a lot of vertical navigation (j/k) or searching (/).What About EasyMotion?You might also hear about Vim-EasyMotion. EasyMotion works slightly differently: you typically press a leader key combination (e.g., <Leader><Leader>w to jump to the start of words), and it overlays unique markers (like letters) on all potential jump targets across the screen. You then type the single marker character to jump instantly.While incredibly powerful, EasyMotion isn't built into VSCode Vim by default like Sneak is. You would typically need to install a separate VSCode extension (like "VSCode Vim EasyMotion" or similar ones that might exist) to get this functionality.Sneak provides a similar benefit of targeted screen jumps with its two-character approach and is readily available once enabled in VSCode Vim settings.Mastering Sneak (s, S) gives you a powerful, precise way to navigate your code, complementing your existing movement commands and significantly reducing wasted keystrokes. Practice identifying unique two-character sequences near your target destination!Solutions// 1. You are editing a configuration object. Your cursor is at the beginning
//    of the file. Jump directly *forward* to the 'tr' in 'trackerUrl'.
//    Then, from that position, jump *backward* to the 'na' in 'analyticsEnabled'.

//  start here
//   /
//  /
// v strSna (Assuming only one 'tr' and 'na' match, otherwise add label char)
const configurationSettings = {
  apiKey: "xyz789-abc123-def456",
  analyticsEnabled: true, // Jump backward to 'na' from 'trackerUrl'
  featureFlags: ["newDashboard", "betaReporting"],
  serverAddress: "[https://api.example.com/v2](https://api.example.com/v2)",
  trackerUrl: "[https://tracker.example.com](https://tracker.example.com)", // Jump forward to 'tr'
  retryAttempts: 3,
};

function applyConfiguration(settings) {
  if (settings.analyticsEnabled) {
    initializeAnalytics(settings.trackerUrl);
  }
  console.log("Configuration applied.");
}
```python
# 2. Your cursor is on the `import` statement. You need to jump directly to
#    the 'el' in the word 'else' within the `process_data` function several
#    lines below. Then, from 'else', jump backward to the 'rt' in 'important'.

#  start here
#   /
#  /
# v selSrt (Assuming only one 'el' and 'rt' match, otherwise add label char)
import os
import sys

class DataProcessor:
  def __init__(self, source_file):
    self.source = source_file
    self.data = None

  def load_data(self):
    # This is an important loading step
    print(f"Loading from {self.source}") # Jump backward to 'rt' from 'else'
    # ... file reading logic ...
    self.data = [1, 5, 3, 8, 2]

  def process_data(self):
    if not self.data:
      print("No data loaded.")
      return None
    if len(self.data) > 5:
      # Complex processing for larger datasets
      processed = sorted(self.data, reverse=True)
    else: # Jump forward to 'el'
      # Simpler processing
      processed = sorted(self.data)
    return processed

# Entry point
if __name__ == "__main__":
  processor = DataProcessor("data.txt")
  processor.load_data()
  results = processor.process_data()
  print(f"Results: {results}")
````
