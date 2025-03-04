# 代码浅读

vban-source.c中 调用 obs_source_output_audio()函数将接收到的音频数据交付给OBS。


---

# VBAN Audio Plugin for OBS Studio

## Introduction

This plugin provides audio source from and output to VBAN, an audio over UDP protocol.

## Properties for VBAN Audio Source

Streams will be identified by these two properties. If your computer is receiving multiple VBAN streams, please set them.

### Port

Set the listening port number.
The default is 6980.

> [!TIP]
> If you are running VoiceMeeter with VBAN, which uses the same port, you need to change the port number.
> On VoiceMeeter, right-click a label "Info" on Outgoing Streams table. You can configure port number for each outgoing stream.

### IP Address From

Set IP address or host name of your source.
If empty, any sources can be received from.

### Stream Name

Set name of your stream.
If empty, any stream will be received.

## Properties for VBAN Audio Output and Filter

### Port
Set the port number.
The default is 6980.

### IP Address To
Set IP address or host name of your destination.

### Stream Name
Set name of your stream.

### Track
Choose the track number in OBS Studio to be streamed.
This property is not available for filters.

### Sampling Rate
Choose the sampling rate to stream.
The default is same as OBS Studio so that no resample will happen.
If you choose different sampling rate, a resampler will convert the sampling rate.

### Format
Choose the format of each sample. Available options are 16-bit and 24-bit integers and 32-bit floating point.

## Build and install
### Linux
Use cmake to build on Linux. After checkout, run these commands.
```
sed -i 's;${CMAKE_INSTALL_FULL_LIBDIR};/usr/lib;' CMakeLists.txt
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=/usr/lib ..
make
sudo make install
```
You might need to adjust `CMAKE_INSTALL_LIBDIR` for your system.

### macOS
Build flow is similar to that for Linux.

## See also

- Tools supporting VBAN
  - For Windows
    - [VB-Audio VoiceMeeter Banana](https://vb-audio.com/Voicemeeter/banana.htm)
  - For macOS
    - [VBAN Receptor](https://apps.apple.com/us/app/vban-receptor/id1462414931)
    - [VBAN Talkie Cherry](https://apps.apple.com/us/app/vban-talkie-cherry/id1553486090)
  - For iOS
    - [VBAN Receptor](https://apps.apple.com/us/app/vban-receptor/id1094354001)
    - [VBAN Talkie](https://apps.apple.com/us/app/vban-talkie/id1541587241)
  - For Android
    - [VBAN Receptor](https://play.google.com/store/apps/details?id=vbaudio.vbanreceptor)
    - [VBAN Talkie](https://play.google.com/store/apps/details?id=com.vbaudio.vbantalkie)
  - For Linux
    - [vban](https://github.com/quiniouben/vban)
  - For developers
    - [Specification](https://vb-audio.com/Services/support.htm#VBAN)
- For glitch-free audio on OBS Studio
  - [Asynchronous Audio Filter](https://github.com/norihiro/obs-async-audio-filter) - If you hear a glitch, please consider using this plugin.
