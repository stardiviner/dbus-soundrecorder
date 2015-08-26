# dbus-soundrecorder
Records sound from Pulse Audio using ffmpeg.

Uses D-Bus to determine current song, album, artist and other meta data
provided by the media player application via MPRIS D-Bus service.

When the next song start, the recorder automatically starts a new file
and sets available meta data.

## Usage
```
dbus-soundrecorder record [options]
```

Here's a simple example:

First, get a list of your Pulse Audio sinks:
```
pactl list short sinks
```

You can also create a new virtual Pulse Audio sink:
```
pactl load-module module-null-sink sink_name=virtual1
```
In any case, you should ensure that the media player uses the sink (eg. using pavucontrol).

Then start the recorder. You need to specify the media player application and the sink:
```
dbus-soundrecorder -a vlc -s virtual1.monitor -o "-c:a libfdk_aac -vbr 4 -ar 44100"
```
As you can see, it is also possible to specify options for ffmpeg. However input sink,
output file and meta data are provided by the recorder and shouldn't be specified.

For all available options, use the --help command.

## Build instructions
The application depends on the c++utilities library. It is built in the same way as c++utilities.

The following Qt 5 modules are requried: core dbus


