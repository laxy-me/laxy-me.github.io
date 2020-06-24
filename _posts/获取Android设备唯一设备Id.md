需求:获取每台设备唯一且与软件无关的唯一标识  
Android Q
#### 有效的硬件标识
1. Device ID  
问题：6.0之后需要READ_PHONE_STATE权限，没有权限获取不到。

2. Android ID  
设备首次启动时，系统随机生成一个64位的数字，并以16进制字符串保存下来。设备刷机之后会被重置。可能会重复

3. Mac地址  
WLAN Mac地址和Bluetooth Mac地址都是与硬件相关的唯一号码，分别需要ACCESS_WIFI_STATE和BLUETOOTH权限。  
需要有Wifi和蓝牙硬件。  
Android 6.0以后，官方为保护用户隐私关闭了获取Mac地址的接口。会统一返回02:00:00:00:00:00  
有黑科技可以获取

4. 广告ID