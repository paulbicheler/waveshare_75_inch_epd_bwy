# Demo for waveshare 7.5 inch tri color display.

## Introduction
This demo code for [this display](https://www.waveshare.com/7.5inch-e-paper-hat-c.htm) was downloaded from [their wiki](https://www.waveshare.com/wiki/File:7.5inch_e-paper_hat_b_code.7z).
Unlike what you might expect from a Chinese reseller, Waveshare seems to have recognized the utility in providing usable documentation. Providing a link in the actual box would the cherry on top of the e-ink cake. Talking about e-ink, this type of display is also called *electronic paper display* hence the the acronmy epd you will encounter when reading the code.

This particular display is actually sourced from [Good Display]() and goes by the name of GDEW075C21. It is a 7.5 inch 600x384 pixel display which can display three colors: Black, White and Yellow (bwy). It is similar to the more common Black, White and Red (bwr) and works exactly the same except that it shows yellow instead of Red.

Before trying out any other libraries I wanted to actually test if the display worked. The code was downloaded on (04.03.2018) and slightly modified to compile/run on the [Adafruit Huzzah](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266)


## ## Instructions

* Download the Arduino IDE [from here]() This code was tested with version 1.8.5
* Follow the [Adafruit guide]() to setup the Feather Huzzah 8266 with the Arduino IDE
* Download zip or clone this repository o your local computer
    - If you downloaded the zip, unzip it
* Open the Arduino IDE and find out your Sketchbook folder
    - You can find your Sketchbook Location under File -> Preferences -> Sketchbook Location
    - Set the location to the downloaded/cloned folder.
    - Restart the Arduino IDE
* Open the demo sketch using File -> Sketchbook -> waveshare_75_inch_epd_bwy
* Make sure that the Board is set to Adafruit HUZZAH Esp 8266 
    - Setting the board is done under Tools -> Board
* Compile
* Connection the display breakout board to the Feather using the following pinout:
    - E-ink -> Huzzah
    - GND   -> GND
    - 3.3V  -> 3V
    - BUSY  -> Pin 4
    - RST   -> Pin 2
    - DC    -> Pin 5
    - CS    -> Pin 15
    - CLK   -> SCK
    - DIN   -> MOSI
* Upload the sketch.


If you want to change the pins you also need to change the pin configuration in the code by changing the file **epdif.h**:

```
#define RST_PIN         2
#define DC_PIN          5
#define CS_PIN          15
#define BUSY_PIN        4
```


Now it should display the following picture after flickering for some time. Refresh rate is rated at 31s. As far as I can tell it is normal that the yellow will appear last.

![Display](/res/display.png?raw=true "Adafruit Huzzah 8266 + 7.5 e-ink")

The display method is done in the setup method which means that if you want to rerun it you have to reset the board by pressing the Reset button.

# Further Reading

ased off the Adafruit GFX library the [gxEPD library](https://github.com/ZinggJM/GxEPD) seems to be well maintained and the project is active with the author replying in the [arduino forum](http://forum.arduino.cc/index.php?topic=487007.0).

Similar to the Waveshare samples you need to download / clone the repository and put it in the libraries folder of your Arduino folder or the Sketchbook folder. The name of the library in the IDE will be the same as the folder!

After you restart the Arduino IDE you see the library in Sketch -> Include Libraries -> Manage Libraries. 

I got the [GxEPD_SPI_TestExample](https://github.com/ZinggJM/GxEPD/tree/master/examples/GxEPD_SPI_TestExample) working with my Adafruit Huzzah Esp8266:

* In the 52 to 63 you need to comment every line except the one that matches your electronic paper display

 `#include <GxGDEW075Z09/GxGDEW075Z09.cpp>    // 7.5" b/w/r`

* In the `#if defined(ESP8266)` block you need to change the following lines

    ```
    static const uint8_t E_DC   = 5;
    static const uint8_t E_BUSY = 4;
    static const uint8_t E_RST  = 2;

    // GxIO_SPI(SPIClass& spi, int8_t cs, int8_t dc, int8_t rst = -1, int8_t bl = -1);
    GxIO_Class io(SPI, SS, E_DC, E_RST); // arbitrary selection of D3(=0), D4(=2), selected for default of GxEPD_Class
    // GxGDEP015OC1(GxIO& io, uint8_t rst = 2, uint8_t busy = 4);
    GxEPD_Class display(io, E_RST, E_BUSY); // default selection of D4(=2), D2(=4)
    ```

The display connections remain the same as before.