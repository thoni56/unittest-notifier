# unittest-notifier - a somewhat portable notifier

## What It Is

`unittest-notifier` takes a command and runs it. Woot? Yes, but before
it starts it makes a notification on your screen/desktop using a
mechanism that it can find. And when the command is finished it makes
another notification with "Passed" or "Failed" depending on the return
code of the command.

The name might now make it clear that a typical command to run would be
to run your unittests. But of course you can give it any command.

In the future there might be options to change what is show in the
notifications, making it a bit more general.


## System Requirements

`unittest-notifier` is a shell script so it can run only on MacOS,
Linux, Cygwin and now "Bash on Windows".

To make it do its thing you need a notification mechanism in the form
of command line-capable program.


## The Story

The `unittest-notifier` was born in an attempt to create an environment
where unittests are run automatically as soon as you save a file.

There are a number of utilities that can watch a set of files or a part
of your file system for changes (`entr`, `ionotify`, `fswatch`, ...) which
all have different quirks.

But I could not find an even reasonably portable notification
mechanism. As I develop a few portable programs (notably
[`cgreen`](https://github.com/cgreen-devs/cgreen) and
[`alan`](http://www.alanif.se)) this was high on my wish-list.

Having already made a stab at a `monitor` command to monitor file
changes I felt the notification was a nice challenge.


## Supported Notification Mechanisms

### MacOS/Darwin

- terminal-notifier (<https://github.com/julienXX/terminal-notifier>)

### Linux

- notify-send (__sudo &lt;pkgmgr&gt; install notify-send__)

### Cygwin

On Cygwin we need a Windows program, but since Cygwin runs Windows
.exe:s just fine, you just need to make the command available in your
Cygwin shell, e.g. by putting it in a directory included in your PATH
or by adding the directory where they are located to your PATH.

- snoretoast - uses the native Windows 8/10 notification mechanism
(<https://github.com/KDE/snoretoast>)
- growlnotify - included with *Growl for Windows* (<http://www.growlforwindows.com/gfw/>)

### Bash on Windows

Since the Linux layer can't run Windows programs (yet, at least) the
only way that seems to work is to install `cbwin` from
https://github.com/xilun/cbwin, use `outbash.exe` instead of "Bash for
Windows" and then call `wrun` to excute one or the other notification
mechanisms that works for Cygwin.

This is work in progress.