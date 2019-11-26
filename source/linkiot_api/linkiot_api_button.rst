=========================
LinkIoT Button模块
=========================

LinkIoT具有可编程按钮button。


按钮按下状态
=========================
linkiot.button.wasPressed()
 方法返回按钮当前是否按下


linkiot.button.wasReleased()
 方法返回按钮是否释放状态即未按下状态


示例1：

.. code-block:: python
    :linenos:

    import time
    from linkiot import *

    while True:
        if linkiot.button.wasPressed():
            print("Button was pressed")
        
        if linkiot.button.wasReleased():
            print("Button was Released")

        utime.sleep(0.1)


按钮回调方法
===========================

示例2：

.. code-block:: python
    :linenos:

    import time
    from linkiot import *

    def on_wasPressed():
        print("Button was pressed")
    
    def on_wasReleased():
        print("Button was Released")

    linkiot.button.wasPressed(on_wasPressed)
    linkiot.button.wasReleased(on_wasReleased)