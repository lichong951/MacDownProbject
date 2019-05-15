---
title: Android常用代码模板 
tags: Android,模板,java
grammar_cjkRuby: true
---
[Shape](#shape)；[Activity](#Activity)；[ListView](#ListView);[recyclerView](#RecyclerView);[webView](#WebView);[Gson](#Gson);[TabLayout](#TabLayout);[屏幕宽高](#屏幕宽高);
[Monkey](#Monkey);[阴影](#阴影);[扫描雷达](#扫描雷达);[动画](#动画);
[动画](#定点平移动画);
[PopupWindow](#PopupWindow);
[Glide](#Glide);
[自动安装](#自动安装);
[呼吸灯](#呼吸灯);
[wifi热点（AP）](#Wifi热点（AP）);
[](#Bitmap转缓存输入流BufferedInputStream)
[](#)

##
## Bitmap转缓存输入流BufferedInputStream
[https://blog.csdn.net/u013008419/article/details/45170387](https://blog.csdn.net/u013008419/article/details/45170387)

## Wifi热点（AP）
[https://juejin.im/post/5bec1a5d6fb9a049be5d0aa8](https://juejin.im/post/5bec1a5d6fb9a049be5d0aa8)
[https://blog.csdn.net/a_zhon/article/details/52472657](https://blog.csdn.net/a_zhon/article/details/52472657)
[https://blog.csdn.net/vnanyesheshou/article/details/82147110](https://blog.csdn.net/vnanyesheshou/article/details/82147110)
[https://blog.csdn.net/guang_liang_/article/details/55224675](https://blog.csdn.net/guang_liang_/article/details/55224675)
## 保活
[https://juejin.im/post/5baedde6f265da0a8d369eb2](https://juejin.im/post/5baedde6f265da0a8d369eb2)

## IP&网关


## 启动页
``` stylus
<style name="SplashTheme">
    <!--关闭启动窗口-->
    <item name="android:windowDisablePreview">true</item>
</style>
```
``` stylus
<activity
    android:name=".SplashActivity"
    android:label="@string/app_name"
    android:theme="@style/SplashTheme">
    <intent-filter>
        <action android:name="android.intent.action.MAIN"/>
        <category android:name="android.intent.category.LAUNCHER"/>
    </intent-filter>
</activity>
```

``` stylus
<style name="SplashTheme">
    <item name="android:windowBackground">@drawable/placeholder_ui</item>
</style>
```

> 参考
[https://imeiji.github.io/2017/11/13/Android%20App%20%E5%90%AF%E5%8A%A8%E9%A1%B5%E9%9D%A2%E6%9C%80%E4%BD%B3%E5%AE%9E%E7%8E%B0/](https://imeiji.github.io/2017/11/13/Android%20App%20%E5%90%AF%E5%8A%A8%E9%A1%B5%E9%9D%A2%E6%9C%80%E4%BD%B3%E5%AE%9E%E7%8E%B0/)
[https://segmentfault.com/a/1190000016125742](https://segmentfault.com/a/1190000016125742)
[https://jaeger.itscoder.com/android/2015/11/18/android-splash.html](https://jaeger.itscoder.com/android/2015/11/18/android-splash.html)
[https://www.jianshu.com/p/7e2983b65ead](https://www.jianshu.com/p/7e2983b65ead)
[https://www.jianshu.com/p/662274d5d637](https://www.jianshu.com/p/662274d5d637)
[https://www.jianshu.com/p/6a863fac3f58](https://www.jianshu.com/p/6a863fac3f58)
[https://juejin.im/post/5bf8f90a518825396d71ff2a](https://juejin.im/post/5bf8f90a518825396d71ff2a)
[https://blog.csdn.net/qq_36455052/article/details/78429713](https://blog.csdn.net/qq_36455052/article/details/78429713)




## 呼吸灯

animator/anim_breath.xml
``` stylus
<set xmlns:android="http://schemas.android.com/apk/res/android"
     <!-顺序动画->
     android:ordering="sequentially"> 
    <set 
        <!--插值器使用立方减速 效果很逼真-->
        android:interpolator="@android:interpolator/decelerate_cubic"
        android:ordering="together">
        <!--同步动画-->
        <!--X Y轴同时放大5% -->
        <objectAnimator
                android:propertyName="scaleX"
                android:duration="2700"
                android:valueTo="1.05"
                android:valueFrom="1"
                android:valueType="floatType"/>
        <objectAnimator
                android:propertyName="scaleY"
                android:duration="2700"
                android:valueTo="1.05"
                android:valueFrom="1"
                android:valueType="floatType"/>
    </set>
    <set 
        android:interpolator="@android:interpolator/decelerate_cubic"
        android:ordering="together">
        <!--X Y轴同时缩小回原始大小 -->
        <objectAnimator
                android:propertyName="scaleX"
                android:duration="1300"
                android:valueTo="1"
                android:valueFrom="1.05"
                android:valueType="floatType"/>
        <objectAnimator
                android:propertyName="scaleY"
                android:duration="1300"
                android:valueTo="1"
                android:valueFrom="1.05"
                android:valueType="floatType"/>
    </set>
</set>
```

``` stylus
public class BreathAnim {
    AnimatorSet mSet;

    public BreathAnim(Context ctx, int animRid, Object target) {
        mSet = (AnimatorSet) AnimatorInflater.loadAnimator(ctx, animRid);
        mSet.setTarget(target);
        mSet.addListener(new Animator.AnimatorListener() {
             …
            @Override
            public void onAnimationEnd(Animator animation) {
                //ToDo
                mSet.start();
            }
            ...
        });
    }

    public void start() {
        mSet.start();
    }

    public void cancel() {
        mSet.cancel();
        mSet = null;
    }
}
```

最后简单调用

``` stylus
BreathAnim ba=new BreathAnim(context,R.animator.anim_breath,mTargetView);
ba.start();
```

> 参考地址
[https://www.jianshu.com/p/4b4a5a1df589](https://www.jianshu.com/p/4b4a5a1df589)
[http://linkyan.github.io/2013/06/breath/](http://linkyan.github.io/2013/06/breath/)
[]()

## 自动安装
``` stylus
//普通安装
private static void installNormal(Context context,String apkPath) {
    Intent intent = new Intent(Intent.ACTION_VIEW);
    //版本在7.0以上是不能直接通过uri访问的
    if (Build.VERSION.SDK_INT > Build.VERSION_CODES.N) {
        File file = (new File(apkPath));
        // 由于没有在Activity环境下启动Activity,设置下面的标签
        intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
        //参数1 上下文, 参数2 Provider主机地址 和配置文件中保持一致   参数3  共享的文件
        Uri apkUri = FileProvider.getUriForFile(context, "com.example.chenfengyao.installapkdemo", file);
        //2. 设置 category 如果没有这个会有一个选择列表（比较糟糕的现象）
         intent.addCategory(Intent.CATEGORY_DEFAULT);
        //添加这一句表示对目标应用临时授权该Uri所代表的文件
        intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
        intent.setDataAndType(apkUri, "application/vnd.android.package-archive");
    } else {
        intent.setDataAndType(Uri.fromFile(new File(apkPath)),
                "application/vnd.android.package-archive");
    }
    context.startActivity(intent);
}
```
[https://blog.csdn.net/cfy137000/article/details/70257912](https://blog.csdn.net/cfy137000/article/details/70257912)

## Glide

[https://www.jianshu.com/p/91161f458cd8](https://www.jianshu.com/p/91161f458cd8)
[https://juejin.im/post/5b3a3b8d6fb9a025080411e8](https://juejin.im/post/5b3a3b8d6fb9a025080411e8)

[https://www.jianshu.com/p/89567c934008](https://www.jianshu.com/p/89567c934008)

### 圆角+圆角边框
[https://www.jianshu.com/p/d44206f36106](https://www.jianshu.com/p/d44206f36106)

[https://blog.csdn.net/aiguoguo000/article/details/80185011](https://blog.csdn.net/aiguoguo000/article/details/80185011)
[]()
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

``` stylus

//        //初始化 Translate动画
//        TranslateAnimation translateAnimation = new TranslateAnimation(
//                itemView.getX(),
//                Utils.dp2px(this,220),
//                itemView.getY(),
//                Utils.dp2px(this,320));
//        //初始化 Alpha动画
//        AlphaAnimation alphaAnimation = new AlphaAnimation(0.3f, 1.0f);
//
//        ScaleAnimation scaleAnimation = new ScaleAnimation(1f, 0.625f, 1f, 0.625f,
//                ScaleAnimation.ABSOLUTE,
//                itemView.getWidth() / 2f,
//                ScaleAnimation.ABSOLUTE, itemView.getHeight() / 2f);
//        //动画集
//        AnimationSet set = new AnimationSet(true);
//        set.addAnimation(translateAnimation);
//        set.addAnimation(alphaAnimation);
//        set.addAnimation(scaleAnimation);
//        //设置动画结束之后的状态是否是动画的最终状态，true，表示是保持动画结束时的最终状态
//        set.setFillAfter(true);
//        set.setFillEnabled(true);//使其可以填充效果从而不回到原地
//        //设置动画时间 (作用到每个动画)
//        set.setDuration(6000);
//        itemView.startAnimation(set);

translateAnimation.setAnimationListener(
                new Animation.AnimationListener() {
                    @Override
                    public void onAnimationStart(Animation animation) {//开始时
 
                    }
 
                    @Override
                    public void onAnimationEnd(Animation animation) {//结束时
 
                    }
 
                    @Override
                    public void onAnimationRepeat(Animation animation) {//进行时
 
                    }
                });

```
### 定点平移动画
``` stylus
 String xyStr = (String) imageView.getTag();
        String[] x_y = xyStr.split("，");
        float xEnd =Utils.dp2px(this, Integer.valueOf(x_y[0]))- Utils.dip2px(this, 40) / 2;
        float yEnd =  Utils.dp2px(this, Integer.valueOf(x_y[1]))- Utils.dip2px(this, 40) / 2;

        imageView.setX(Utils.getScreenWith(this) / 2 - Utils.dip2px(this, 80) / 2);
        imageView.setY(Utils.dp2px(this, 10) - Utils.dip2px(this, 80) / 2);
        FrameLayout.LayoutParams params = new FrameLayout.LayoutParams(Utils.dp2px(this, 80)
                , Utils.dp2px(this, 80));
        imageView.setLayoutParams(params);

        //移动
        ObjectAnimator translationXAnimator = ObjectAnimator.ofFloat(imageView, "translationX",
                xEnd);
        ObjectAnimator translationYAnimator = ObjectAnimator.ofFloat(imageView, "translationY",
                yEnd);

        //沿x轴放大
        ObjectAnimator scaleXAnimator = ObjectAnimator.ofFloat(imageView, "scaleX", 1f, 0.5f);
//沿y轴放大
        ObjectAnimator scaleYAnimator = ObjectAnimator.ofFloat(imageView, "scaleY", 1f, 0.5f);

        AnimatorSet set = new AnimatorSet();
        //同时沿X,Y轴放大，且改变透明度，然后移动
        set.play(translationXAnimator)
                .with(translationYAnimator)
                .after(scaleXAnimator).after(scaleYAnimator);
//都设置3s，也可以为每个单独设置
        set.setDuration(1000);
        set.start();
```


[原文：https://blog.csdn.net/qq_39056803/article/details/79375667 ](https://blog.csdn.net/qq_39056803/article/details/79375667 )

``` stylus
 //沿x轴放大
        ObjectAnimator scaleXAnimator = ObjectAnimator.ofFloat(itemView, "scaleX", 1f, 0.625f);
//沿y轴放大
        ObjectAnimator scaleYAnimator = ObjectAnimator.ofFloat(itemView, "scaleY", 1f, 0.625f);
//移动
        ObjectAnimator translationXAnimator = ObjectAnimator.ofFloat(itemView, "translationX",
                itemView.getX(), Utils.dp2px(this,220)-itemView.getX());
        ObjectAnimator translationYAnimator = ObjectAnimator.ofFloat(itemView, "translationY",
                itemView.getY(), Utils.dp2px(this,320)-itemView.getY());

//透明动画
        ObjectAnimator animator = ObjectAnimator.ofFloat(itemView, "alpha", 1f, 0.6f, 1f);
        AnimatorSet set = new AnimatorSet();
//同时沿X,Y轴放大，且改变透明度，然后移动
        set.play(scaleXAnimator)
                .with(scaleYAnimator)
                .with(animator)
                .before(translationXAnimator)
                .before(translationYAnimator);
//都设置3s，也可以为每个单独设置
        set.setDuration(800);
        set.start();
        
        //添加监听事件
                set.addListener(new Animator.AnimatorListener() {
                    @Override
                    public void onAnimationStart(Animator animation) {
                        //动画开始的时候调用
                    }
        
                    @Override
                    public void onAnimationEnd(Animator animation) {
                        //画结束的时候调用
                    }
        
                    @Override
                    public void onAnimationCancel(Animator animation) {
                        //动画被取消的时候调用
                    }
        
                    @Override
                    public void onAnimationRepeat(Animator animation) {
                        //动画重复执行的时候调用
        
                    }
                });
```

> 参考
[https://www.jianshu.com/p/d23f58f4368d](https://www.jianshu.com/p/d23f58f4368d)

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
        
        //支持javascript  
        web.getSettings().setJavaScriptEnabled(true);   
        // 设置可以支持缩放   
        web.getSettings().setSupportZoom(true);   
        // 设置出现缩放工具   
        web.getSettings().setBuiltInZoomControls(true);  
        //扩大比例的缩放  
        web.getSettings().setUseWideViewPort(true);  
        //自适应屏幕  
        web.getSettings().setLayoutAlgorithm(LayoutAlgorithm.SINGLE_COLUMN);  
        web.getSettings().setLoadWithOverviewMode(true); 
        
        原文：https://blog.csdn.net/zrbcsdn/article/details/76077387 

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

> chromium: [INFO:CONSOLE(1)] "Uncaught ReferenceError: 张 is not defined

类似情况
``` stylus
[INFO:CONSOLE(1)] “Uncaught ReferenceError: getData is not defined”, source: (1) 
[INFO:CONSOLE(1)] “Uncaught ReferenceError: myData is not defined”, source: (1)
原文：https://blog.csdn.net/Xiong_IT/article/details/52703941 
```
原因是，当Webview调用js方法传递参数时，如果参数类型为数字时,这里的数字不一定是int型，也指string型数字，比如“12345”，毕竟js中是没有类型区分的。 
大写的但是BUT：如果你传递不是数字，而是普通字符串时，就要注意了，会报上述的错误，传递的String值没有定义。 
解决方法：修改上述错误那行代码，在传递的数据两边加上单引号包裹字符串即可，大家可以在浏览器F12的console调试台试试调用js方法，传递非数字参数时，必须使用’data’这类形式方可正确调用，不然控制台也报上述错误。比如要在控制台调用:getData(myData)，会报错，但是如果调用:getData(‘myData’)是没问题的。
原文：https://blog.csdn.net/Xiong_IT/article/details/52703941 
**解决**
``` stylus
...
mWeb.loadUrl("javascript:getData('" + data  + "')");// 注意data两边各多了一个单引号。
...
```





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