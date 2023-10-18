# mavid

## OVERVIEW

`mavid` (Make Video) is utility to record screencasts of your X11 desktop using ffmpeg, inspired by [`maim`](https://github.com/naelstrof/maim).

By default, it records lossless video & audio using the [libx264rgb](https://ffmpeg.org/ffmpeg-codecs.html#libx264_002c-libx264rgb) & [flac](https://ffmpeg.org/ffmpeg-codecs.html#flac-2) encoders, respectively, into a single [Matroska](https://www.matroska.org/) (`.mkv`) container file. The lossless MKV recording can then be transcoded into smaller, lossy formats in different container formats. This generally reduces CPU load while recording, which is helpful on slower processors, but produces significantly larger recording files.

**NOTE:** It currently only supports [OpenBSD](https://www.openbsd.org/) due to its reliance on [sndio](https://sndio.org/) and especially OpenBSD's [`sndioctl`](http://man.openbsd.org/sndioctl).

## PREREQUISITES

* [OpenBSD](https://www.openbsd.org/)
* [`sndio`](https://sndio.org/)
* [`ffmpeg`](https://ffmpeg.org/)
* [`slop`](https://github.com/naelstrof/slop)

## USAGE

1. Install the OpenBSSD `ffmpeg` and `slop` packages:

```
pkg_add ffmpeg slop
```

2. Enable OpenBSD audio recording, if you haven't already:

```
sysctl kern.audio.record=1
```

2. Record your entire display:

```
mavid <file>
```

Alternatively, you can select a portion of your display to record prior to starting recording by executing `mavid -s`:

```
mavid -s <file>
```

3. Press `Ctrl-C` to cancel recording. (Pressing `q`, which normally also stops `ffmpeg` recording because of the way video & audio are being piped.)

## Reference

* [FFMPEG Capture/Desktop (Lossless Recording)](https://trac.ffmpeg.org/wiki/Capture/Desktop#LosslessRecording)
* [`fauxstream`](https://github.com/rfht/fauxstream) (example of piping `x11grab` video & `sndio` audio into a single file with `ffmpeg`)
* My old [x11record](https://github.com/morgant/x11record) utility

## LICENSE

Released under the [MIT License](LICENSE).
