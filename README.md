# 2021LightDanceSTM
# 2021-LightDance-Arduino

# Rpi
### 檔案傳輸
- Mac to Rpi
    - `scp <Path to File To Copy> pi@<IP Address of Raspberry Pi>:<Path that File will Go>`
    - 傳輸終點可加可不加，預設大目錄
- Rpi to Mac
    - `scp pi@<IP Address of Raspberry Pi>:<Path to File To Copy>`
### SPI 
- [SPI介紹](https://learn.sparkfun.com/tutorials/serial-peripheral-interface-spi)
- [Arduino SPI library](https://www.arduino.cc/en/Reference/SPI)
- [Rpi Uno SPI](http://robotics.hobbizine.com/raspiduino.html)
### BCM2835.h
- Installation
    - download the latest version of the library, say bcm2835-1.xx.tar.gz, then:
        -    `wget http://www.airspayce.com/mikem/bcm2835/bcm2835-1.xx.tar.gz`
            `gunzip /bcm2835-1.25.tar.gz`
           `tar zxvf bcm2835-1.xx.tar.gz`
        `cd bcm2835-1.xx`
        `./configure`
        `make`
        `sudo make check`
        `sudo make install`
- [Compile with bcm2835](https://blog.gtwang.org/programming/gcc-comipler-basic-tutorial-examples/)
    - `gcc -o OutFile Code.c -lbcm2835`
- Execute
    - `sudo ./Outfile`
- SPI clock Speed
    - ![](https://i.imgur.com/Jd8oXOU.png)
    - 經實測DIVIDER要大於8，也就是RPi3的Clock要小於50MHz，而DIVIDER為16，延遲看起來最低
    - 測試環境：96顆燈，300個Bytes

| DIV_512-781kHz | DIV_128-3.125MHz | DIV_64-6.25MHz | DIV_32-12.5MHz | DIV_16-25MHz | DIV_8-50MHz |
|:--------------:|:----------------:|:--------------:|:--------------:|:------------:|:-----------:|
|     8.6 ms     |      4.4 ms      |     3.9 ms     |     3.6 ms     |   3.35 ms    |  Data Lost  |



- SPI reference
    - [語法](https://www.iot-programmer.com/index.php/books/22-raspberry-pi-and-the-iot-in-c/chapters-raspberry-pi-and-the-iot-in-c/32-getting-started-with-the-spi-bus?start=1)
    - [實作2](http://raspberryalphaomega.org.uk/2013/06/24/using-the-bcm2835-c-library-for-spi/)
    - [語法解釋](https://www.airspayce.com/mikem/bcm2835/group__spi.html#gad623657d9513faa89d22ae1dc87eec38)
# STM32
- Arduino IDE
    - **Note**: 在STM32duino裡面使用Serial1(PA9, PA10)一定要寫清楚是 Serial1 不能只寫 Serial
    - [接線＆ Arduino環境架設](https://atceiling.blogspot.com/2020/09/arduino81stm32arduino-ide.html)
- 燒錄
    - [ST-link](http://slemi.info/2018/08/14/making-your-own-st-link-v2/) 不需透過UART轉成tty-usb接口，但無法查看Serial1的輸出
# FastLED
### WS2812 驅動比較
 - [燈條函式庫筆記](https://hackmd.io/@openlabtaipei/H1tsHcXXD)
 - [FastLED vs. NeoPixel](https://blog.ja-ke.tech/2019/06/02/neopixel-performance.html#driving-methods)
 - [詳細介紹](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/fastled-library/#color)
### Library安裝
 - clone下來STM專屬[FastLED library ](https://github.com/13rac1/FastLED-STM32)
 - Arduino - 草稿碼 - 匯入程式庫 - 加入.zip程式庫
 - **注意！** 若本來有安裝過FastLED，需要把本來的刪掉