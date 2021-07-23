# mpv handler

A protocol handler for mpv, written by Rust.

Please use with UserScript:

[![play-with-mpv-handler][play-with-mpv-badges]][play-with-mpv-greasyfork ]

## Install

### Linux

`mpv-handler.toml` should be stored at `~/.config/mpv/mpv-handler.toml`.

- Arch Linux
  - [mpv-handler][mpv-handler-download-aur] <sup>AUR</sup>
  - [mpv-handler-git][mpv-handler-download-aur-git] <sup>AUR</sup>
- GitHub Actions Build
  - [latest/mpv-handler-linux-x64.zip][mpv-handler-download-linux]

### Windows

`mpv-handler.toml` should be stored in the same directory with `mpv-hander.exe`.

**For Windows users, don't forget to edit the configuration file following the comments.**

- GitHub Actions Build
  - [latest/mpv-handler-windows-x64.zip](https://github.com/akiirui/mpv-handler/releases/latest/download/mpv-handler-windows-x64.zip)

[mpv-handler-download-aur]: https://aur.archlinux.org/packages/mpv-handler/
[mpv-handler-download-aur-git]: https://aur.archlinux.org/packages/mpv-handler-git/
[mpv-handler-download-linux]: https://github.com/akiirui/mpv-handler/releases/latest/download/mpv-handler-linux-x64.zip
[mpv-handler-download-windows]: https://github.com/akiirui/mpv-handler/releases/latest/download/mpv-handler-windows-x64.zip
[play-with-mpv-badges]: https://img.shields.io/badge/dynamic/json?style=for-the-badge&label=play-with-mpv&prefix=v&query=version&url=https%3A%2F%2Fgreasyfork.org%2Fscripts%2F416271.json
[play-with-mpv-greasyfork]: https://greasyfork.org/scripts/416271-play-with-mpv
[play-with-mpv-github]: https://github.com/akiirui/userscript/tree/main/play-with-mpv-handler

## Protocol URL

Base URL:

```
mpv://BASE64_ENCODE_VIDEO_URL/
```

Optional parameters:

```
cookies = [ www.domain.com.txt ]
downloader = [ mpv, ytdl, you-get, streamlink, and more...] (default: mpv)
quality = [ best, 4k, 2k, 1080p, 720p, 480p, 360p, and more... ]
```

Example:

```
mpv://aHR0cHM6Ly93d3cueW91dHViZS5jb20vd2F0Y2g/dj01cWFwNWFPNGk5QQ==/?cookies=www.youtube.com.txt&downloader=mpv&quality=best
```

## Customize Configuration

Generally, users only need to edit `player` and downloader `bin` to corresponding executable binary.

As of `v0.2.3`, default `mpv-handler.toml` configuration is like this:

```toml
### Player ###
# You should be change the value of "player" to your player executalbe binary path.
player = "/usr/bin/mpv"

### Video Downloader ###
# You should be change the value of "bin" to your downloader executable binary path.
[mpv]
bin = "/usr/bin/mpv"
cookies = "--ytdl-raw-options-append=cookies="
cookies_prefix = true
direct = true
quality.best = "--ytdl-format=bestvideo+bestaudio/best"
quality.360p = "--ytdl-format=bestvideo[height<=360]+bestaudio/best[height<=360]/best"
quality.480p = "--ytdl-format=bestvideo[height<=480]+bestaudio/best[height<=480]/best"
quality.720p = "--ytdl-format=bestvideo[height<=720]+bestaudio/best[height<=720]/best"
quality.1080p = "--ytdl-format=bestvideo[height<=1080]+bestaudio/best[height<=1080]/best"
quality.1440p = "--ytdl-format=bestvideo[height<=1440]+bestaudio/best[height<=1440]/best"
quality.2160p = "--ytdl-format=bestvideo[height<=2160]+bestaudio/best[height<=2160]/best"

[ytdl]
bin = "/usr/bin/youtube-dl"
cookies = "--cookies"
pipeline = true
options = ["--quiet", "--output", "-"]

[you-get]
bin = "/usr/bin/you-get"
cookies = "--cookies"
options = ["--player"]

[streamlink]
bin = "/usr/bin/streamlink"
options = ["--player"]

# For advanced user, you can add other downloader manually.
# Example:
#
# [example]
# bin = "/usr/bin/example"
# cookies = "--cookies"
# cookies_prefix = false
# direct = false
# pipeline = false
# options = ["--player"]
# quality.best = "--quality=best"
#
#
# [example]       Required, Type: String
#                     The value "example" is downloader table name
# bin             Required, Type: String
#                     The downloader executable binary path.
# cookies         Optional, Type: String (default: "")
#                     The downloader parameter of passthorgh cookies.
# cookies_prefix  Optional, Type: Boolen (default: false)
#                     Set as true to mark cookies parameter as prefix.
# direct          Optional, Type: Boolen (defalut: false)
#                     Set as true to mark downloader run directly without player.
# pipeline        Optional, Type: Boolen (default: false)
#                     Set as true to mark downloader transfer video data through pipeline.
# options         Optional, Type: Array of Strings (default: [])
#                     The parameters of downloader to set player or output.
# quality.LEVEL   Optional, Type: String
#                     The LEVEL is a key name
#                     The value is parameter of downloader to choose quality/format.
```
