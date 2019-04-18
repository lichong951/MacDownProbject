# 扫描蓝牙设备-设备联网认证-动画效果设计初稿

## 开启蓝牙扫描

* 蓝牙支持库
`implementation 'com.radiusnetworks:AndroidIBeaconLibrary:0.7.6'`
* 申请权限
``` stylus
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```
* 开启蓝牙
``` stylus
 BluetoothAdapter bluetoothAdapter = BluetoothAdapter.getDefaultAdapter();// 初始化本机蓝牙功能
        if (null == bluetoothAdapter)
            return;

        if (bluetoothAdapter.getState() == BluetoothAdapter.STATE_OFF)// 开蓝牙
            bluetoothAdapter.enable();
```
* 

> 参考
[https://github.com/AltBeacon/android-beacon-library](https://github.com/AltBeacon/android-beacon-library)
[]()

## 扫描设备记录去重
* 数据结构
`Map<String,Device> deviceMap=new HashMap<>()`
* 算法
``` stylus
 Device device ;
  if (scanResult.containsKey(newuuid)){
      device=scanResult.get(newuuid);
  }else {
        device=new Device();
        scanResult.put(newuuid, device);
  }
  '''
  if (scanResult.containsKey(newuuid)){
       //通知设备信号变化
    }else {
          device=new Device();
          scanResult.put(newuuid, device);
          //广播传递device
          
    }
```
* 广播传递
``` stylus
    /** 普通用，传递芯片号 */
    Intent intent = new Intent();
    Bundle bundle = new Bundle();
    bundle.putSerializable("BluetoothDevice", device);
    mIntent.putExtras(bundle);
    mIntent.setAction("com.glodon.gdb.bluetooth.service.BeaconServiceKq");
    sendBroadcast(mIntent);
```
* 广播接收
``` stylus
 /***
     * 广播接收得到扫描芯片
     */
    BroadcastReceiver broadcastReceiver = new BroadcastReceiver() {

        @Override
        public void onReceive(Context context, Intent intent) {
            Bundle bundle = intent.getExtras();
            if (null != bundle.get("BluetoothDevice")) {
               Device device= (Device) bundle.get("BluetoothDevice");
              //传递设备到待认证队列
              ...
            }
        }
    };
```
*

## 传递设备到待认证队列
* 数据结构

`BlockingQueue<Device> waitAuthFromNet = new LinkedBlockingQueue<>();`
* 进行认证过程
    * 认证返回成功进入待动画执行队列，并执行出队列操作
    * 认证返回失败，执行出队操作
    * 认证过程失败，再次执行
    * 直到认证队列为空
*

## 认证成功设备进入待动画执行队列
* 数据结构

`BlockingQueue<Worker> waitAnim = new LinkedBlockingQueue<>();`

* 监听动画过程
    * 动画完成；
    * 加入待执行考勤列表；
    * 执行出队
*

## 随机选取一个坐标作为动画的终点
* 数据结构
    * 坐标数组=12
    
* 算法
    * 随机抽取一个坐标进入动画执行坐标队列
    * 已使用坐标队列<=7
    * 待使用坐标队列=5
    * 先收回一个已使用的坐标入待使用坐标队列
    * 再从待使用坐标队列里出队一个坐标使用并入队已使用坐标

*


## 动画完成后刷新待记入考勤数量+1（待扩展数字滚动增加动画）
* 执行认证队列数量增1;后期考虑使用数字增加滚动动画