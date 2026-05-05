+++
title = "Surf Camera"
date = "2025-12-01"
description = "Remote surf camera for checking real-time conditions"
repo = "https://github.com/ottowillborn/surf-cam-project"
demo = "https://drive.google.com/file/d/1bP89tZNPIIb6sGZLYniAG5QkJzFCBAgP/view?usp=sharing"
stack = ["react", "typescript", "python", "pi"]
icon = "/images/surfcamlogo.PNG"
featured = true
+++

I built this project to solve a simple problem: I wanted to check the surf conditions at my local break without driving all the way there. It turned into a deep dive into streaming, networking, and off-grid power management. For the code side that is... I got to learn a ton about 3D design and hardware management as well!

## What’s under the hood
The system is split into two main parts that work together to stream high-quality video from the coast to my phone or desktop:

* **The Controller:** A Raspberry Pi running a custom Python backend. It handles the camera feed via the `Picamera2` library, pushing a real-time MJPEG stream. I used `Tailscale` to keep the connection secure and low-latency, even when streaming from a remote location.
* **The App:** I built a custom `React Native` app so I can check the feed on the go. It’s fully cross-platform (iOS, Android, and Desktop), which made managing the different environment configs a fun challenge.

## Recent Field Upgrades
Since this thing lives outside, I’ve been constantly tweaking it to make it more reliable for long-term, off-grid deployments:

* **Solar & Battery:** I’ve added hardware support for solar power so it can run indefinitely.
* **Battery Monitoring:** I refactored the controller to log battery data, so I know exactly how much juice is left before I need to worry about power. It logs to a local database intermittently to save on space, plus opens the door for future analysis and optimizations.
* **Smart UI:** I added a `BatteryModal` component in the app, so I can see my battery stats in real-time right alongside the video feed. 

## TODO
It's most definitely still a work in progress... Theres a few problems which im always mentally troubleshooting:

* **Remote Network Connection:** Sure it works locally on a wifi network and in *theory* would work just fine on a wifi network hosted over a cellular connection, but how to connect it is still up in the air. I've researched sim-to-wifi adapters, but these would require an American carrier and plan as that is the only service at the location. It would also be expensive on the battery life of the system. Another idea I had was a relay of radio transmitters, but with limited range and throughput im not sure if the tradoff would be worth it.

* **Weatherproofing:** I built it into a Pelican case with all of the electrical components harnessed inside, except for the small camera. I've been doing some research on the best translucent materials to put over the lens, balancing visibility, protection, potential for glare and fog, plus resistance to scratches and damage. Have a feeling this might just be a trial and error situation...

## Gallery
{{< gallery >}}
![Alt text](/images/camassembly.jpg)
![Alt text](/images/camdemo.png)
![Alt text](/images/socket.jpg)
![Alt text](/images/soc.jpg)
![Alt text](/images/IMG_1731.jpeg)
![Alt text](/images/IMG_1732.jpeg)
{{< /gallery >}}
