fzf-launcher-pass
=================

An interactive prompt that allows the user to pick a [password store
(pass)][pass] secret, and types it out using [ydotool][ydotool]. In addition to
conventional secrets, the prompt also supports one-time passwords (OTPs),
frequently used in two-factor authentication (2FA).


## What is this?

[pass][pass] is a minimalistic password manager, which became known thanks to
its incredible versatility and abundance of extension points.

One tool which makes _pass_ extremely convenient for everyday use in X11 is
[passmenu-otp][passmenu-otp] -- a shell script, which utilizes _dmenu_ to offer
user interactive list of available secrets. Having selected a specific one, user
can copy it to clipboard temporarily, or use _xdotool_ to input it into focused
text area directly. An extension of [passmenu][passmenu], _passmenu-otp_ adds
support for one-time passwords (OTPs) managed with [pass-otp][pass-otp].

Transitioning away form X11, I have discovered that _passmenu-otp_ is
incompatible with Wayland in various ways. This gave rise to
_fzf-launcher-pass_, which can be viewed as its Wayland-savvy successor:

 - Instead of _dmenu_ that was X11-only at the time of writing, this script
   uses [fzf][fzf] -- a Wayland-compatible command-line fuzzy finder that can be
   readily used to generate all sorts of convenient UI prompts.

 - Instead of _xdotool_, this script uses [ydotool][ydotool] -- a
   Wayland-compatible UI automation tool that serves the same purpose.

 - Just like [passmenu-otp][passmenu-otp], this script retains support for
   secrets that are OTPs managed with [pass-otp][pass-otp].

**TL;DR**: this project is [passmenu-otp][passmenu-otp] but for Wayland.


## How to use it?

_fzf-launcher-pass_ works the same way as _passmenu-otp_:

  1. Run it (from shell or using keybinding).
  2. Pick a password in fzf.
  3. The password gets typed out into the currently focused field.

If you use multiple tools that call ydotool, you may want to synchronize their
operation by running the `ydotoold` daemon in the background at all times.


## More goodies

 - The script looks for a `~/.passmenu_ignore` file, which can contain wildcard
   patterns (just like .gitignore) that exclude secrets from the presented list.
   This is useful in cases where other programs automatically populate your
   password store with long garbled secret names that unnecessarily obstruct
   your prompt.

 - The script maintains a history file in your XDG cache directory (by default
   `~/.cache`), which contains the names of recently used secrets, so that fzf
   can sort them for you.

Paths to all these files can be changed in the "Configuration" section of the
script.


## Security considerations

Disclaimer: This script runs the contents of your secret through `tr` and
`grep`. If you don't trust your environment, it won't be safe to use!


## Copyright

This project was created in the Winter of 2020/2021 by Petr Mánek, and is
licensed under the MIT license. For copyright of the original works, check out
[passmenu-otp][passmenu-otp] and [passmenu][passmenu].


[pass]: https://github.com/peff/pass
[fzf]: https://github.com/junegunn/fzf
[passmenu]: https://github.com/cdown/passmenu
[passmenu-otp]: https://github.com/petrmanek/passmenu-otp
[pass-otp]: https://github.com/tadfisher/pass-otp
[ydotool]: https://github.com/ReimuNotMoe/ydotool


