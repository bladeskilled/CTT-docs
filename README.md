# CTT docs (WIP & unofficial)
## Join CTT @ https://discord.gg/CTT

## Section 1: OBS
What's OBS?

Open Broadcaster Software,  is a program you can use to record and stream applications. 
These threads will teach you how to configure OBS for all your needs.

Install OBS using OBS-Studio-Full-Installer-x64.exe:
https://github.com/obsproject/obs-studio/releases/latest

There is no reason to use OBS 25.0.8 anymore, (there used to be claims newer versions caused frames halving when recording at a High FPS) - s/o Tellinq 

Automated settings script

This script can optimize (or make a new) OBS profile with all the relevant settings for high FPS recording tuned, with settings for all PCs:

0. Open PowerShell

1. Import TweakList by copying and pasting in this command, then pressing enter:
powershell -noe "iex(irm tl.ctt.cx)"

2. Run the Optimize-OBS function, example:
Optimize-OBS -Preset HighPerformance -Encoder NVENC

Change NVENC to AMF if you have an AMD GPU.

## Section 2: blur
blur is a free, faster and open source alternative to frame blending/resampling  and FFmpeg's T-mix.

Installing blur:
blur can be installed manually thru this URL: https://github.com/f0e/blur/releases/latest/download/blur-installer.exe 

Features:
Resample
You can render your videos, just like T-mix or like if you opened Vegas, dropped a clip and rendered it to 60FPS, except that it's much faster, especially when resampling high FPS (240+)

Interpolation:
There's also the possibility of interpolating your videos with SVPFlow (which is uncomparably faster than Flowframes RIFE). It's only downside is that the frames it creates are less accurate (recommended input FPS: 160-240minimum). The higher your clips' original FPS, the less artifacts you'll get and the faster speed preset you can use to trade accuracy for speed, in it's config you can set "interpolation speed" to medium, fast or faster. RIFE implementation is still WIP

Frame deduplication:
Since blur v1.8 there's a setting in the blur-config that's turned off by default called deduplicate, if you turn it on it'll look for duplicated frames (caused by FPS spikes / slight encoding lag) and try to fill in the gaps with interpolation. 

blur config explained:
If a setting isn't mentioned here, it's not relevant to be tuned except if you feel like it

blur:
blur - whether or not the output video file will be blurred
amount - if blur is enabled, this is the amount of motion blur (0 = no blur, 1 = fully blend every frame together, 1+ = more blur/ghosting).
output fps - if blur is enabled, this is the fps the output video will be

interpolation:
interpolate - whether or not the input video file will be interpolated to a higher fps
interpolated fps - if interpolate is enabled, this is the fps that the input file will be interpolated to (before blending)
interpolation speed - default is 'medium'
interpolation tuning - default is 'weak'
interpolation algorithm - default is '23'

rendering:
gpu - enables gpu accelerated rendering (likely faster, test for yourself)
deduplicate - removes duplicate frames and generates new interpolated frames to take their place
custom ffmpeg filters - custom ffmpeg flags (video filters and encoding args)

Custom FFmpeg output:
If you care about your render time, videos' size/quality, you can efficiently compress your videos with custom FFmpeg settings, here's a few of them to start off with:

For NVIDIA GPUs, you can put this after custom ffmpeg filters: for smaller clips:
-c:v hevc_nvenc -rc constqp -preset p7 -qp 18
or, a little less efficient but faster: (to encode & play back, so less preview lag):
-c:v h264_nvenc -rc constqp -preset p7 -qp 15

For AMD GPUs, same thing:
-c:v hevc_amf -quality quality -qp_i 16 -qp_p 18 -qp_b 20
same thing:
-c:v h264_amf -quality quality -qp_i 12 -qp_p 12 -qp_b 12

HEVC might not work at all on older cards / if you have some old drivers

##Section 3: Optimization Guides
Guides that talk about latency / both software & hardware :

⭐ Zusier's Archive https://github.com/Zusier/archive
⭐ Amit's https://github.com/amitxv/PC-Tuning
imribiy's NTLite Guide - https://cutt.ly/nA2fnK9
Sieger's handbook - https://github.com/sieger/handbook
GamingPCSetup - https://github.com/djdallmann/GamingPCSetup
Riot's Hit-Reg and Network Latency - https://cutt.ly/jA2oT2T (Seems to have been privated sadly)
Calypto's latency guide - https://calypto.us/
