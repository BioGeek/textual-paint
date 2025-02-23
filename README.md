
Textual Paint
=============

MS Paint in your terminal.

This is a TUI (Text User Interface) image editor, inspired by MS Paint, built with [Textual](https://textual.textualize.io/).

![MS Paint like interface](https://raw.githubusercontent.com/1j01/textual-paint/v0.1.0/screenshot.svg)

## Features

- [x] Open and save images
  - [x] Fancy file dialogs
  - [x] Drag and drop files to open
  - [x] Warnings when overwriting an existing file, or closing with unsaved changes
  - [x] Auto-saves a temporary `.ans~` backup file alongside the file you're editing, for crash recovery
  - [x] Edits ANSI art and raster images and more. See [File Formats](#file-formats)
- [x] All tools from MS Paint: Free-Form Select, Select, Eraser/Color Eraser, Fill With Color, Pick Color, Magnifier, Pencil, Brush, Airbrush, Text, Line, Curve, Rectangle, Polygon, Ellipse, and Rounded Rectangle
- [x] Color palette
- [x] Efficient screen updates and undo/redo history, by tracking regions affected by each action
- [x] You should be able to use this over SSH
- [x] Brush previews
- [x] Status bar
- [x] Menu bar
- [x] Keyboard shortcuts
- [x] Nearly every command from MS Paint is supported, including fun ones like:
  - [x] Flip/Rotate
  - [x] Stretch/Skew
  - [x] Edit Colors
  - [x] Set As Wallpaper (Tiled/Centered)
- [x] Localization into 26 languages: Arabic, Czech, Danish, German, Greek, English, Spanish, Finnish, French, Hebrew, Hungarian, Italian, Japanese, Korean, Dutch, Norwegian, Polish, Portuguese, Brazilian Portuguese, Russian, Slovak, Slovenian, Swedish, Turkish, Chinese, Simplified Chinese
- [x] Dark mode
- [x] Zooming works with text, despite running in the terminal :)

## Usage

Textual Paint requires a Python version between 3.10 and 3.12 to run.

See [Compatibility](#compatibility) for details on terminals supported.

Python 3.13 is not yet supported, so please use Python 3.12 for now.

### Installation

Use `pipx` to install globally, without installing dependencies globally:
```bash
pip install --upgrade pipx  # or in Arch Linux, sudo pacman -S python-pipx
pipx install textual-paint
```

Alternatively, you can install using `pip`:
```bash
pip install textual-paint
```

### Running

```bash
textual-paint
```

### Command Line Options

```
$ textual-paint --help
usage: textual-paint [options] [filename]

Paint in the terminal.

positional arguments:
  filename              Path to a file to open. File will be created if it
                        doesn't exist.

options:
  -h, --help            show this help message and exit
  --version             show program's version number and exit
  --theme {light,dark}  Theme to use, either "light" or "dark"
  --language {ar,cs,da,de,el,en,es,fi,fr,he,hu,it,ja,ko,nl,no,pl,pt,pt-br,ru,sk,sl,sv,tr,zh,zh-simplified}
                        Language to use
  --ascii-only-icons    Use only ASCII characters for tool icons, no emoji or
                        other Unicode symbols
  --ascii-only          Use only ASCII characters for the entire UI, for use in
                        older terminals. Implies --ascii-only-icons
  --backup-folder FOLDER
                        Folder to save backups to. By default a backup is saved
                        alongside the edited file.

development options:
  --inspect-layout      Enables DOM inspector (F12) and middle click highlight
  --clear-screen        Clear the screen before starting, to avoid seeing
                        outdated errors
  --restart-on-changes  Restart the app when the source code is changed
```

### Keyboard Shortcuts

- <kbd>Ctrl</kbd>+<kbd>D</kbd>: Toggle Dark Mode
- <kbd>Ctrl</kbd>+<kbd>Q</kbd>: Quit
- <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>S</kbd>: Save As **IF SHIFT IS DETECTED** — ⚠️ it might trigger Save instead, and overwrite the open file!
- <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Z</kbd>: Redo **IF SHIFT IS DETECTED** — ⚠️ it might trigger Undo instead.

The rest match MS Paint's keyboard shortcuts:

- <kbd>Ctrl</kbd>+<kbd>S</kbd>: Save
- <kbd>Ctrl</kbd>+<kbd>O</kbd>: Open
- <kbd>Ctrl</kbd>+<kbd>N</kbd>: New
- <kbd>Ctrl</kbd>+<kbd>T</kbd>: Toggle Tools Box
- <kbd>Ctrl</kbd>+<kbd>W</kbd>: Toggle Colors Box
- <kbd>Ctrl</kbd>+<kbd>Z</kbd>: Undo
- <kbd>Ctrl</kbd>+<kbd>Y</kbd>: Redo
- <kbd>F4</kbd>: Redo
- <kbd>Ctrl</kbd>+<kbd>A</kbd>: Select All
- <kbd>Delete</kbd>: Clear Selection
- <kbd>Ctrl</kbd>+<kbd>C</kbd>: Copy
- <kbd>Ctrl</kbd>+<kbd>V</kbd>: Paste
- <kbd>Ctrl</kbd>+<kbd>X</kbd>: Cut
- <kbd>Ctrl</kbd>+<kbd>E</kbd>: Image Attributes
- <kbd>Ctrl</kbd>+<kbd>PageUp</kbd>: Large Size
- <kbd>Ctrl</kbd>+<kbd>PageDown</kbd>: Normal Size

### File Formats

<!-- PyPI doesn't generate linkable headings -->
<a id="file-formats"></a>

Many file formats are supported, including ANSI art, raster images, SVG and HTML.

To choose a file format when saving, type its file extension. For example, to save a PNG, add `.png` to the end of the filename. The default is `.ans`.

| Format | Notes |
| --- | --- |
| **ANSI** (.ans) | Note that while it handles many more ANSI control codes when loading than those that it uses to save files, you may have limited success loading other ANSI files that you find on the web, or create with other tools. ANSI files can vary a lot and even encode animations! |
| **mIRC codes** (.irc, .mirc) | invented file extensions, and not to be confused with .mrc mIRC script files |
| **Plain Text** (.txt) | |
| **SVG** (.svg) | can open SVGs saved by Textual Paint, which embed ANSI data; can also open some other SVGs that consist of a grid of rectangles and text elements. For fun, as a challenge, I made it quite flexible; it can handle uneven grids of unsorted rectangles. But that's only used as a fallback, because it's not perfect. |
| **HTML** (.htm, html) | write-only (opening not supported) |
| **PNG** (.png) | opens first frame of an APNG file |
| **Bitmap** (.bmp) | |
| **GIF** (.gif) | opens first frame |
| **TIFF** (.tiff) | opens first frame |
| **WebP** (.webp) | opens first frame |
| **JPEG** (.jpg, .jpeg) | saving disabled because it's lossy (it would destroy your pixel art) |
| **Windows Icon** (.ico) | opens largest size in the file |
| **Mac OS Icon** (.icns) | opens largest size in the file; saving disabled because it requires specific sizes |
| **Windows Cursor** (.cur) | opens largest size in the file; saving not supported by Pillow (and it would need a defined hot spot) |

See [Pillow's documentation](https://pillow.readthedocs.io/en/stable/handbook/image-file-formats.html) for more supported formats.

Note that metadata is not preserved when opening and saving image files. This is however common for many image editors.

### Tips

You can draw with a character by clicking the selected color display area in the palette and then typing the character,
or by double clicking the same area to pick a character from a list.

You can set the text color by right clicking or holding <kbd>Ctrl</kbd> while clicking a color in the palette.
Also, if you double right click or hold <kbd>Ctrl</kbd> while double clicking on a color to open the Edit Colors dialog,
if will edit the text color when you click OK.

You can swap the foreground and background colors by right clicking or holding <kbd>Ctrl</kbd> while clicking the current colors area.
This is a great convenience, especially when using the Color Eraser tool, or when using custom colors that may be hard to distinguish.

You can display a saved ANSI file in the terminal with `cat`:

```bash
cat samples/ship.ans
```

To browse the sample art, run:

```bash
python -m src.textual_paint.gallery
```

To preview ANSI art files in file managers like Nautilus, Thunar, Nemo, or Caja, you can install the [ansi-art-thumbnailer](https://github.com/1j01/ansi-art-thumbnailer) program I made to go along with this project.


## Known Issues

### Editing
- Undo/Redo doesn't work inside the Text tool's textbox. <kbd>Ctrl</kbd>+<kbd>Z</kbd> will delete the textbox. (Also note that the Text tool works differently from MS Paint; it will overwrite characters and the cursor can move freely, which makes it better for ASCII art, but worse for prose.)
- Pressing both mouse buttons stops the current tool, but doesn't undo the current action. Also Pick Color can't be cancelled (with <kbd>Esc</kbd> or by pressing both mouse buttons), since it samples the color continuously.
- Airbrush is continuous in space instead of time. It should keep spraying while the mouse stays still.
- Large files can make the program very slow, as can magnifying the canvas. There is a 500 KB limit when opening files to prevent it from freezing.

### Visual
- The selection box border appears inside instead of outside (and lacks dashes). For the text box, I hid the border because it was too visually confusing, but it should also have an outer border.
- The canvas flickers when zooming in with the Magnifier tool.
- Some languages don't display correctly.
- The cursor can blink on the canvas while focus is on the character input. In fact you can have three blinking cursors at once if you open the command palette (via the icon in the top left corner) with a cursor on the canvas and focus on the character input.

### Menus
- Due to limitations of the terminal, shortcuts using <kbd>Shift</kbd> or <kbd>Alt</kbd> might not work. Menus are not keyboard navigable, because I can't detect <kbd>Alt</kbd>+<kbd>F</kbd>, etc.
- The status bar description can be left blank when selecting a menu item. (I think the `Leave` event can come after closing, once the mouse moves.)
- Menu items like Copy/Cut/Paste are not grayed out when inapplicable. Only unimplemented items are grayed out.
- Entering View Bitmap mode with <kbd>Ctrl</kbd>+<kbd>F</kbd> doesn't close any open menus.
- <kbd>Esc</kbd> doesn't close menus.

### File compatibility
- ANSI files (.ans) are treated as UTF-8 when saving and loading, rather than CP437 or Windows-1252 or any other encodings. Unicode is nice and modern terminals support it, but it's not the standard for ANSI files. There isn't really a standard for ANSI files.
- ANSI files are loaded with a white background. This may make sense as a default for text files, but ANSI files either draw a background or assume a black background, being designed for terminals.
- Edit > Paste From doesn't support image files, only ANSI art and plain text files. It should support all the same formats as Open.
- Error messages may not show up when opening a file fails. I'm not sure how to reproduce this, so if you run into this, do let me know.

### Edit Colors dialog
- Focus ring shows even while grid is not focused
- Can show two cells as selected, instead of one across both grids
- Custom colors order X/Y is different from MS Paint
- Pressing enter in color grid should select color and close
- Selection ring is hard to see in dark mode
- Focus ring is invisible on a black color cell
- When dragging on the color field or luminosity slider, the cursor can be seen to jump back to earlier places where the mouse was, before settling at the current position. (This may only be visible when the program is running slowly, such as while debugging. I haven't observed this on the canvas, so maybe it has something to do with the dialog being on a separate layer.)
- When opening the Edit Colors dialog, it may immediately close, if the mouse lines up with the "OK" or "Cancel" buttons. (This doesn't seem to currently happen, but I haven't knowingly fixed it. A git bisect turned up a bogus commit, possibly due to reproducing the behavior being unreliable. It also seems like it might depend on the specific layout of the dialog, which changed during development, and maybe even the terminal size.)

### Misc
- Extraneous undo states may be created in some cases. In particular, I noticed when undoing/redoing with free-typing mode, the last state had no cursor but was otherwise identical.
- Document recovery dialog is shown unnecessarily if the backup file is identical.
- Pressing a key to exit View Bitmap mode may cause unwanted side effects.
- Pressing a key doesn't exit View Bitmap mode if the character input is focused.

## Compatibility

<!-- PyPI doesn't generate linkable headings -->
<a id="compatibility"></a>

A Python version between 3.10 and 3.12 is required.

### Linux

Tested on Ubuntu 22, with GNOME Terminal, Kitty, XTerm, and VS Code's integrated terminal.

GNOME Terminal works best, with crisp triangles used for icons in dialogs, emoji support, and true color support.

Kitty works fine, supporting true color and emoji.

XTerm supports true color, but not emoji. Run with `COLORTERM=truecolor textual-paint --ascii-only` for XTerm compatibility.

### macOS

Tested on OSX 10.14 (Mojave), with iTerm2, and VS Code's integrated terminal.

In VS Code, Free-Form Select shows as tofu (a missing character symbol).

The default Terminal has missing characters, causing misalignment of everything to the right of them, plus borders are not rendered nicely, giving it a sort of *frayed fabric* look, and it's limited to 256 colors.

### Windows

Textual Paint works with the new [Windows Terminal](https://learn.microsoft.com/windows/terminal/install).

#### Pasting in Windows Terminal

[<kbd>Ctrl</kbd>+<kbd>V</kbd> does not work](https://github.com/microsoft/terminal/issues/11267) to paste by default, but **Edit > Paste** does work.
You can unbind <kbd>Ctrl</kbd>+<kbd>V</kbd> to fix this:
- Open Windows Terminal's Settings (<kbd>Ctrl</kbd>+<kbd>,</kbd>)
- Click "Open JSON file"
- Disable the paste binding by adding `//` to the beginning of the lines:
  ```json
  // {
  //     "command": "paste",
  //     "keys": "ctrl+v"
  // },
  ```
- Save the file, and the behavior should update immediately.

Alternatively, you can use the Actions tab of the Settings UI to remove the binding for <kbd>Ctrl</kbd>+<kbd>V</kbd>.

If you're wondering why *removing* the Paste binding fixes it, it's because Textual Paint needs to receive the literal <kbd>Ctrl</kbd>+<kbd>V</kbd> key presses in order to trigger its own Paste command.

#### Powershell Problems

Running in Powershell, you may run into a bug where the powershell prompt becomes active at the same time as the TUI.
Moving the mouse will redraw parts of the TUI, and it becomes hard to click on things, but still possible.
Commands can be entered, and the output will be interwoven with the TUI, including if you run a second instance of the program, in which case the two instances will vie for the screen.
If this happens, I would recommend first messing around with it, since it's a fun glitch, then opening a new tab in Windows Terminal with the **Command Prompt profile**, available in the new tab dropdown menu.

#### Windows Console

Textual Paint will **not** work properly with the old Windows console (`conhost.exe`), which lacks emoji/Unicode support and true color support.
This program is commonly thought of as the "Command Prompt", but the Command Prompt (`cmd.exe`) is actually a *shell* (like `bash`) that can run in either the old console or the new Windows Terminal, which are both *terminal emulators*.

You can run with `--ascii-only` to limit the characters used in the UI to ASCII, but colors will still be limited and similar colors will appear confusingly identical.

### VS Code

Note that VS Code's integrated terminal tries to fix the contrast of text, including in the canvas, which is entirely inappropriate for an ANSI art editor, as it obscures the colors, and can indeed *harm* the contrast of the resulting document, by tricking you into thinking there's more contrast than there actually is.

To disable this, you can add this to your settings.json:

```json
"terminal.integrated.minimumContrastRatio": 1
```

If this doesn't work, try increasing it to 1.1.


## Development

First, create a virtual environment, and activate it:
```bash
python -m venv .venv
# The activate script is in different places on different systems:
# Linux/macOS/WSL:
source .venv/bin/activate
# Windows (cmd.exe or PowerShell):
.venv\Scripts\activate
# Git Bash on Windows:
source .venv/Scripts/activate
```

Install Textual and other dependencies:
```bash
pip install -r requirements.txt
```

Run the app via Textual's CLI for live-reloading CSS support, and enable other development features:
```bash
textual run --dev "src.textual_paint.paint --clear-screen --inspect-layout --restart-on-changes"
```

Or run more basically:
```bash
python -m src.textual_paint.paint
```

Or install the CLI globally\*:
```bash
pip install --editable .
```

Then run:
```bash
textual-paint
```

\*If you use a virtual environment, it will only install within that environment.

`--clear-screen` is useful for development, because it's sometimes jarring or perplexing to see error messages that have actually been fixed, when exiting the program.

`--inspect-layout` enables a DOM inspector accessible with F12, which I built. It also lets you apply a rainbow highlight and labels to all ancestors under the mouse with middle click, but this is mostly obsolete/redundant with the DOM inspector now. The labels affect the layout, so you can also hold Ctrl to only colorize, and you can remember how the colors correspond to the labels, to build a mental model of the layout.

`--restart-on-changes` automatically restarts the program when any Python files change. This works by the program restarting itself directly. (Programs like `modd` or `nodemon` that run your program in a subprocess don't work well with a TUI's escape sequences.)

There are also launch tasks configured for VS Code, so you can run the program from the Run and Debug panel.
Note that it runs slower in VS Code's debugger.

To see logs, run [`textual console`](https://textual.textualize.io/guide/devtools/#console) and then run the program via `textual run --dev`.
This also makes it run slower.

Often it's useful to exclude events with `textual console -x EVENT`.

### Troubleshooting

> `Unable to import 'app' from module 'src.textual_paint.paint'`

- Make sure to activate the virtual environment, if you're using one.
- Make sure to run the program from the root directory of the repository.

> `ModuleNotFoundError: No module named 'src'`

- Make sure to run the program from the root directory of the repository.

> `pip install -r requirements.txt` fails with `KeyError: '__version__'` or other errors

- `KeyError: '__version__'` is due to an [incompatibility](https://github.com/python-pillow/Pillow/issues/8075) between Pillow 9.5.0 and Python 3.13. Please use Python 3.12 for now, until I can update Pillow and other dependencies for compatibility with the latest Python version.
- A VS Code launch configuration is included to debug the installation process.
  - This allows pausing on exceptions and setting breakpoints in pip source code and `setup.py` files.
  - If you want to set breakpoints in package source code, or test out modifications to a `setup.py` file, since packages are extracted to temporary folders, you need to pause early and find the newest temporary folder for the package.

### Quality Assurance

```bash
# Spell checking
# I use the VS Code extension "Code Spell Checker", and its associated CLI:
cspell-cli lint .

# Type checking
# I use the "Python" and "Pylance" VS Code extensions, and the Pyright CLI:
pyright
# I'm targeting zero errors at this version of Pyright:
PYRIGHT_PYTHON_FORCE_VERSION=1.1.345 pyright
# I also tried mypy and fixed some errors it reported, but I'm not targeting zero errors with mypy.
mypy src --no-namespace-packages --check-untyped-defs

# Visual Regression Testing (and a few other tests)
# I use pytest-textual-snapshot, which is a pytest plugin for comparing SVG screenshots of Textual apps over time.
pytest
# To accept differences, update the baseline with:
pytest --snapshot-update
# I also made a test recorder, which can generate test code, which is great for creating tests that interact with the canvas.
# Run with:
python tests/pilot_recorder.py
# Then interact with the app, and press Ctrl+C to stop recording.
# You can also hit Ctrl+R to replay what you have,
# or Ctrl+Z to remove the last step and replay the rest.
```

### Publishing

- Run QA steps above
- Update version numbers in `setup.cfg` and `src/textual_paint/__init__.py` to a pre-release version (e.g. `0.3.0-pre.1`)
- Add version header to `CHANGELOG.md` below "Unreleased", and update version links at bottom
- Commit (e.g. `git commit -m "Prepare v0.3.0"`)
- Build package: `python -m build --sdist --wheel`
- Upload to TestPyPI: (updating version numbers) `python -m twine upload --repository testpypi dist/textual_paint-0.3.0rc1-py3-none-any.whl dist/textual_paint-0.3.0rc1.tar.gz`
- Test installing from TestPyPI with: (outside the venv, updating the version number) `pipx uninstall textual-paint; pipx install textual-paint==0.3.0rc1 --pip-args "--index-url https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple textual-paint"`
- If all is good, update version numbers to remove `-pre.N` suffixes
- Amend commit (`git commit --amend --no-edit`)
- Rebuild: `python -m build --sdist --wheel`
- Upload to PyPI: `python -m twine upload dist/textual_paint-0.3.0-py3-none-any.whl dist/textual_paint-0.3.0.tar.gz`
- Push `main` branch (`git push origin main`)
- Tag and push tag (e.g. `git tag v0.3.0 && git push origin v0.3.0`)

## License

[MIT](https://github.com/1j01/textual-paint/blob/main/LICENSE.txt)

## News

For a history of changes to the project, see the [changelog](https://github.com/1j01/textual-paint/blob/main/CHANGELOG.md).

## Unicode Symbols and Emojis for Paint Tools

The first thing I did in this project was to collect possible characters to represent all the tool icons in MS Paint, to gauge how good of a recreation it would be possible to achieve, starting from looks.
As it turns out, I didn't run into any significant roadblocks, so I ended up recreating MS Paint. [Again.](https://jspaint.app)

These are the symbols I've found so far:

- Free-Form Select: ✂️📐🆓🕸✨☆⚝⛤⛥⛦⛧⚛🫥🇫/🇸◌⁛⁘ ⢼⠮ 📿➰➿𓍼യ🪢𓍯 𔗫 𓍲 𓍱 ౿ Ꮼ Ꮘ
- Select: ✂️⬚▧🔲 ⣏⣹ ⛶
- Eraser/Color Eraser: 🧼🧽🧹🚫👋🗑️▰▱
- Fill With Color: 🌊💦💧🩸🌈🎉🎊🪣🫗🚰⛽🍯 ꗃ﹆ ⬙﹅ 🪣﹅
- Pick Color: 🎨🌈💉💅💧🩸🎈📌📍🪛🪠🥍🩼🌡💄🎯𖡡⤤𝀃🝯⊸⚲𓋼🗡𓍊🍶🧪🍼🌂👁️‍🗨️🧿🍷⤵❣⚗ ⤆Ϸ ⟽þ ⇐ c⟾ /̥͚̥̥͚͚̊̊
- Magnifier: 🔍🔎👀🔬🔭🧐🕵️‍♂️🕵️‍♀️
- Pencil: ✏️✎✍️🖎🖊️🖋️✒️🖆📝🖍️🪶🪈🥖🥕▪
- Brush: 🖌👨‍🎨🧑‍🎨💅🧹🪮🪥🪒🪠ⵄ⑃ሐ⋔⋲ ▭⋹ 𝈸⋹ ⊏⋹ ⸦⋹ ⊂⋹ ▬▤
- Airbrush: ⛫💨дᖜ💨╔💨🧴🥤🧃🧯🧨🍾🥫💈🫠🌬️🗯☄💭༄༺☁️🌪️🌫🌀🚿 ⪧𖤘 ᗒᗣ дᖜᗕ
- Text: 📝📄📃📜AＡ🅰️🆎🔤🔠𝐴
- Line: 📏📉📈＼⟍𝈏╲⧹\⧵∖
- Curve: ↪️🪝🌙〰️◡◠~∼≈∽∿〜〰﹋﹏≈≋～⁓
- Rectangle: ▭▬▮▯➖🟥🟧🟨🟩🟦🟪🟫⬛⬜🔲🔳⏹️◼️◻️◾◽▪️▫️
- Polygon: ▙𝗟𝙇﹄』𓊋⬣⬟🔶🔷🔸🔹🔺🔻△▲☖⛉♦️🛑📐🪁✴️
- Ellipse: ⬭⭕🔴🟠🟡🟢🔵🟣🟤⚫⚪🔘🫧🕳️🥚💫💊🛞
- Rounded Rectangle: ▢⬜⬛𓋰⌨️⏺️💳📺🧫

The default symbols used may not be the best on your particular system, so I may add some kind of configuration for this in the future.

### Cursor

A crosshair cursor could use one of `+✜✛⊹✚╋╬⁘⁛𖥔⌖⯐`, but it might be better to show the pixel under the cursor, i.e. character cell, surrounded by dashes, like this:

```
 ╻
╺█╸
 ╹
```

## See Also

- [JavE](http://jave.de/), an advanced Java-based ASCII art editor
- [Playscii](http://vectorpoem.com/playscii/), a beautiful ASCII/ANSI art editor. This is also written in Python and MIT licensed, so I might take some code from it, for converting images to ANSI, for example. Who knows, maybe I could even try to support its file format.
- [cmdpxl](https://github.com/knosmos/cmdpxl), a pixel art editor for the terminal using the keyboard
- [pypixelart](https://github.com/douglascdev/pypixelart), a pixel art editor using vim-like keybindings, inspired by cmdpxl but not terminal-based
