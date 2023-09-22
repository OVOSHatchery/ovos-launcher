# ovos-launcher

Who is this repo for?

If these questions are something you can picture yourself asking, you are in the right place!
- where is the desktop icon?
- how do i install the app?
- I NEED start-mycroft.sh
- where do i click to run the assistant application
- what is the launch command
- what is a system daemon? what is systemd?
- I install ovos-core but nothing happpens, now what?

Hello newcomer! OpenVoiceOS provides a larger number of applications and packages, it is a Voice Operating System!
This can be overwhelming when you just want to try out and have a quick chat with a voice assistant, this repo tries to soften your introduction to ovos by providing the most accessible way to run the basic voice assistant stack

If you are a hardcore linux grey beard you probably are in the wrong place, you want each service as a system daemon, you MUST have performance, you want to tune your config files, you want native integration with your already existing OS! get out of this repo nerd!

## Install

install system libraries

debian: `sudo apt-get install XXXX TODO`
arch: `XXXX TODO`
fedora: `XXXX TODO`

`pip install ovos-launcher`

that's it!

## Running OVOS

by default you can only run OVOS 1 time, do not launch ovos multiple times! If you already have OVOS running as a system daemon, you are a nerd! wrong repo!

in the cli type `ovos-launcher`, that's it! the essential OVOS stack is running in a single process with each service in it's own thread