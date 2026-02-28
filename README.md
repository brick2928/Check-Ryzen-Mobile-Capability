# Welcome
This repo will explain to you how you can quickly check what your Ryzen Mobile CPU is capable of! 

## Navigation

[CPU Undervolting Guide](https://github.com/brick2928/Check-Ryzen-Mobile-Capability/edit/main/README.md#cpu-undervolting)
[iGPU Undervolting Guide](https://github.com/brick2928/Check-Ryzen-Mobile-Capability/edit/main/README.md#igpu-undervolting)
Memeory overclocking Guide - TBD

## Required Software
### Universal x86 Tuning Utility
Universal x86 Tuning Utility is a software that lets you tune your CPU in a lot of ways. We will be mainly using this tool for undervolting. 
You can download UXTU(Universal x86 Tuning Utility) from Command line using winget via "winget install JamesCJ60.Universalx86TuningUtility",

I recommend this because winget will install dependencies you need automatically excluding PawnIO.

Or you can get the official installer and portable from [here.](https://github.com/JamesCJ60/Universal-x86-Tuning-Utility/releases) 

UXTU needs a lot of dependencies like MS .net desktop runtime and pawnIO, if you struggle somehow you can join the discord server of this software [here.](https://discord.gg/u8eEAMTzU4)

<img width="861" height="480" alt="image" src="https://github.com/user-attachments/assets/923fdecf-3cd4-4007-9fd4-0d2bdedc73ac" />

This is the custom tab. You will be spending most of your time here. As you can see its the third tab on the left side, in this screenshot I scrolled down to showcase the curve optimizer options.

### Hwinfo64
Hwinfo64 is a powerful tool capable of a lot of things, but we are mainly interested in the sensors feature. You can download HWinfo64 [here.](https://www.hwinfo.com/download/) Hwinfo64 doesnt not have any dependencies you need to seperately download/install.

<img width="354" height="288" alt="{5DC4B0E6-3536-4994-8CFA-876E65DE96CE}" src="https://github.com/user-attachments/assets/1bbe3f7e-f1af-4652-889d-c3d505c6b431" />

This is how the start screen of HWinfo64 looks. Upon first install, it will be set to Full Mode however we do not need Full Mode as its cluttered and has features which we do not need. Select "Sensors Only" in the drop down menu. 
After choosing sensors only mode and pressing start, you should now be seeing something like this:
<img width="700" height="1000" alt="{09294320-9618-47D9-86DE-11AD3475ED09}" src="https://github.com/user-attachments/assets/df99473a-5e7e-47c3-b2e5-f156c740bfe4" />

We will spend most of our time here. 

## Curve Optimizer 
### CPU Undervolting
Checking Curve Optimizer compatiblity is pretty easy. I will recommend you to use UXTU (Universal x86 tuning utility)
and HWinfo64, even though CPU-Z and GPU-Z can technically also get the job done.

Curve Optimizer is AMD's undervolting technology, its available for both the CPU and the iGPU. There are multiple ways to check the current iGPU and CPU voltage, however we will be using HWinfo64 since its a very capable tool picking up on pretty much every sensor on the device you could need including CPU VID and GFX Voltage.

Start HWinfo64 with Sensors only mode and then look for the Core VID(s) sensor. It should looks something like this:
<img width="1220" height="585" alt="image" src="https://github.com/user-attachments/assets/f9ffca9e-ed9b-47e4-8683-3eeadd6bb7b9" />

The amount of sensors you have on your device will depend on your motherboard manufacturer and CPU generation, however these sensors in the screenshot should look the same for the most part.

Now start a stress test aimed at your CPU, I recommend you run cinebench r23 10 minutes stress test. This will lock your cpu at its maximu performance state and mostly stop the voltage from fluctuating. Take note of the voltage your cpu stays at. 
Now start UXTU, go into the custom tab and find the All Core Curve Optimizer option and make sure its ticked at the left for it to apply. Now drag the slider down to -15, dont apply yet. Make sure you are watching the CPU Core VID(s) at the same time. You can double click that sensor to get an extra graph of it.
When you are ready, click apply (ignore the fact that this is on a intel system)

<img width="1203" height="715" alt="image" src="https://github.com/user-attachments/assets/282adf33-53ba-4d96-a511-a1bc6cebaf49" />

Now watch the graph for a consistent drop in the CPU Core VID(s), did you notice a drop? If you arent sure, you can try setting a +15 or +30 curve optimizer offset temporarily.
__With a short test, positive curve optimizer will not do any harm, but if you use a positive CO offset consistently it could degrade the CPU.__
If your cpu voltage increases with positive curve optimizer or decreases with negative curve optimizer, then your cpu is capable of undervolting.

When making a issue at the AMD-Mobile-overclocking-capabilities repo, please post 2 screenshots like this:

First screenshot showing lower voltage and higher clocks with negative Curve Optimizer, 0.756MV
<img width="1616" height="1006" alt="image" src="https://github.com/user-attachments/assets/663f91b2-064e-482d-8abe-ffc21d865095" />

Second screenshot showing higher voltage and lower clocks with positive Curve Optimizer, 0.787MV
<img width="1920" height="1027" alt="image" src="https://github.com/user-attachments/assets/e47a4bb1-35bf-47c8-a580-f901e354a807" />


in both screenshots, cinebench r23 is runing in the background. 
This concludes our testing of the CPU CO capability. If the CPU Core VID(s) differ with different CO offsets, then your CPU supports CO. If the CPU Core VID(s) do not change at all and stay stable, that indicates the CPU does not support undervolting.

### iGPU undervolting

iGPU/iGP undervolting is pretty simple. 

Follow the CPU undervolting guide all the way down to "Now start UXTU, go into the custom tab and find the All Core Curve Optimizer option and make sure its ticked at the left for it to apply."
Instead of "All Core Offset" Choose the "iGPU Offset" option:
<img width="986" height="231" alt="image" src="https://github.com/user-attachments/assets/5881de5c-b216-400c-8f6b-c404465dde8f" />

Instead of looking at the CPU Core VID(s) you will be looking at the GFX voltage, it will depend on the generation of your CPU what that sensor is called. Here is a example of what it could look like:
<img width="644" height="370" alt="image" src="https://github.com/user-attachments/assets/a38e6e75-ad23-4993-9631-44fce5240913" />

Start any kind of heavy workload that will fully utilize your iGPU. I will use Furmark 2 as a example. 
You can install Furmark 2 through CMD by writing "winget install furmark2" and it will automatically install, or alternatively you can install it from [here.](https://www.techpowerup.com/download/furmark/)

Make sure the stress test runs on your iGPU:

<img width="539" height="753" alt="image" src="https://github.com/user-attachments/assets/b7730e9f-062b-48bb-83c5-bc9d69135be6" />

Click "RUN TEST" and the stress test will launch.
Now watch the iGPU behaviour on HWinfo64

Make sure:
- GPU Utilization is maxed out at 99%+
- GPU voltage is stable at a specific value, in my case 1v
- GPU Clock is mostly stable at its maximum
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/e0bb905c-bde3-49f9-a227-6ff8b093546f" />
Now, set a negative iGPU Offset, -15 should be safe starting point. Watch the graph and the sensor for any changes in the voltage.
If you arent sure wether the voltage changed, you can try setting a +30 iGPU Offset.

**With a short test, positive curve optimizer will not do any harm, but if you use a positive CO offset consistently it could degrade the iGPU.**

If the VID goes up or down by 30mv or more, then your CPU is CO capable. If the iGPU voltage stays where it is, the iGPU isnt not capable of utilizing iGPU Curve Optimizer. 
