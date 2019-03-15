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


欢迎使用 **{小书匠}(xiaoshujiang)编辑器**，您可以通过==设置==里的修改模板来改变新建文章的内容。