Apple TV Media Explorer
=====


1. 确保您的AppleTV固件版本是5.1 或 5.1.1（必须，支持幻灯片方式查看图片和TAB方式的呈现）。

2. 在设置中把区域改成香港（或者美国也行，但香港图标少点，看起来舒爽点），这样主页上你可以看到好些图标。
* MLB.TV：劫持到我们自己的本地媒体浏览器上，这是本次帖子的重点。
* WSJ Live：劫持到坚果在线。
* 预告片：劫持到TT的服务器。

3. 劫持DNS，有两种方法，请任选其一：
1).如果您的路由器支持DNSMasQ，可以在路由器上配置DNS劫持（192.168.1.9换成你的http服务器的ip地址）：

* address=/trailers.apple.com/180.153.225.136

* address=/www.marketwatch.com/192.168.1.9

* address=/lecurea.mlb.com/192.168.1.9

2).如果你不会弄DNS服务器，可以用我提供的，在AppleTV上设置DNS为117.41.182.103，这样的话http服务器地址必须是 192.168.1.9。

4. 搭建HTTP服务，确保 http://192.168.1.9 能访问（IP地址仅举例，自行替换）；HTTP弄好后，需要开启文件列表功能（dir listing），这样我们才能以让ATV把上面的媒体文件列出来播放。
1). Tomato 能用的lighttpd精简版可以从我这里自行提取：http://hdweb.googlecode.com/svn/ROUTER，已开启dir listing）
2). My Book Live 开启dir listing，参考TT的帖子：http://bbs.weiphone.com/read-htm-tid-5484774.html，其实可以改进一下，编辑 wdnas文件，里面var/www的-Indexes前面的减号去掉，全局都支持dir listing了，不用创建.htaccess文件了。
3). 其他NAS请自行想办法搭建http服务器。

5. 把附件下载下来，解压放到http服务器根目录下（注意是http://192.168.1.9/appletvv2，目录不要多了，也不要少了）。源代码在http://hdweb.googlecode.com/svn/ATV/上，需要尝鲜的可以去哪里随时看看有什么更新。

6. 修改里面的index.xml文件，指向把url指向你的媒体文件的http url（能列出你的媒体文件的），目前index.xml是TAB页面，有5个版面：照片、视频、音乐、下载、设置。如果你也正好用我的文件路径（比如/media/Pictures）那就不用改了。注意每个URL最后的“/”是必须的，不要省略。

7. 打开ATV，看看MLB.TV，把你的文件都列出来了。

0). 常规使用：视频、音乐直接点击播放，照片文件夹则以平铺方式呈现，支持幻灯片显示，非常完美。
1). 支持缩略图：如果有“文件或文件夹名称.thumb.jpg”（或“.thumb.文件或文件夹名称.jpg”）存在，则会自动用作缩略图。
2). 外挂SRT字幕：如果有“文件名.srt”存在（注意扩展名也需要，如“A.mp4.srt”），则会显示外挂字幕。
3). 支持连续播放：播放视频和音乐时如果按播放键（Play），完成后会自动播放下一个；如果按选择键（Select/Enter），则播放完成后不会自动播放下一个。
4). 显示简要信息：播放过程中按向上方向键两次，则会显示URL信息和播放列表剩余的项目数。（BTW：播放过程中按向下一次可以分段Seek，ATV内置的功能）。

 

更新历史：
  1.0  第一个实现版本。
  1.2  支持SRT外挂字幕和连续播放。
  1.3  支持文件夹优先显示；缩略图url不再要求前置。
  2.0 支持TT的MKV播放方案，支持自动生成缩略图（需要ffmpeg最新版，需要开启任意目录cgi支持，步骤稍复杂，教程后面再整理），代码在SVN上。


持续更新中，详细步骤和说明请移步看2楼的详细帖子。：http://bbs.weiphone.com/read-htm-tid-5460032.html

MKV方案请看TT的论坛：http://www.ottnt.com/forum.php
