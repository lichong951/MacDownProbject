---
title: 常用代码模板 
tags: Android,模板,java
grammar_cjkRuby: true
---
[Shape](#shape)；[Activity](#Activity)；
## Shape
``` stylus
  <?xml version="1.0" encoding="UTF-8"?>
      <shape android:shape="oval"
      android:useLevel="false"
      xmlns:android="http://schemas.android.com/apk/res/android">
      <!-- 填充的颜色 -->
      <!--<solid android:color="#ffffff"/>-->
      <!-- 设置矩形的四个角为弧形 -->
      <!-- android:radius 弧形的半径 -->
      <stroke android:color="#B1BBBE" android:width="@dimen/size_4"/>
      <!--<corners android:radius="@dimen/size_90"/>-->
      <!-- 渐变 -->
      <!--<gradient-->
      <!--android:startColor="#4C9EFF"-->
      <!--android:endColor="#644DED"-->
      <!--android:angle="270" />-->
      <!--这里宽高要一样 -->
      <size android:width="@dimen/size_42"
          android:height="@dimen/size_42" />
  </shape>
```


## Activity最佳实践

``` stylus
public static void actionStart(Context context){
        context.startActivity(new Intent(context,GlodonGroupManageSearch.class));
    }
```
## ListView

``` stylus
class MyAdapter extends BaseAdapter {
    private Context context = null;
    public MyAdapter(Context context) {
            this.context = context;
    }
    @Override
    public int getCount() {
            return list.size();
    }
    @Override
    public Object getItem(int position) {
            return list.get(position);
    }
    @Override
    public long getItemId(int position) {
            return position;
    }
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
            ViewHolder mHolder;
            if (convertView == null) {
                    mHolder = new ViewHolder();
                    LayoutInflater inflater = LayoutInflater.from(context);
                    convertView = inflater.inflate(R.layout.item_listview_main_userlist, null, true);
                    mHolder.text_item_listview_username = (TextView) convertView.findViewById(R.id.text_item_listview_username);
                    mHolder.text_item_listview_email = (TextView) convertView.findViewById(R.id.text_item_listview_email);
                    mHolder.imageView_item_listview_headpic = (ImageView) convertView.findViewById(R.id.imageView_item_listview_headpic);
                    convertView.setTag(mHolder);
            } else {
                    mHolder = (ViewHolder) convertView.getTag();
            }
            String username = list.get(position).get("username").toString();
            String email = list.get(position).get("email").toString();
            int picId = Integer.parseInt(list.get(position).get("headpic").toString());
      mHolder.text_item_listview_username.setText(username);
            mHolder.text_item_listview_email.setText(email);
            mHolder.imageView_item_listview_headpic.setImageResource(picId);
            return convertView;
    }

    class ViewHolder {
            private TextView text_item_listview_username;
            private TextView text_item_listview_email;
            private ImageView imageView_item_listview_headpic;
    }
}
```

## 异常收集

``` stylus
package com.authentication.utils;

import android.content.Context;
import android.content.pm.PackageInfo;
import android.content.pm.PackageManager;
import android.os.Build;
import android.os.Environment;
import android.util.Log;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.PrintWriter;
import java.io.StringWriter;
import java.io.Writer;
import java.lang.reflect.Field;
import java.util.HashMap;
import java.util.Map;

/**
 * 奔溃日志处理
 */

public class CrashHandler implements Thread.UncaughtExceptionHandler {

    public static String TAG = "CrashHandler";


    //系统默认的UncaughtException处理类
    private Thread.UncaughtExceptionHandler mDefaultHandler;
    //CrashHandler实例
    private static CrashHandler INSTANCE;
    //程序的Context对象
    private Context mContext;
    //用来存储设备信息和异常信息
    private Map<String, String> infos = new HashMap<String, String>();

    private CrashHandler() {

    }

    /**
     * 获取CrashHandler实例 ,单例模式
     */
    public static CrashHandler getInstance() {
        if (INSTANCE == null)
            INSTANCE = new CrashHandler();
        return INSTANCE;
    }

    /**
     * 初始化
     *
     * @param context
     */
    public void init(Context context) {
        mContext = context;
        //获取系统默认的UncaughtException处理器
        mDefaultHandler = Thread.getDefaultUncaughtExceptionHandler();
        //设置该CrashHandler为程序的默认处理器
        Thread.setDefaultUncaughtExceptionHandler(this);
    }

    /**
     * 当UncaughtException发生时会转入该函数来处理
     */
    @Override
    public void uncaughtException(Thread thread, Throwable ex) {
        if (!handleException(ex) && mDefaultHandler != null) {
            //如果用户没有处理则让系统默认的异常处理器来处理
            mDefaultHandler.uncaughtException(thread, ex);
        } else {
            try {
                Thread.sleep(3000);
            } catch (InterruptedException e) {
                Log.i(TAG,e.toString());
            }
            //退出程序
            android.os.Process.killProcess(android.os.Process.myPid());
            System.exit(1);
        }
    }

    /**
     * 自定义错误处理,收集错误信息 发送错误报告等操作均在此完成.
     *
     * @param ex
     * @return true:如果处理了该异常信息;否则返回false.
     */
    private boolean handleException(Throwable ex) {
        if (ex == null) {
            return false;
        }
        //收集设备参数信息
        collectDeviceInfo(mContext);
        //保存日志文件
        String errorContent = saveCrashInfo2File(ex);
        saveFile(errorContent);
        return true;
    }

    /**
     * 保存到文件里
     *
     * @param errorContent
     */
    private void saveFile(final String errorContent) {
        new Thread() {
            @Override
            public void run() {
                String path = Environment.getExternalStorageDirectory().getPath() +  "/Tdemo.log";
                FileOutputStream outStream = null;
                try {
                    outStream = new FileOutputStream(new File(path)); //模式会检查文件是否存在，存在就往文件追加内容，否则就创建新文件。
                    outStream.write(errorContent.getBytes("UTF-8"));
                } catch (IOException e) {
                    e.printStackTrace();
                } finally {
                    if (outStream != null) {
                        try {
                            outStream.close();
                        } catch (IOException e) {
                            e.printStackTrace();
                        }
                    }
                }
                Log.d("CHEN", "错误日志路径:-------- " + path);
            }
        }.start();
    }

    /**
     * 收集设备参数信息
     *
     * @param ctx
     */
    public void collectDeviceInfo(Context ctx) {
        try {
            PackageManager pm = ctx.getPackageManager();
            PackageInfo pi = pm.getPackageInfo(ctx.getPackageName(), PackageManager.GET_ACTIVITIES);
            if (pi != null) {
                String versionName = pi.versionName == null ? "null" : pi.versionName;
                String versionCode = pi.versionCode + "";
                infos.put("versionName", versionName);
                infos.put("versionCode", versionCode);
            }
        } catch (PackageManager.NameNotFoundException e) {
            Log.d("CHEN", "CrashHandleran.NameNotFoundException---> error occured when collect package info: " + e.getMessage());
        }
        Field[] fields = Build.class.getDeclaredFields();
        for (Field field : fields) {
            try {
                field.setAccessible(true);
                infos.put(field.getName(), field.get(null).toString());
            } catch (Exception e) {
                Log.d("CHEN", "CrashHandler.NameNotFoundException---> an error occured when collect crash info: " + e.getMessage());
            }
        }
    }

    /**
     * 保存错误信息到文件中
     *
     * @param ex
     * @return 返回文件名称, 便于将文件传送到服务器
     */
    private String saveCrashInfo2File(Throwable ex) {

        StringBuffer sb = new StringBuffer();
        sb.append("---------------------sta--------------------------");
        for (Map.Entry<String, String> entry : infos.entrySet()) {
            String key = entry.getKey();
            String value = entry.getValue();
            sb.append(key + "=" + value + "\n");
        }

        Writer writer = new StringWriter();
        PrintWriter printWriter = new PrintWriter(writer);
        ex.printStackTrace(printWriter);
        Throwable cause = ex.getCause();
        while (cause != null) {
            cause.printStackTrace(printWriter);
            cause = cause.getCause();
        }
        printWriter.close();
        String result = writer.toString();
        sb.append(result);
        sb.append("--------------------end---------------------------");

        Log.i(TAG,sb.toString());
        return sb.toString();
    }
}

```

## SharedPreferences
```


import android.content.Context;
import android.content.SharedPreferences;

import java.util.Set;

public class SharedPreferencesUtil {
    public static final String SETTING_ANIM_STEP_VALUE = "setting_anim_step_value";
    public static final String AIR_TEMPE_MIN = "airTempeMin";
    public static final String AIR_TEMPE_MAX = "airTempeMax";
    public static final String FINGER_IS_USING = "fingIsUsing";
    public static final String AIR_HUM_MIN = "airHumMin";
    public static final String AIR_HUM_MAX = "airHumMax";
    public static final String AIR_ENABLE = "airEnable";
    private static SharedPreferencesUtil _instance = new SharedPreferencesUtil();
    public static SharedPreferencesUtil Instance(){
        return _instance;
    }
    private String KEY = "top.lc951.smartShelf";
    private SharedPreferences mSharedPreferences;

    public static final String IS_FOLLOW_DEVICE ="isFollowDevice";
    public static final String IS_VOICE_AUTH="isVoiceAuth";

    public static final String ARCHIVES_IP="ArchivesIp";
    public static final String ARCHIVES_PORT="ArchivesPort";
    public static final String MAIN_IP="mainIp";
    public static final String MAIN_PORT="mainPort";



    public void init(Context context){
        if(mSharedPreferences == null){
            mSharedPreferences= context.getApplicationContext().getSharedPreferences(KEY,0);
        }
    }

    /**
     * str: md5+isTracing
     */
    public void put(String id, String str){
        mSharedPreferences.edit().putString(id,str).commit();
    }

    public String get(String id){
        return mSharedPreferences.getString(id,"");
    }

    public String getMd5(String id){
        String str = mSharedPreferences.getString(id,"");
        if(!"".equals(str)){
            return str.substring(0,str.length()-1);
        }
        return "";
    }

    public int getIsTracing(String id){
        String str = mSharedPreferences.getString(id,"");
        if(str != null&&str.length()>0){
            return Integer.valueOf(str.substring(str.length()-1),str.length());
        }
        return 1;
    }

    public void remove(String id){
        mSharedPreferences.edit().remove(id).commit();
    }

    public Set<String> getIds(){
        return mSharedPreferences.getAll().keySet();
    }
    public void clear(){
        mSharedPreferences.edit().clear().commit();
    }

    public void putBoolean(String key, boolean b) {
        mSharedPreferences.edit().putBoolean(key,b).commit();
    }

    public boolean getBoolean(String key){
        return mSharedPreferences.getBoolean(key,false);
    }
    public boolean getBooleanDefaultFalse(String key){
        return mSharedPreferences.getBoolean(key,false);
    }

    public boolean putInt(String mainPort, int port) {
        return mSharedPreferences.edit().putInt(mainPort,port).commit();
    }

    public int getInt(String key) {
        return mSharedPreferences.getInt(key,0);
    }
    public boolean putFloat(String mainPort, float port) {
        return mSharedPreferences.edit().putFloat(mainPort,port).commit();
    }

    public float getFloat(String key) {
        return mSharedPreferences.getFloat(key,0);
    }
}

```
## Monkey

	adb shell monkey -p XXXXX -s 200 --throttle 500  --monitor-native-crashes -v -v -v 1000

欢迎使用 **{小书匠}(xiaoshujiang)编辑器**，您可以通过==设置==里的修改模板来改变新建文章的内容。