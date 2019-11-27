=========================
可编程加速度传感器模块
=========================

LinkIoT具有加速度传感器，可以获取姿态X 、Y、Z方向的数值和检测是否摇晃状态。

更新加速度传感器
=========================
linkiot.updateAttitude()
 updateAttitude()方法更新加速度传感器数值，再获取传感器的数值和状态前，必须先使用该方法，才能获取当前传感器实际数值。

X Y Z方向加速度数值
=========================

linkiot.accX
 accX属性返回当前X方向加速度数值

linkiot.accY
 accY属性返回当前Y方向加速度数值

linkiot.accZ
 accZ属性返回当前Z方向加速度数值

示例1：

.. code-block:: python
    :linenos:

    import time
    from linkiot import *

    while True:
        linkiot.updateAttitude()
        print("x = " + str(linkiot.accX))
        print("y = " + str(linkiot.accY))
        print("z = " + str(linkiot.accZ))
        utime.sleep(0.3)


俯仰角（Pitch angle）和翻滚角（Roll angle）
===========================

linkiot.anglePitch
 anglePitch属性返回俯仰角角度

linkiot.angleRoll
 angleRoll属性返回翻滚角角度

示例2：

.. code-block:: python
    :linenos:

    import time
    from linkiot import *

    while True:
        linkiot.updateAttitude()
        print("Pitch angle = " + str(linkiot.anglePitch))
        print("Roll angle = "  + str(linkiot.angleRoll))
        utime.sleep(0.2)


振动状态
=============================

linkiot.wasShaked
 wasShaked属性返回当前是否振动

示例3：

.. code-block:: python
    :linenos:

    import time
    from linkiot import *

    while True:
        linkiot.updateAttitude()
        if linkiot.wasShaked:
            print("Shaked")
        utime.sleep(0.1)