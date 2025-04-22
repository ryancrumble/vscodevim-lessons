# Surrounding Things with Vim Surround

Manipulating surrounding characters like quotes, brackets, parentheses, and HTML tags is a frequent task in coding. Doing it manually often involves tedious cursor movements and keystrokes. Enter `vim-surround`, a fantastic Vim plugin (and built into VSCode Vim!) that makes these operations incredibly efficient.

> **VSCode Vim Setup:** The `vim-surround` functionality is included in the VSCode Vim extension but needs to be enabled. Ensure `"vim.surround": true` is present in your `settings.json`.

This lesson will guide you through the core features of `vim-surround`. Let's get surrounding!

> Remember you can find the solutions by searching for /Solutions. To come back use <CTRL-O>.

## Adding Surrounds (`ys`)

The basic command to add surrounds is `ys{motion}{char}`. `ys` stands for "you surround".

- `{motion}` is any Vim motion (like `iw` for inner word, `$` for to end of line, `ap` for around paragraph).
- `{char}` is the character you want to surround with (like `"`, `'`, `(`, `[`, `{`, `t` for tags). Note that some characters are aliases: `b` is `()`, `B` is `{}`.

Let's practice adding some basic surrounds.

```typescript
// 1. Our spell list needs proper formatting. Surround each spell name (the
//    word under the cursor) with double quotes `"`. Then, surround the entire
//    array contents (inside the square brackets) with parentheses `()`.

//  start here
//   /
//  /
// v
const basicSpells = [Fireball, IceShard, LightningBolt];

const advancedSpells = [GreaterHeal, Teleport, SummonImp];

function castSpell(spellName) {
  console.log("Casting: " + spellName);
}
```

Easy, right? You can combine ys with any motion you know.

Deleting Surrounds (ds)
To delete surrounding characters, use ds{char}. ds stands for "delete surrounding".

{char} is the character you want to delete (e.g., ", ', (, [, {, t for tags).
Let's clean up some text.

```JavaScript

// 2. Someone went overboard with the parentheses and quotes!
//    Remove the outer parentheses `()` around the function call.
//    Then, remove the single quotes `'` around the string 'Overly verbose message'.

//  start here
//   /
//  /
// v
function logMessage(message) {
  console.log(message);
}

(logMessage('Overly verbose message')); // Too many brackets!

const data = { 'key': '[value]' }; // Remove the [] around value later
```

ds is your quick escape from unwanted enclosures!

Changing Surrounds (cs)
Changing one set of surrounds for another is done with cs{old_char}{new_char}. cs stands for "change surrounding".

{old_char} is the existing surrounding character to target.
{new_char} is the new character you want to use.
Time for some refactoring!

```JavaScript

// 3. We've decided to switch our string quoting style and array notation.
//    Change the double quotes `"` around "Hello World" to single quotes `'`.
//    Change the square brackets `[]` around the numbers to curly braces `{}`.
//    Finally, change the parentheses `()` around the function arguments to
//    square brackets `[]`. (Maybe not wise, but good practice!)

//  start here
//   /
//  /
// v
const greeting = "Hello World";

const coordinates = [10, 20, 30];

function calculate(a, b) {
  return (a + b); // Change these ()
}
```

cs is incredibly useful for quick style changes or fixing mistakes.

Visual Mode Surrounding (S)
You can also add surrounds after making a visual selection (v, V, CTRL-V). Once the text is selected, just press S{char}.

```HTML

<body>
  <h1>Website Update</h1>
  <p>This is an important announcement regarding the site.</p>

  <ul>
    <li>Update 1</li>
    <li>Update 2</li>
  </ul>

  <footer>Contact us</footer>
</body>
```

Visual mode gives you precise control over what gets surrounded.

Tag Surrounding (t)
As seen above, surrounding with tags is common in HTML/XML. You can use:

ys{motion}t: This will prompt you to enter the tag (e.g., <div>).
S{tag} in Visual Mode (often easier, e.g., S<p>).
cst{new_tag}: Change surrounding tags (e.g., cst<div> to change <p> to <div>).
dst: Delete surrounding tags.

```HTML

<main>
  <div>
    <p>Just some content inside a paragraph.</p>
  </div>
</main>
```

Mastering tag surrounding is a huge time-saver for web development.

Fantastic! You've now learned the essentials of the powerful vim-surround plugin. Adding, deleting, changing, and visually surrounding text and tags should now feel much faster. Keep practicing these commands, and they'll become second nature!

Solutions

```TypeScript

// 1. Our spell list needs proper formatting. Surround each spell name (the
//    word under the cursor) with double quotes `"`. Then, surround the entire
//    array contents (inside the square brackets) with parentheses `()`.

//  start here
//   /
//  /
// v /Fire<ENTER>ysiw"jysiw"jysiw"gg/\[<ENTER>ysib
const basicSpells = [
  Fireball,
  IceShard,
  LightningBolt
];

const advancedSpells = [GreaterHeal, Teleport, SummonImp];

function castSpell(spellName) {
  console.log("Casting: " + spellName);
}
```

```JavaScript

// 2. Someone went overboard with the parentheses and quotes!
//    Remove the outer parentheses `()` around the function call.
//    Then, remove the single quotes `'` around the string 'Overly verbose message'.

//  start here
//   /
//  /
// v /logM<ENTER>ds(findDs'
function logMessage(message) {
  console.log(message);
}

(logMessage('Overly verbose message')); // Too many brackets!

const data = { 'key': '[value]' }; // Remove the [] around value later
```

```JavaScript

// 3. We've decided to switch our string quoting style and array notation.
//    Change the double quotes `"` around "Hello World" to single quotes `'`.
//    Change the square brackets `[]` around the numbers to curly braces `{}`.
//    Finally, change the parentheses `()` around the function arguments to
//    square brackets `[]`. (Maybe not wise, but good practice!)

//  start here
//   /
//  /
// v /Hello<ENTER>cs"'/\[<ENTER>cs]{/calc<ENTER>f(cs)[
const greeting = "Hello World";

const coordinates = [10, 20, 30];

function calculate(a, b) {
  return (a + b); // Change these ()
}
```

```HTML

<body>
  <h1>Website Update</h1>
  <p>This is an important announcement regarding the site.</p>

  <ul>
    <li>Update 1</li>
    <li>Update 2</li>
  </ul>

  <footer>Contact us</footer>
</body>
```

```HTML

<main>
  <div>
    <p>Just some content inside a paragraph.</p>
  </div>
</main>
```
