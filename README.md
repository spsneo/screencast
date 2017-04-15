screencast
==========

- [DESCRIPTION](#description)
- [USAGE](#usage)
- [OPTIONS](#options)
    - [```-o, --output-dir=DIR```](#-o---output-dirdir)
    - [```-t, --tmp-dir=DIR```](#-t---tmp-dirdir)
    - [```-u, --auto-filename```](#-u---auto-filename)
    - [```-p, --position=N,N```](#-p---positionnn)
    - [```-s, --size=NxN```](#-s---sizenxn)
    - [```-r, --fps=N```](#-r---fpsn)
    - [```-f, --format=TYPE```](#-f---formattype)
    - [```-i, --audio-input=NAME```](#-i---audio-inputname)
    - [```-a, --audio-encoder=NAME```](#-a---audio-encodername)
    - [```-v, --video-encoder=NAME```](#-v---video-encodername)
    - [```-e, --fade=TYPE```](#-e---fadetype)
    - [```-m, --volume-factor=N```](#-m---volume-factorn)
    - [```-w, --watermark=TEXT```](#-w---watermarktext)
    - [```-k, --wmark-position=N,N```](#-k---wmark-positionnn)
    - [```-z, --wmark-size=NxN```](#-z---wmark-sizenxn)
    - [```-c, --wmark-font=NAME```](#-c---wmark-fontname)
    - [```-x, --fixed=N```](#-x---fixedn)
    - [```-n, --no-notifications```](#-n---no-notifications)
    - [```-g, --png-optimizer=NAME```](#-g---png-optimizername)
    - [```-l, --list```](#-l---list)
    - [```-h, --help```](#-h---help)
    - [```--version```](#--version)
- [EXAMPLES](#examples)
- [INSTALLATION](#installation)
- [REQUIREMENTS](#requirements)
- [REMARKS](#remarks)
- [LINKS](#links)
- [AUTHOR](#author)
- [COPYRIGHT](#copyright)
- [LICENSE](#license)

------------------------------------------------------------------------

## DESCRIPTION
**screencast** is a command line interface to record a X11 desktop using FFmpeg. It’s designed to make desktop recording a simple task, eliminating the somewhat complex FFmpeg command line arguments and the need of multiple commands. It uses predefined encoder settings that should be suitable for most needs. The default settings provides a quick and affordable way to record the desktop, letting the user to be focused on just specifying the desired video position and size. If the user doesn’t want to stick with the default settings it is possible to choose among a set of supported encoders and container formats.

**screencast** not only provides an easy way to record your desktop, but it also has options to automatically add some effects to the recordings, like video fade-in / fade-out, text watermarking and volume increase.

## USAGE
```
$ screencast [options] output
$ screencast [options] -u
```

The specified output filename must have an extension which in turn must be a supported container format.

## OPTIONS
Long options can be used with spaces or an equal sign (’```=```’). For example, ```--fade in``` is the same as ```--fade=in```.

#### ```-o, --output-dir=DIR```

Set the output video to be saved in *DIR*. This is to be used with ```-u``` option (if you want to specify a save directory when using automatic output filename choosing). When not using ```-u``` option you can specify the output directory directly in the output filename.

default: the local directory

#### ```-t, --tmp-dir=DIR```

Set temporary files to be placed in *DIR*. By default, the ```/tmp``` directory will be used for temporary files, which usually is a ramdisk filesystem in most systems. You may want to change it if you have limited RAM and/or are recording very long videos. Make sure to have enough free space in the specified directory.

default: ```/tmp```

#### ```-u, --auto-filename```

Auto choose output filename based on date and time. The output filename will have the following format:

screencast-YEAR-MONTH-DAY\_HOUR.MINUTE.SECOND.FORMAT

#### ```-p, --position=N,N```

The screen position defining from where the recording will take place. These are X and Y offsets from the screen top left corner. Combined with ```-s``` option it will define a rectangular desktop area that will be recorded.

default: ```0,0``` (screen top left corner)

#### ```-s, --size=NxN```

The video size. This is actually the video resolution. Combined with ```-p``` option it will define a rectangular desktop area that will be recorded.

default: ```640x480```

#### ```-r, --fps=N```

Video framerate (frames per second - fps).

default: ```25```

#### ```-f, --format=TYPE```

Container format of the output video. This is to be used with ```-u``` option (if you want to specify a container format when using automatic output filename choosing). When not using ```-u``` option you can specify the container format directly in the output filename.

default: ```mp4```

supported types: ```mp4```, ```mkv```, ```webm```, ```ogg```

#### ```-i, --audio-input=NAME```

ALSA audio input device. When setted to ```none``` the audio will be disabled (video without audio, only video stream will be present). To determine possible audio input device names please see the
[FFmpeg ALSA capture guide](https://trac.ffmpeg.org/wiki/Capture/ALSA).

default: ```pulse```

#### ```-a, --audio-encoder=NAME```

Audio encoder to be used to encode the recorded audio. When setted to ```none``` the audio will be disabled (video without audio, only video stream will be present).

default: ```aac```

supported types: ```aac```, ```opus```, ```vorbis```, ```mp3```/```mp3lame```, ```shine```, ```none```

#### ```-v, --video-encoder=NAME```

Video encoder to be used to encode the recorded video. If using a NVIDIA hardware accelerated encoder please make sure that you have a NVIDIA graphics card that supports the choosed encoder.

default: ```x264```

supported types: ```x264```, ```h264_nvenc```, ```x265```, ```kvazaar```, ```hevc_nvenc```, ```theora```, ```vp8```, ```vp9```

#### ```-e, --fade=TYPE```

Video fade effect to be added to the recorded video. When setted to ```none``` the recorded video will have no fade effect.

default: ```none```

supported types: ```in```, ```out```, ```both```, ```none```

#### ```-m, --volume-factor=N```

Volume increase effect factor. This will increase the volume of the recorded audio. Normally, audio volume is low with default settings, even if you increse your microphone capture volume. Use this to give your videos a better hearing experience, letting your viewers fell more confortable to watch it whithout needing to rise their sound volume. It works as a percentage factor. For example, a value of ```1.5``` will increase volume by 50% and a value of ```2.0``` will double volume. When setted to ```1.0``` or ```0.0``` this effect is disabled.

default: ```1.0```

#### ```-w, --watermark=TEXT```

Enable text watermarking, setting text to *TEXT*. Although it is a text, it is generated as a PNG image so it can be integrated in the video.

default: disabled

#### ```-k, --wmark-position=N,N```

Set text watermark position inside the video. These are X and Y offsets from the video top left corner (not from the screen). Combined with ```-z``` option it will define a rectangular area in the video that will contain the text watermark image.

default: ```0,0``` (video top left corner)

#### ```-z, --wmark-size=NxN```

Set text watermark size. Combined with ```-k``` option it will define a rectangular area in the video that will contain the text watermark image.

default: ```255x35```

#### ```-c, --wmark-font=NAME```

Set text watermark font to *NAME*.

default: ```Arial```

note: if the default or setted font is not installed it will be auto choosed

#### ```-x, --fixed=N```

Set the video to have a fixed length of *N* seconds. When setted to ```0``` this is disabled, meaning a indefinite video length that will be  recorded until the user stops it by presing the **q** key in the terminal window.

default: ```0```

#### ```-n, --no-notifications```

Disable desktop notifications. Desktop notifications are shown by default, allowing a better visual control of the recording. Use this option to disable them.

#### ```-g, --png-optimizer=NAME```

Use PNG optimizer *NAME* and *advdef* (advancecomp) in the PNG image generated by ```-w``` option that will be used as a text watermark. This option is useful when you want to use a big text watermark in a big video, allowing the video to be a few bytes smaller. Not really needed if using default watermark settings with a small text. When setted to ```none``` PNG optimization is disabled.

default: ```none```

supported ones: ```truepng```, ```pingo```, ```optipng```, ```opt-png```, ```none```

#### ```-l, --list```

List arguments supported by these options.

#### ```-h, --help```

Help screen.

#### ```--version```

Show program version information.

## EXAMPLES
- Use all default settings:

    - ```$ screencast myvideo.mp4```

- Use default settings for a 1280x720 video from screen positon 200,234 with auto choosen output filename:

    - ```$ screencast -p 200,234 -s 1280x720 -u```

- Changing just the container format without specifying encoders will make it to auto choose them. In this case, the ```webm``` format will produce a video with opus and vp9 encoders:

    - ```$ screencast /home/user/webmvideos/myvideo.webm```

- Specifying save dir and container format, with auto choosen encoders and output filename. In this case, the ```ogg``` format will produce a video with vorbis (libvorbis) and theora encoders:

    - ```$ screencast -o /home/user/myvideos -f ogg -u```

- 1280x720 video from screen positon 200,234 , 30 fps, mp3 (libmp3lame) audio encoder, x265 video encoder, mkv container format, fade-in video effect, volume increase effect of 50%, small text watermark in top right video corner:

    - ```$ screencast -p 200,234 -s 1280x720 -r 30 -a mp3 -v x265 -e in -m 1.5 -w www.mysitehere.com myvideo.mkv```

**NOTE**:
When not using the ```-x``` option press the **q** key in terminal window to end the recording.

## INSTALLATION
Make the  **screencast** file executable and copy it to a directory that is in your *PATH*.

Copy the *screencast.1* man page file to your user commands man page directory, usually at ```/usr/share/man/man1```. For convenience, firstly compress the man page with *gzip*.

You can acomplish this by doing:

```
$ chmod +x screencast
$ sudo mv screencast /usr/local/bin
$ gzip -9 screencast.1
$ sudo mv screencast.1.gz /usr/share/man/man1
```

## REQUIREMENTS
- The minimum requirement is a recent *FFmpeg* version compiled with support for x11grab and the desired encoders. For example, if you want to use *vp9* video encoder and *opus* audio encoder it will require *FFmpeg* to be compiled with support for x11grab, libvpx and libopus. It’s advised to use *FFmpeg* version git master. You can see a *FFmpeg* compilation guide and a recommended *FFmpeg* Arch Linux AUR package at the [LINKS](#links) section.

- When recording audio (```-i``` and ```-a``` options not setted to ```none```) *FFmpeg* must have been compiled with support for ALSA audio. The default ```pulse``` setting for ```-i``` option requires *FFmpeg* to be compiled with support for pulseaudio (libpulse) as well.

- *notify-send* (libnotify) is needed for desktop notifications. Note that desktop notifications are enabled by default. They can be disabled by using the ```-n``` option, eliminating the need of *notify-send*. Running **screencast** in a system without *notify-send* and without using the ```-n``` option will result in error.

- Other requirements are needed according to additional options that may be specified by the user:

    - *FFprobe* and *bc* are needed for video fade effect (```-e``` option).

    - *ImageMagick* is needed for text watermarking (```-w``` option). Both IM6 and IM7 are supported, but IM7 is preferred.

    - At least one supported PNG optimizer and *advdef* (advancecomp) are needed for PNG (watermark) optimization (```-g``` option).

## REMARKS
- **screencast** uses a two step recording process. Firstly the audio and video are recorded to a lossless format and at a second stage it is encoded to produce the output video. That’s why you see a desktop notification saying ’*encoding...*’. This mechanism allows a better video and avoids problems.

- When using ```aac``` audio encoder (which is the default setting), **screencast** will check if the detected FFmpeg build has support for libfdk\_aac and use it if present, otherwise it will use the FFmpeg built-in AAC audio encoder. Make sure to have a recent FFmpeg version as older  versions do not support the built-in AAC audio encoder without being experimental, or do not support it at all.

- FFmpeg encoder names have the 'lib' prefix removed for simplicity. For example, libx264 is called ```x264``` in this program.

- Although the ```vorbis``` audio encoder is mentioned in the options, it is made this way just for simplicity as mentioned right above. When the user selects the ```vorbis``` audio encoder **screencast** uses the FFmpeg libvorbis encoder, which has a much superior quality than the FFmpeg built-in vorbis encoder.

- The ```mkv``` container format is the only one that supports all audio and video encoders. All other container formats have restrictions. **screencast** will exit with error if an unsupported encoder is choosed for a given container format. For example, you cannot use the ```opus``` audio encoder with ```mp4``` container format.

- When using the ```mp4``` container format, the moov atom will be automatically moved to the beginning of the output video file. This is the same as running *qt-faststart* in the output video and is useful for uploading it to streaming websites like [YouTube](https://www.youtube.com/).

- The default settings for container format and audio/video encoders will produce a video that is ready to be uploaded to [YouTube](https://www.youtube.com/).

- The default ```pulse``` audio input setting (```-i``` option) will be suitable for most users as it will use the default recording device configured in pulseaudio, as long as FFmpeg was compiled with ALSA and pulseaudio support.

- *Oxygen* icon names are used for displaying desktop notifications. Although not a requirement, *Oxygen* icons are recommended to be installed for a better visual integration.

- **screencast** will try to play a notification sound when the encoding process is finished. For this, it will use *paplay* (from *pulseaudio*) and a sound file from the freedesktop sound theme (usually a package called *sound-theme-freedesktop* in most Linux distributions). Although not a requirement, they are recommended to be installed for a better user experience.

## LINKS
- FFmpeg: [https://www.ffmpeg.org/](https://www.ffmpeg.org/)

- FFmpeg compilation guide: [https://trac.ffmpeg.org/wiki/CompilationGuide](https://trac.ffmpeg.org/wiki/CompilationGuide)

- **screencast** Arch Linux AUR package: [https://aur.archlinux.org/packages/screencast/](https://aur.archlinux.org/packages/screencast/)

- FFmpeg version git master Arch Linux AUR package (with all possible libs including libfdk_aac): [https://aur.archlinux.org/packages/ffmpeg-full-git/](https://aur.archlinux.org/packages/ffmpeg-full-git/)

## AUTHOR
Daniel Bermond

[https://github.com/bermond/screencast](https://github.com/bermond/screencast)

## COPYRIGHT
Copyright © 2015-2017 Daniel Bermond

## LICENSE
GNU General Public License version 2 (GPL2).

For details see the file COPYING or visit:
[http://www.gnu.org/licenses/gpl-2.0.html](http://www.gnu.org/licenses/gpl-2.0.html)

------------------------------------------------------------------------