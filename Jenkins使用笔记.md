# Jenkins使用笔记

## 运行命令（war）

    java -jar jenkins.war

## 邮件通知格式

163邮箱通知设置

https://blog.csdn.net/yamingwu/article/details/44142635

```
Jenkins构建通知:$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!
```

```
<hr/>

(本邮件是程序自动下发的，请勿回复！)<br/><hr/>

项目名称：$PROJECT_NAME<br/><hr/>

构建编号：$BUILD_NUMBER<br/><hr/>

构建状态：$BUILD_STATUS<br/><hr/>

扫描二维码 
<img src="http://192.168.31.10:8000/unknow_file.png" height="200px" width="200px"/><br/><hr/>

触发原因：${CAUSE}<br/><hr/>

构建日志地址：<a href="${BUILD_URL}console">${BUILD_URL}console</a><br/><hr/>

构建地址：<a href="$BUILD_URL">$BUILD_URL</a><br/><hr/>

变更集:${JELLY_SCRIPT,template="html"}<br/><hr/>
```

## 参考
https://blog.csdn.net/u013066244/article/details/78665075