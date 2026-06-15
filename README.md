<div align="center">
<h1><code>snake</code></h1>
<p>A super minimal TUI, classic snake implementation written in pure BASH v5.1+</p>
<img src="https://shields.io/badge/made-with%20%20bash-green?style=flat-square&color=d5c4a1&labelColor=1d2021&logo=gnu-bash">
<img src=https://img.shields.io/badge/Maintained%3F-yes-green.svg></img>  
<a href="https://discord.gg/W4mQqNnfSq">
<img src="https://discordapp.com/api/guilds/913584348937207839/widget.png?style=shield"/></a>
<img src="./snake.gif">
</div>

## Install
stream `snake` without downloading/installing
```bash
bash <(curl -s https://raw.githubusercontent.com/wick3dr0se/snake/main/snake)
```

otherwise, download
```bash
git clone https://github.com/wick3dr0se/snake; cd snake
```

install to $PATH (optional)
```bash
cp snake /usr/local/bin
```

## Usage
if installed to $PATH `snake`, otherwise `./snake` or `bash snake`

## Interface Controls
arrow keys, or:  
`H`, `A` - move left  
`J`, `S` - move down   
`K`, `W` - move up  
`L`, `D` - move right

`Q` - quit
any other key pauses

## Compatibility & Verifying Input
Controls are read one keypress at a time. Letter keys (`WASD`, `HJKL`, `Q`) are single bytes and are case-insensitive. Arrow keys arrive as an escape sequence — `ESC` followed by 2 bytes — recognized as `\e[A` `\e[B` `\e[C` `\e[D` (up/down/left/right) in the terminal's *normal* cursor-key mode.

Note: in *application* cursor-key mode (DECCKM) arrows are sent as `\eOA`–`\eOD` instead of `\e[A`–`\e[D`, so they are not recognized — the letter keys still work. `snake` never enables application mode itself, but a wrapper (tmux, an ssh remote) might. Modified arrow sequences (e.g. `\e[1;5A`) are likewise not parsed.

Verify what your terminal sends:
```bash
cat -v   # press each arrow, then Ctrl-C
```
Expect `^[[A ^[[B ^[[C ^[[D`. If you instead see `^[OA…`, use `WASD`/`HJKL`, or leave application mode with `tput rmkx`.

Requires Bash ≥ 5.1 (`SRANDOM`, `${var^^}`). Worth checking in each terminal you target — xterm, GNOME Terminal, Apple Terminal, iTerm2, kitty, alacritty — plus inside tmux and over ssh.
