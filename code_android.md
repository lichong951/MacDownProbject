---
title: Android常用代码模板 
tags: Android,模板,java
grammar_cjkRuby: true
---
[Shape](#shape)；[Activity](#Activity)；[ListView](#ListView);[recyclerView](#RecyclerView);[webView](#WebView);[Gson](#Gson);[TabLayout](#TabLayout);[屏幕宽高](#屏幕宽高);
[Monkey](#Monkey);[阴影](#阴影);
[扫描雷达](#扫描雷达);
[动画](#动画);

## 动画
``` stylus
RotateAnimation rotateAnimation = new RotateAnimation(0, 359, Animation.RELATIVE_TO_SELF, 0.5f, Animation.RELATIVE_TO_SELF, 0.5f);
        rotateAnimation.setDuration(4000);
        rotateAnimation.setFillAfter(true);
        rotateAnimation.setRepeatMode(Animation.RESTART);
        //让旋转动画一直转，不停顿的重点
        rotateAnimation.setInterpolator(new LinearInterpolator());
        rotateAnimation.setRepeatCount(-1);

        ivScanningRotate.startAnimation(rotateAnimation);
```

` ivScanningRotate.clearAnimation();`
## 扫描雷达


> 参考
[]()
[http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2017/1214/8913.html](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2017/1214/8913.html)
[https://github.com/donkingliang/RadarView](https://github.com/donkingliang/RadarView)

## 阴影

`                        android:elevation="8dp"
`

## monkey
`adb -s emulator-5556 shell monkey -s 200 --throttle 300 -p com.glodon.gdb.app -v 100`

`adb -s emulator-5554 shell`


## 泡泡碰撞


https://demo.demohuo.top/jquery/22/2223/demo/

## 屏幕宽高

``` stylus
		WindowManager wm = (WindowManager) this
				.getSystemService(Context.WINDOW_SERVICE);
		int width = wm.getDefaultDisplay().getWidth();
		int height = wm.getDefaultDisplay().getHeight();
```

``` stylus
		WindowManager wm1 = this.getWindowManager();
		int width1 = wm1.getDefaultDisplay().getWidth();
		int height1 = wm1.getDefaultDisplay().getHeight();
```

``` stylus
		WindowManager manager = this.getWindowManager();
		DisplayMetrics outMetrics = new DisplayMetrics();
		manager.getDefaultDisplay().getMetrics(outMetrics);
		int width2 = outMetrics.widthPixels;
		int height2 = outMetrics.heightPixels;
```

``` stylus
		Resources resources = this.getResources();
		DisplayMetrics dm = resources.getDisplayMetrics();
		float density1 = dm.density;
		int width3 = dm.widthPixels;
		int height3 = dm.heightPixels;
```

## Gson
``` stylus
Gson gson = new Gson();
String jsonArray = "[\"Android\",\"Java\",\"PHP\"]";
String[] strings = gson.fromJson(jsonArray, String[].class);
List<String> stringList = gson.fromJson(jsonArray, new TypeToken<List<String>>() {}.getType());

```

``` stylus
//不再重复定义Result类
Type userType = new TypeToken<Result<User>>(){}.getType();
Result<User> userResult = gson.fromJson(json,userType);
User user = userResult.data;

Type userListType = new TypeToken<Result<List<User>>>(){}.getType();
Result<List<User>> userListResult = gson.fromJson(json,userListType);
List<User> users = userListResult.data;
```
[https://www.jianshu.com/p/e740196225a4](https://www.jianshu.com/p/e740196225a4)


## WebView

``` stylus
webView = new WebView(this);
        WebSettings settings = webView.getSettings();
        settings.setDomStorageEnabled(true);
        settings.setJavaScriptEnabled(true);
        settings.setBlockNetworkImage(false);
        webView.setWebViewClient(javaMethod.getWebViewClient());
        webView.setWebChromeClient(javaMethod.getWebChromeClient());
        webView.addJavascriptInterface(javaMethod,"androidTest");
        frameLayout.addView(webView);
//        webView.loadUrl("file:///android_asset/JsMethod.html");
        webView.loadUrl("file:///android_asset/www/page/person_overview.html");

```
.JAVA.CLOUD.AUTH=4d145eeb-7e5f-46c0-8c59-51789531df2a;__gm.t=eyJhbGciOiJIUzUxMiJ9.WlhsS2FHSkhZMmxQYVVwcllWaEphVXhEU214aWJVMXBUMmxLUWsxVVNUUlJNRXBFVEZWb1ZFMXFWVEpKYmpBdUxsSnFTVmhOVTAxNVRGVk5aRmxuWkdwNFNqRTFlWGN1WmpkSVoxQjRYMWwyYTBwVVZsaGpjMGs0Y1dKTGFIVXdNMlY2YlZZNWNVOUJaVzV2WlhObGIyaFhTRzF6Y1hoa1JVWlBiakJOZDFGdU1tMXZMVTlwVmtzeGVWWkNORmhQVmtsek0ycEhTWFZ0Vm0xeE9FNUVRMkpJVTNaSGFXMWllVEI0VDNwMFZEWjBXazF3UjBONlNGQkNaa0kzVUV0M1VXa3hOVTgyU0dNM1N6WldabmxEYVV4RWFFYzRNMVpsYTB0Sk1WUTFhM1JYVUhaZldGTXpNWGhqTTNCMlpIbDJUWEpWTGpGU00wMTVWbE15UlRaMWVtaE1aSE4wZWpGd1RWRT0.DHoeQfL4h3tWB3QVIEwhzDZNW4mocBWx78nR1_0VAe1jv8GuP1dg_jj3C2nf4MbBt1MJYjLScXL3pds7psts9Q;.CLOUD_ACCESS_TOKEN=cn-d555a4d0-5497-4893-aba3-15bfaf1f3864;

 


---
net：：ERR_CLEARTEXT_NOT_PERMITTED Android9.0无法加载url

解决：
    
    <?xml version="1.0" encoding="utf-8"?>
    <manifest ...>
        <uses-permission android:name="android.permission.INTERNET" />
        <application
            ...
            android:usesCleartextTraffic="true"
            ...>
            ...
        </application>
    </manifest>


---

## TabLayout

``` stylus
    <!--app:tabTextColor="#ffffff" 设置字体默认颜色-->
    <!--app:tabSelectedTextColor="#e40707" 设置字体被选中后的颜色-->
    <!--app:tabIndicatorColor="#30e407" 设置指示器颜色-->
    <!---->
    <!--app:tabBackground="@color/colorye" 设置Tab背景颜色-->
    <!--app:tabMode="scrollable"可滚动 app:tabMode="fixed"固定-->
    <android.support.design.widget.TabLayout
        android:id="@+id/tab_layout"
        android:layout_width="match_parent"
        android:layout_height="49dp"
        app:tabIndicatorHeight="5dp"
        app:tabIndicatorColor="#FF42C3FC"
        app:tabIndicatorFullWidth="false"
        />
```
#### 参考
https://www.jianshu.com/p/83922d08250b

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


## Activity

``` stylus
public static void actionStart(Context context){
        context.startActivity(new Intent(context,GlodonGroupManageSearch.class));
    }
```
## RecyclerView
``` stylus
 recyclerView = findViewById(R.id.recycler_view);
        LinearLayoutManager searchLayoutManager = new LinearLayoutManager(this);
        recyclerView.setLayoutManager(searchLayoutManager);
        adapter = new SingleItemTextAdapter(this, devices);
        recyclerView.setAdapter(adapter);
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

注意
	
    根据你的代码目前只看到了一种可能:看你在主线程clear了所有的list但并没有立即notifyadapter(等到网络请求回来再notify已经晚了).list的size发生改变就必须立即notifyadapte

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

## PopupWindow

``` stylus
private void showPopupWindow() {
        tvSetImg(chooseTime , R.mipmap.arrow_top);
        View view = LayoutInflater.from(TaskDownActivity.this).inflate(R.layout.choose_pop, null);
        final PopupWindow popupWindow = new PopupWindow(view, ViewGroup.LayoutParams.WRAP_CONTENT, ViewGroup.LayoutParams.WRAP_CONTENT, true);
        popupWindow.setTouchable(true);
        //一定要在代码中setBackgroundDrawable，不然点击外面popupWindow是不会dismiss的
        popupWindow.setBackgroundDrawable(getResources().getDrawable(R.drawable.shape_popup_view));
        popupWindow.showAsDropDown(chooseTime);
        popupWindow.setOnDismissListener(new PopupDismissListener());
        RecyclerView recyclerView = (RecyclerView) view.findViewById(R.id.rv_choose_pop);
        recyclerView.setLayoutManager(new LinearLayoutManager(this));
        ChooseTimeAdapter adapter = new ChooseTimeAdapter(TaskDownActivity.this, new ChooseTimeAdapter.MyItemClickListener() {
            @Override
            public void onClick(View view) {
                int tag = (int) view.getTag();
                chooseTime.setText(mData.get(tag));
                popupWindow.dismiss();
            }
        }, mData);
        recyclerView.setAdapter(adapter);
    }

    /**
     * 弹窗消失的时候让箭头换回来
     */
    class PopupDismissListener implements PopupWindow.OnDismissListener {
        @Override
        public void onDismiss() {
            tvSetImg(chooseTime , R.mipmap.arrow_down);
        }

    }

    /**
     * 设置textView右侧的图像
     * @param textView
     * @param img
     */
    private void tvSetImg(TextView textView ,int img) {
        Drawable nav_up = getResources().getDrawable(img);
        nav_up.setBounds(0, 0, nav_up.getMinimumWidth(), nav_up.getMinimumHeight());
        textView.setCompoundDrawables(null, null, nav_up, null);
    }
--------------------- 
作者：沐左 
来源：CSDN 
原文：https://blog.csdn.net/m0_37168878/article/details/78613947 
版权声明：本文为博主原创文章，转载请附上博文链接！
```

## XXXXAdapter extends BaseRecyclerAdapter

``` stylus
package com.glodon.glm.pad.adapter;

import android.content.Context;
import android.support.v7.widget.RecyclerView;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;

import com.andview.refreshview.recyclerview.BaseRecyclerAdapter;
import com.glodon.glm.pad.R;

import java.util.List;

/**
【结构】SingleItemTextAdapter（C）+SingleItemText(I)
 **/
public class SingleItemTextAdapter extends BaseRecyclerAdapter<SingleItemTextAdapter.ViewHolder> {

    private Context context;

    public void setList(List<? extends SingleItemText> list) {
        this.list = list;
        notifyDataSetChanged();
    }

    private List<? extends SingleItemText> list;

    public void setOnItemClickListener(OnItemClickListener onItemClickListener) {
        this.onItemClickListener = onItemClickListener;
    }

    private OnItemClickListener onItemClickListener;
    public SingleItemTextAdapter(Context context, List<? extends SingleItemText> list) {
        this.context = context;
        this.list = list;
    }

    @Override
    public ViewHolder getViewHolder(View view) {
        return new ViewHolder(view,false);
    }

    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType, boolean isItem) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.glodon_team_adapter_item, parent, false);
        ViewHolder viewHolder=new ViewHolder(view,false);
        viewHolder.itemView.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                onItemClickListener.onItemClick(v);
            }
        });
        return viewHolder;
    }

    @Override
    public void onBindViewHolder(ViewHolder holder, int position, boolean isItem) {
        SingleItemText itemText=list.get(position);
        holder.textView.setText(itemText.getText());
    }

    @Override
    public int getAdapterItemCount() {
        return null == list ? 0 : list.size();
    }

    public class ViewHolder extends RecyclerView.ViewHolder {

        TextView textView;

        public ViewHolder(View itemView, boolean isItem) {
            super(itemView);
            textView = itemView.findViewById(R.id.tv_item);
        }
    }
}

```

### Annotation processors must be explicitly declared now.  The following dependencies on the compile classpath are found to contain annotation processor.  Please add them to the annotationProcessor configuration.- lombok-1.18.6.jar (org.projectlombok:lo

        A problem occurred evaluating project ':glw'.
        > Could not find method javaCompileOptions() for arguments [build_dvpewjfi1881dp1y6jjukd2h5$_run_closure1$_closure5@1984580f] on object of type com.android.build.gradle.AppExtension.


## 记录
https://blog.csdn.net/hardworkingant/article/details/78158154

欢迎使用 **{小书匠}(xiaoshujiang)编辑器**，您可以通过==设置==里的修改模板来改变新建文章的内容。