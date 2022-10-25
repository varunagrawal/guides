# Linux Stuff

### New Ubuntu System

- Run `sudo apt install build-essential cmake cmake-curses-gui git gcc g++` to install build tools.

### Image Modification

#### Compress

```sh
convert test.jpg -quality 50% test-50p.jpg
```

#### Resize

```sh
convert image.jpg -resize 600x400 image.jpg
```

```sh
convert -resize 50% myfigure.png myfigure.jpg
```

### Guide to Tmux

A great [read on how to use Tmux](http://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/) by Herman "Ham" Vocke.
