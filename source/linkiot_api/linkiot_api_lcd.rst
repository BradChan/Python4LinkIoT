=========================
可编程Lcd模块
=========================

LinkIoT具有可编程Lcd，可实现画点、线、矩形、圆等基本图像。


Colors
=========================
在Lcd编程中会使用颜色，可以使用24位整型数值，每种颜色8位。例如，0xFF0000就是红色，0xFF00就是绿色。

定义了一些颜色常量供快捷选择使用：

====================  ===============  ==============
   常量                  颜色              数值
====================  ===============  ==============
TFT_BLACK               黑色              0
TFT_NAVY                海蓝色            128
TFT_BLUE                蓝色              255
TFT_DARKGREEN           深绿色            32768
TFT_DARKCYAN            深青色            32896
TFT_GREEN               绿色              62580
TFT_CYAN                青色              65535
TFT_MAROON              栗色              8388608
TFT_PURPLE              紫色              8388736
TFT_OLIVE               橄榄绿            8421376
TFT_DARKGREY            深灰色            8421504
TFT_GREENYELLOW         黄绿色            11336748
TFT_LIGHTGREY           亮灰色            12632256
TFT_RED                 红色              16515072
TFT_MAGENTA             洋红色            16515327
TFT_ORANGE              橙色              16557056
TFT_PINK                粉红色             16564426
TFT_YELLOW              黄色              16579584
TFT_WHITE               白色              16579836
====================  ===============  ==============

Fonts
===========================

字体常量: 
**TFT_FONT_Default**, **TFT_DEJAVU18_FONT**, **TFT_DEJAVU24_FONT**, **TFT_UBUNTU16_FONT**, **TFT_COMIC24_FONT**,
**TFT_MINYA24_FONT**, **TFT_TOONEY32_FONT**, **TFT_SMALL_FONT**, **TFT_DEF_SMALL_FONT**, **TFT_FONT_7SEG**, **TFT_USER_FONT**

Lcd Methods
============================

画像素点
++++++++++++++++++++++++++++
**linkiot.Lcd.pixel(x, y [,color])** 

设置坐标点(x, y)的像素颜色，
颜色参数color为颜色值，选填参数。

画直线段
++++++++++++++++++++++++++++
**linkiot.Lcd.line(x, y, x1, y1 [, color])**

画坐标点(x, y)到坐标点(x1, y1)的直线，
颜色参数color为线条颜色值，选填参数。

画三角形
++++++++++++++++++++++++++++
**linkiot.Lcd.triangle(x, y, x1, y1, x2, y2 [,color,fillcolor])**

画坐标(x, y), (x1, y1)和 (x2, y2)三点相连的三角形，
颜色参数color和fillcolor选填，分别为三角形颜色和填充颜色。

画矩形
++++++++++++++++++++++++++++
**linkiot.Lcd.rect(x, y, width, height [,color, fillcolor])**

以坐标(x, y)为左上角顶点，width作为宽，height作为高，画矩形，
颜色参数color和fillcolor选填，分别为矩形颜色和填充颜色。

画圆形
++++++++++++++++++++++++++++
**linkiot.Lcd.circle(x, y, r [, color, fillcolor])**

以坐标(x, y)为圆心，r为圆半径画圆，
颜色参数color和fillcolor选填，分别为圆形的颜色和填充颜色。

画椭圆形
++++++++++++++++++++++++++++
**linkiot.Lcd.ellipse(x, y, rx, ry [,color, fillcolor])**

以坐标(x, y)为圆心，x方向半径为rx，y方向半径为ry画椭圆，
颜色参数color和fillcolor选填，分别为椭圆颜色和填充颜色。

显示文本
++++++++++++++++++++++++++++
**linkiot.Lcd.text(x, y, text [, color])**

显示屏输入文本显示，以(x, y)坐标为文本起点，text为文本内容，
颜色参数color选填，为文本颜色。

设置字体
++++++++++++++++++++++++++++
**linkiot.Lcd.font(font)**

设置linkiot显示屏文本字体，参数font选用Fonts字体常量。

设置背景色
++++++++++++++++++++++++++++
**linkiot.Lcd.setbg(color)**

设置显示屏背景颜色。

清屏
++++++++++++++++++++++++++++
**linkiot.Lcd.clear()**

清空显示屏显示内容

设置屏幕方向
++++++++++++++++++++++++++++
**linkiot.Lcd.setRotation(value)**

设置屏幕显示方向，使用默认常量设置。方向常量：**TFT_PORTRAIT** ，**TFT_LANDSCAPE**， **TFT_PORTRAIT_FLIP**，**TFT_LANDSCAPE_FLIP** 。 




示例1：

.. code-block:: python
    :linenos:

    import machine, utime
    from linkiot import *



    def rotateScreen():
        if linkiot.accX > 9.0:
            linkiot.Lcd.setRotation(TFT_LANDSCAPE)
        elif linkiot.accX < -9.0:
            linkiot.Lcd.setRotation(TFT_LANDSCAPE_FLIP)
        elif linkiot.accY > 9.0:
            linkiot.Lcd.setRotation(TFT_PORTRAIT_FLIP)
        elif linkiot.accY < -9.0:
            linkiot.Lcd.setRotation(TFT_PORTRAIT)

    ledStatus = False

    def on_wasPressed():
        print("button pressed")

    linkiot.button.wasPressed(on_wasPressed)

    while True:
        linkiot.updateAttitude()
        rotateScreen()
        
        if linkiot.wasShaked:
            print("shaked")
    
        linkiot.Lcd.clear()
        linkiot.Lcd.text(0,0,str(linkiot.accX), TFT_GREEN)
        linkiot.Lcd.text(0,25,str(linkiot.accY), TFT_BLUE)
        linkiot.Lcd.text(0,50,str(linkiot.accZ), TFT_PURPLE)
        linkiot.Lcd.text(0,75,str(linkiot.anglePitch), TFT_RED)
        linkiot.Lcd.text(0,100,str(linkiot.angleRoll), TFT_YELLOW)

        linkiot.setLed(ledStatus)
        ledStatus = not ledStatus
        utime.sleep_ms(200)