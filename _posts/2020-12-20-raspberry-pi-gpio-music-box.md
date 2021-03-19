---
layout: post
title:  "Raspberry Pi GPIO Music Box"
category: python
---

The first Raspberry Pi project I worked on was the GPIO Music Box.

Here's the [project page](https://projects.raspberrypi.org/en/projects/gpio-music-box) on [raspberrypi.org](https://www.raspberrypi.org).

It's a simple project and a good introduction to the GPIO pins and how to use them, as well as importing modules, using built in functions, and using pygame (or at least pygame's built in sound mixer) to play sounds.

```
import pygame
from gpiozero import Button

#if using pygame version < 2.0.0
#pre-initialize pygame.mixer with a smaller buffer size to lessen sound lag
#(pygame 2.0.0 defaults to a buffer size of 512)
#512 seems to be the smallest buffer size before underrun error occurs

pygame.mixer.pre_init(44100, -16, 2, 512)
pygame.mixer.init()
pygame.init()

kick = pygame.mixer.Sound("/home/pi/gpio-music-box/samples/drum_bass_hard.wav")
snare = pygame.mixer.Sound("/home/pi/gpio-music-box/samples/drum_snare_hard.wav")
hihat = pygame.mixer.Sound("/home/pi/gpio-music-box/samples/drum_cymbal_closed.wav")
bass = pygame.mixer.Sound("/home/pi/gpio-music-box/samples/glitch_bass_g.wav")
glitch = pygame.mixer.Sound("/home/pi/gpio-music-box/samples/glitch_perc5.wav")

#blue/1 is 14
blue_button = Button(14)
#yellow/2 is 15
yellow_button = Button(15)
#green/3 is 18
green_button = Button(18)
#orange/4 is 23
orange_button = Button(23)
#white/5 is 24
white_button = Button(24)

blue_button.when_pressed = kick.play
yellow_button.when_pressed = snare.play
green_button.when_pressed = hihat.play
orange_button.when_pressed = bass.play
white_button.when_pressed = glitch.play
```

While working on the music box, I noticed that there is a considerable delay from the time a button is pressed, to the time a sound is played. (You can see/hear this delay in the first few seconds of the [project YouTube video](https://youtu.be/2izvSzQWYak) when Dr. Le Page 'plays' the music box.) 

It's probably only a second of delay but this is a long amount of time if you're looking to play the music box like you would a keyboard or MPC or drum machine. With these sorts of instruments, the buttons or triggers need to feel like they play a sound instantaneously, with probably only a few milliseconds being an acceptable amount of delay. 

It's similar to a gamepad, where a button press in a game makes a character perform an action; having a one second delay on a jump button could be the difference between making a successful leap or falling off the screen to your death.

I guess what we're talking about here is lag. So you might say, well, what if you anticipated the lag? If you know there's that big of a delay, just hit the button a second earlier. 

While this is possible, it doesn't make for a fun user experience. It'd be like trying to play a drum set with a band but needing to play one beat ahead in order to be in time with everyone. If you could, it'd make more sense to simply play on the beat, which luckliy, you can because of instant physical and auditory feedback from striking real drums and cymbals.

As I've found out, programming a music box to play a beat in real-time is not as straightfoward as I thought!

A big part of my interest in this project was taking the first steps to creating a MIDI controller or drum machine that could be used for playing and recording music.

After researching other Python libraries to play the sounds and eventually circling back around to pygame, I found that there is a way to lessen the delay, and it's an improvement over the original code. 

Unfortunately, I don't think there's an official Raspberry Pi repo for this project that I can push this change to. But here is a solution for the delay.

```
#if using pygame version < 2.0.0
#pre-initialize pygame.mixer with a smaller buffer size to lessen sound lag
#(pygame 2.0.0 defaults to a buffer size of 512)
#512 seems to be the smallest buffer size before underrun error occurs

pygame.mixer.pre_init(44100, -16, 2, 512)
pygame.mixer.init()
pygame.init()
```

You can see from my comment that by pre-initializing pygame.mixer, we can lessen the sound lag.

```pre_init()``` takes four parameters: 
- 44100 is the sample rate (or frequency in pygame)
- -16 is the bit depth (or size in pygame)
- 2 is the number of channels (in this case, stereo, but you can also set this to 1 for mono) 
- 512 is the buffer size

The [pygame mixer documentation](https://www.pygame.org/docs/ref/mixer.html) explains: 

> The buffer argument controls the number of internal samples used in the sound mixer. The default value should work for most cases. It can be lowered to reduce latency, but sound dropout may occur. It can be raised to larger values to ensure playback never skips, but it will impose latency on sound playback. The buffer size must be a power of two (if not it is rounded up to the next nearest power of 2).

I just noticed that since I've worked on the GPIO music box, pygame 2.0.0 was released in October 2020. 

Lo and behold, the default buffer size was changed, which basically nullifies the whole point of writing this! (You can also see the default frequency was changed.)

> Changed in pygame 2.0.0: The default buffersize was changed from 4096 to 512. The default frequency changed to 44100 from 22050.

I guess if you're using an older version of pygame, this post will still be helpful to you, as in the older versions, the buffer size was larger.

> Changed in pygame 1.8: The default buffersize was changed from 1024 to 3072.

> Changed in pygame 1.9.1: The default buffersize was changed from 3072 to 4096.

You can experiment with changing the buffer size to see how it affects the delay.

One last thing:

```
#if using pygame version < 2.0.0
#pre-initialize pygame.mixer with a smaller buffer size to lessen sound lag
#(pygame 2.0.0 defaults to a buffer size of 512)
#512 seems to be the smallest buffer size before underrun error occurs

pygame.mixer.pre_init(44100, -16, 2, 512)
pygame.mixer.init()
pygame.init()
```

```pygame.mixer.init()``` initializes the mixer. This ensures that the mixer is initialized with the values we pre-initialized in the line above.

Here's my [project repo](https://github.com/MikeParish/gpio_music_box) complete with the sounds if you want to build your own GPIO music box.

Thanks for reading and happy coding!

# License

Unless otherwise specified, everything in this repository is covered by the following license:

[![Creative Commons License](http://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

***GPIO Music Box*** by the [Raspberry Pi Foundation](http://www.raspberrypi.org) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

Based on a work at <https://github.com/raspberrypilearning/gpio-music-box>

I modified the original work to fix a problem with delay on sound playback (detailed in this [video](https://youtu.be/3FX-TNEDovw)). More info can be found at <https://424recording.com/raspberry-pi-gpio-music-box>
