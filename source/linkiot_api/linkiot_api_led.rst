=========================
可编程Led模块
=========================

LinkIoT具有一颗可编程控制Led灯，引用LinkIoT模块即可直接控制使用。

控制Led亮/灭
=========================
linkiot.setLed(value)
 参数value是布尔型，若value为True，则Led灯亮，否则Led灭。

示例1：

.. code-block:: python
    :linenos:

    import time
    from linkiot import *

    ledStatus = False

    while True:
        linkiot.setLed(ledStatus)
        ledStatus = not ledStatus
        utime.sleep_ms(500)


控制Led灯亮度
==========================
linkiot.setLedBrightness(value)
 参数value是数字类型，可设置0~100。

示例2：

.. code-block:: python
    :linenos:

    import time
    from linkiot import *

    ledBrightness = 0

    while True:
        if ledBrightness > 100:
            ledBrightness = 0
        
        linkiot.setLedBrightness(ledBrightness)
        ledBrightness += 10
        utime.sleep_ms(100)





