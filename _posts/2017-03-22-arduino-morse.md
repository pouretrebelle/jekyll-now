---
layout: post
title: Morse Code Twitter Answering Machine
---

<div class="post__video"><iframe width="560" height="315" src="https://www.youtube.com/embed/bYPkuMVaIxE?showinfo=0" frameborder="0" allowfullscreen></iframe></div>
> TIL that the buzzing sound from this project can't be recorded??? used 2 pro grade mics and literally nothing. just imaging some quality morse-code-like buzzing when the light is pink.
> Vlog is a'coming

---

Like [my last project]({{ site.baseurl }}/magnetic-drawing-machine), my intention was to make a project that would leverage my magnetic implants, but as an output instead of an input. I took the elementary idea of converting text into electromagnetic fields resembling Morse code, and made it cool&trade; by hooking it up to the Twitter API.

It developed into a de-facto answering machine that outputs morse code either through a buzzer or an electromagnet, the speed of the playback can be manipulated by a dial, and there is also a button to initiate playback or trigger an API request (a minutely occurance anyway), as well as an LED to indicate the current state of the machine.

The light shows blue when there are no messages, red when there are messages to play, flashes pink when it's making an API request, and shows pink when it's handling the API request and during playback. The LED will turn off if the toggle is not switched to either output, but will show for API requests throughout.

![Circuit diagram]({{ site.baseurl }}/assets/arduino-morse/circuit-diagram.jpg)

I used an ESP2866 chip mounted on an Adafruit Huzzah breakout board for the microcontroller in order to have simple WiFi access alongside the ease of Arduino firmware. I went through [several iterations](https://github.com/pouretrebelle/arduino-morse/commits/master/circuit/circuit_diagram.pdf) of the circuit layout and had to compromise some features due to lack of I/O (I thought it was important for the microcontroller to be aware of the toggle switch's state instead of just electronically guiding the output to have an 'off state', but it was at the expense of the green LED).

![Breadboard mockup]({{ site.baseurl }}/assets/arduino-morse/photos1.jpg)

I soldered the chip and resistors onto perma proto board, attaching the components to loose wires so I could mount them onto the enclosure more easily.

![Perfboard layout]({{ site.baseurl }}/assets/arduino-morse/photos2.jpg)

To get the data from Twitter I set up a node.js app on [Glitch](https://glitch.com/edit/#!/tweet-grabber) which grabs mentions of a particular username since a particular point in time (by way of a specific 'since' tweet ID). I had a lot of trouble dealing with the datastructures to parse the Twitter json on the microcontroller side so elected instead to do that on the node side of things.

![Final Piece]({{ site.baseurl }}/assets/arduino-morse/photos3.jpg)
![Final Piece]({{ site.baseurl }}/assets/arduino-morse/photos4.jpg)
![Final Piece]({{ site.baseurl }}/assets/arduino-morse/photos5.jpg)

It looks pretty awesome. I did design the enclosure to fit a battery pack but the machine wouldn't work with 3 AAs, I'm waiting on a Lithium battery to solve that. For now a serial cable is adequate.

- [Check out this project on Github](http://github.com/pouretrebelle/arduino-morse)
