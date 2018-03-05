# Demo for waveshare 7.5 inch tri color display.

This demo code for [this display](https://www.waveshare.com/7.5inch-e-paper-hat-c.htm) was downloaded from [their wiki](https://www.waveshare.com/wiki/File:7.5inch_e-paper_hat_b_code.7z).
Unlike what you might expect from a Chinese reseller, Waveshare seems to have recognized the utility in providing usable documentation. Providing a link in the actual box would the cherry on top of the e-ink cake. Talking about e-ink, this type of display is also called *electronic paper display* hence the the acronmy epd you will encounter when reading the code.

This particular display is actually sourced from [Good Display]() and goes by the name of GDEW075C21. It is a 7.5 inch 600x384 pixel display which can display three colors: Black, White and Yellow (bwy). It is similar to the more common Black, White and Red (bwr) and works exactly the same except that it shows yellow instead of Red.

# Adafruit Huzzah ESP 8266 + 7.5 e-ink

Before trying out any other libraries I wanted to actually test if the display worked. The code was downloaded on (04.03.2018) and slightly modified to compile/run on the [Adafruit Huzzah](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266)

I used the following pin-out:

E-ink -> Huzzah

GND   ->  GND

3.3V  ->  3V

BUSY  ->  Pin 4

RST   ->  Pin 2

DC    ->  Pin 5

CS    ->  Pin 15

CLK   ->  SCK

DIN   ->  MOSI

To use this pin configuration please make sure that the pins are defined as following in the **epdif.h**:

```
#define RST_PIN         2
#define DC_PIN          5
#define CS_PIN          15
#define BUSY_PIN        4
```


Now it should display the following picture after flickering for some time. Refresh rate is rated at 31s. As far as I can tell it is normal that the yellow will appear last.

![Display](/res/display.png?raw=true "Adafruit Huzzah 8266 + 7.5 e-ink")

# Links

* https://github.com/ZinggJM/GxEPD/ Based off the Adafruit GFx library this seems to be well maintained and the project is active with the author replying in the [arduino forum](http://forum.arduino.cc/index.php?topic=487007.0)