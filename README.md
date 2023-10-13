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

If you are a hardcore linux grey beard you probably are in the wrong place, you want each service as a [system daemon](https://github.com/OpenVoiceOS/ovos-systemd), you MUST have performance, you want to tune your config files, you want [native integration](https://github.com/OpenVoiceOS/raspbian-ovos/blob/dev/manual_user_install.sh) with your already existing OS! get out of this repo nerd!

## Install

install system libraries

debian: `sudo apt-get install -y build-essential python3-dev python3-pip python3-venv swig libssl-dev libfann-dev portaudio19-dev libpulse-dev cmake libncurses-dev pulseaudio-utils pulseaudio`

install ovos

`pip install ovos-launcher`

that's it! it's installed! Now go to [Running OVOS](#Running-OVOS)

## Running OVOS

by default you can only run OVOS 1 time, do not launch ovos multiple times! If you already have OVOS running as a system daemon, you are a nerd! wrong repo!

in the cli type `ovos-launcher`, that's it!

the essential OVOS stack is running in a single process with each service in its own thread

```bash
$ovos-launcher --help

Usage: ovos-launcher [OPTIONS]

Options:
  -l, --listener TEXT  Choose a listener for mic input handling,
                       dinkum/old/classic
  --help               Show this message and exit.
```

#### Troubleshooting

##### tflite_runtime failure

if setup fails to install tflite_runtime in your platform, you can find wheels here https://whl.smartgic.io/ , install `tflite_runtime` first and then retry to install `ovos-launcher`

eg, for python 3.11 in x86

`pip install https://whl.smartgic.io/tflite_runtime-2.13.0-cp311-cp311-linux_x86_64.whl`

##### Audio doesn't play

Issues with pipewire in Kubuntu have been observed. If you see a log similar to this:

```bash
2023-10-13 08:38:48.270 - ovos-launcher - ovos_dinkum_listener.voice_loop.voice_loop:run:222 - INFO - Wakeword detected
stream node 39 error: no node available
remote error: id=3 seq:7 res:-2 (No such file or directory): no node available
```

Create or edit a file at `~/.config/mycroft/mycroft.conf` with the following data:

```json
{
  "play_wav_cmdline": "paplay %1",
  "play_mp3_cmdline": "mpg123 %1"
}
```

That will force OVOS to use PulseAudio and mpg123 instead.

##### How do I install new skills???

OVOS skills are all Python packages that can be pip installed. Find the skill you want, and run `pip install git+$REPO` (ex: `pip install git+https://github.com/OpenVoiceOS/ovos-skill-easter-eggs`), then re-run `ovos-launcher`. Your new skill will be picked up as OVOS loads.

#### Known issues

OCP (OVOS Common Play) is coupled to the OVOS GUI, which does not run with `ovos-launcher`. Work is coming soon to decouple that requirement and get music skills working in a no-GUI configuration.
