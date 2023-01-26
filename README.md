# Gengir: Genuine* autocompletion for your PyGObject code!

This tool initially started as a fork of [fakegir](https://github.com/strycore/fakegir) but now it has been rewritten entirely.

Gengir is a tool to create type definitions for PyGObject. It uses modern python standards and it's easy to use 

## Features

- Supports [PEP 484](https://www.python.org/dev/peps/pep-0484/) type annotations
- Installs typings as a [PEP 561](https://www.python.org/dev/peps/pep-0561/) stub in the correct site-packages, even for venv!
  It creates a package named `gi-stubs`. Once it's installed, it should be recognized by your IDE and it should provide autocompletion and typing errors.
- Uses Sphinx markup on docstrings
- ~~A GTK version switch~~
  _It's now chosen automatically based on the module dependencies!_
- ~~Multithreading!~~
  _Not anymore!_ (but it's fast still)

## TODO

- Complete [`overrides.rs`](src/overrides.rs)
- Typings for `.connect` signal names and callbacks

## Building & Installing

To build this project, you need to have installed the Rust toolchain, version 1.56.0 or newer.

`git clone` this repository, and run `cargo build --release`.

You can run the program once using `cargo run --release`, but if you use separate `venv`s for your projects, I'd recommend installing it user wide with `cargo install --path .`


## Usage

The `*.gir` with the type info files should be included with each GNOME library development package in `/usr/share/gir-1.0/`.

If you wanted to install stubs for libadwaita, run `gengir Adw-1`. If you're using a venv you'll need to run gengir inside the venv. With poetry for example just run `poetry run gengir Module-x`.

### Install Rust
`curl https://sh.rustup.rs -sSf | sh`

### Clone official repo
`git clone https://github.com/santiagocezar/gengir.git`

### Build the cloned repo
`cargo build --release`

### If you get error: File or directory not found
If you are using this repo then you need python3 executable or if from official repo then python executable. You probably don't have python installed or you have python3 only, not python. Gengir tries to run `python -c "xxx"` so either change your python3 name to python or install python so that Gengir can find the `python` executable.

### Start installation of various `code completions` code
```./gengir Gtk-3.0
./gengir Gdk-3.0
./gengir Gio-2.0
./gengir GiRepository-2.0
./gengir GIRepository-2.0
./gengir GL-1.0
./gengir GLib-2.0
./gengir GModule-2.0
./gengir GObject-2.0
./gengir WebKit2-4.0
./gengir WebKit2WebExtension-4.0
```

### The below packages might be required
Python3 venv: `sudo apt install python3.8-venv`

Poetry: `curl -sSL https://install.python-poetry.org | python3 -`

### If you want to check what other packages can be installed
Go to directory `/usr/share/gir-1.0/`

### Already have Gengir binary and *.git files? Do:
`mv ./target/release/gir-1.0 /usr/share/`

### Uninstalling rust can be done by
```rustup self uninstall
sudo apt remove cargo
sudo apt autoremove
```

### Uninstalling poetry can be done by
```
curl -sSL https://install.python-poetry.org | python3 - --uninstall
curl -sSL https://install.python-poetry.org | POETRY_UNINSTALL=1 python3 -
```

### Below is the output of one of the commands running: `./gengir WebKit2WebExtension-4.0`
```creating gi-stubs tree in ~/.local/lib/python3.8/site-packages/gi-stubs
WebKit2WebExtension v4.0
| Gtk v3.0
| | Atk v1.0
| | | GObject v2.0
| | | | GLib v2.0
| | Gdk v3.0
| | | GdkPixbuf v2.0
| | | | GModule v2.0
| | | | Gio v2.0
| | | Pango v1.0
| | | | cairo v1.0
| | xlib v2.0
| JavaScriptCore v4.0
| Soup v2.4
```

## Editor support

-   VSCode has support for stub packages out of the box.
-   [Jedi](https://github.com/davidhalter/jedi) supports it too, so any editor using it should work.

<sup>*not completely genuine, but it's getting there</sup>
