# Linux Stuff

## New Ubuntu System

### Basic Tools

Run `sudo apt install build-essential cmake cmake-curses-gui git gcc g++` to install build tools.

### Pyenv

**NOTE** Install `homebrew` after installing pyenv since for Ubuntu 20.04 and before, there is a `glibc` version mismatch.

- Install `pyenv` using the [installer](https://github.com/pyenv/pyenv-installer).
- Install Python and set the global version: `pyenv install 3.9.11 && pyenv global 3.9.11`
- Finally install useful packages:

  ```
  pip install -U pip numpy scipy ipython jupyter argcomplete`
  ```
- Run `ipython` once to set up its directories.

### Homebrew

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Dot Files

Go to `github.com/varunagrawal/dotfiles`, clone the repo and run `./install` to automagically set up all the dotfiles.

## Image Modification

### Compress

```sh
convert test.jpg -quality 50% test-50p.jpg
```

### Resize

```sh
convert image.jpg -resize 600x400 image.jpg
```

```sh
convert -resize 50% myfigure.png myfigure.jpg
```

## Guide to Tmux

A great [read on how to use Tmux](http://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/) by Herman "Ham" Vocke.
