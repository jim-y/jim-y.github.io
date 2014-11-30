---
layout: post
title: rpi morse synthesizer
published: True
categories: [javascript]
tags: [raspberry, linux, javascript]
---

A morse synthesizer for RaspberryPi written in node via JohnnyFive.

## Prototyping

![pygmentized_cat](/assets/led_pelda.jpg)

## The Code

First, the morse code table for the english alphabet

```js
'use strict';
module.exports = {
  a: '01',
  b: '1000',
  C: '1010',
  d: '100',
  e: '0',
  f: '0010',
  g: '110',
  h: '0000',
  i: '00',
  j: '0111',
  k: '101',
  l: '0100',
  m: '11',
  n: '10',
  o: '111',
  p: '0110',
  q: '1101',
  r: '010',
  s: '000',
  t: '1',
  u: '001',
  v: '0001',
  w: '011',
  x: '1001',
  y: '1011',
  z: '1100'
};
```

Then the configs of the synthesizer

```js
'use strict';
module.exports = {
  shortMark: '0',
  longMark: '1',
  intraLetterMark: '/',
  intraWordMark: '#',
  shortGap: 100,
  longGap: 100 * 3,
  intraMarkGap: 100,
  intraLetterGap: 100 * 3,
  intraWordGap: 100 * 7
};
```

After that i wrote the more encoder, very simple though

```js
'use strict';

var config = require('./morse_config'),
    table = require('./morse_code_table');

module.exports.encode = function(message) {
  return message.split(' ').map(function(word) {
    return word.split('').map(function(letter) {
      return table[letter];
    }).join('/');
  }).join('#');
};
```

Lastly the fizz_buzz example, which translates a common english sentence to morse code, and synthesizes it trough a LED on the Raspberry breadboard.

```js
'use strict';

var MESSAGE = 'Welcome to the Internet of Things',
    config = require('./morse_config'),
    dit = config.shortGap,
    dah = config.longGap,
    morse = require('./morse'),
    raspi = require('raspi-io'),
    five = require('johnny-five'),
    board = new five.Board({
      io: new raspi()
    });

function compute(message, led) {
  
  if (message.length === 0) {
    return;
  }

  switch (message.shift()) {

    case '0':
      led.on();
      setTimeout(function() {
        led.off();
        setTimeout(
          compute.bind(null, message, led),
          config.intraMarkGap
        );
      }, dit);
      break;

    case '1':
      led.on();
      setTimeout(function() {
        led.off();
        setTimeout( 
          compute.bind(null, message, led),
          config.intraMarkGap
        );
      }, dah);
      break;

    case '/':
      setTimeout(
        compute.bind(null, message, led),
        config.intraLetterGap
      );
      break;

    case '#':
      setTimeout(
        compute.bind(null, message, led),
        config.intraWordGap
      );
      break;

    default:
      return true;
  }
}


board.on('ready', function() {

  var led = new five.Led(16),
      buzzer = new five.Pin(15),
      msg = morse.encode(MESSAGE.toLowerCase());

  compute(msg.split(''), led);

});
```

I didn't care about the quality of the JS code this time, just tried to make the thing work :)

## Demo

[Youtube link](http://youtu.be/DVll6zFRToU)