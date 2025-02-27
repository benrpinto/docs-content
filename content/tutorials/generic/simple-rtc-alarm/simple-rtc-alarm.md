---
author: 'Arduino'
description: 'This example demonstrate how to use the RTC library methods in order to do something when an alarm is matched.'
title: 'Simple RTC Alarm with a SAMD Board'
tags: [RTC]
---

This example demonstrate how to use the RTC library methods in order to do something when an alarm is matched. In particular in this example, the RTC time is set at 16:00:00 and an alarm at 16:00:10. When the time match using the match type `MATCH_HHMMSS` is reached, the attached interrupt function will print on the serial monitor **Alarm Match!**.

## Hardware Required

- [Arduino Zero](https://www.arduino.cc/en/Main/ArduinoBoardZero) or [MKRZero](https://www.arduino.cc/en/Main/ArduinoBoardMKRZero) or  [MKR1000](https://www.arduino.cc/en/Main/ArduinoMKR1000)

## Circuit

Only your Arduino Board is needed for this example.

![The circuit for this example.](assets/ArduinoZero_bb.jpg)



## Code

```arduino

/*

  Simple RTC Alarm for Arduino Zero and MKR1000

  Demonstrates how to set an RTC alarm for the Arduino Zero and MKR1000

  This example code is in the public domain

  https://www.arduino.cc/en/Tutorial/SimpleRTCAlarm

  created by Arturo Guadalupi <a.guadalupi@arduino.cc>

  25 Sept 2015



  modified

  21 Oct 2015

*/

#include <RTCZero.h>

/* Create an rtc object */

RTCZero rtc;

/* Change these values to set the current initial time */

const byte seconds = 0;

const byte minutes = 0;

const byte hours = 16;

/* Change these values to set the current initial date */

const byte day = 25;

const byte month = 9;

const byte year = 15;

void setup()
{

  Serial.begin(9600);

  rtc.begin(); // initialize RTC 24H format

  rtc.setTime(hours, minutes, seconds);

  rtc.setDate(day, month, year);

  rtc.setAlarmTime(16, 0, 10);

  rtc.enableAlarm(rtc.MATCH_HHMMSS);



  rtc.attachInterrupt(alarmMatch);
}

void loop()
{

}

void alarmMatch()
{

  Serial.println("Alarm Match!");
}
```