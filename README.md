EC - Echo Canceller
===================

The `ec` is an Acoustic Echo Cancellation (AEC) deamon.
It is a part of [voice-engine project](https://github.com/voice-engine).
The goal is to make an open source smart speaker for daily use.

It will read audio data from a named pipe and play it.
Meanwhile it will record audio and remove the playing audio from the recording,
and then output it to another named pipe.

It uses ALSA API to read and write audio, uses SpeexDSP's AEC algorithm.

### Build
```
sudo apt-get -y install libasound2-dev libspeexdsp-dev
git clone https://github.com/voice-engine/ec.git
cd ec
make
```

### Configuration
+ ALSA, use [File plugin](https://www.alsa-project.org/alsa-doc/alsa-lib/pcm_plugins.html)

+ PulseAudio, use [module-pipe-sink](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/#index1h3) and [module-pipe-source](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/#index2h3)

### Usage
1. Run `./ec -h` to show its command line options
2. Run `arecord -L` and `aplay -L` to get audio devices' name
3. Select audio input/output devices `./ec -i {input device name} -o {output device name} -c {input channels}`

```
./ec -h
./ec -i plughw:1 -o plughw:1 -s
```

### Hardware
+ ReSpeaker 2 Mic Hat for Raspberry Pi

  The delay between playback and recording is about 200. `./ec -i plughw:1 -o plughw:1 -d 200`

### License
GPL V3

### Credits
+ The ring buffer implementation is from PortAudio
+ [SpeexDSP](https://github.com/xiph/speexdsp) provides the excellent open source AEC algorithm
+ Using named pipe for I/O is inspired by [snapcast](https://github.com/badaix/snapcast)
