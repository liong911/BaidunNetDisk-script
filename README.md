
![image.png](https://note.youdao.com/yws/public/resource/7118a972bf860164e6674f7b167271ae/WEBRESOURCE98a421a7955663862f67696fde34aabf)

> 掘金用法:
[导出新版本百度网盘文件库目录——篡改猴脚本](https://juejin.cn/spost/7300876243953025075)

# 0 更新日志

## 2024.1.20

1.增加Excel导出模式

# 1 背景

当前版本适用于新的百度网盘进行目录导出。
脚本基于[【Avens666/BaidunNetDisk-script】](https://github.com/Avens666/BaidunNetDisk-script)，虽然已经全改，但还是拉一个fork分支表示尊敬，【Avens666/BaidunNetDisk-script】当前已不适用于新版本的百度网盘页面，所以干脆重写了。

github地址:
<https://github.com/dirty-damn/BaidunNetDisk-script>

***

# 2 作用

> 当你找到这个插件的时候，你已经知道它是做什么用的了，也知道为什么要用这个了...

虽然自己的网盘，有导出目录的工具，但是很多用户间分享的网盘数据，动辄10T 20T，不可能都转存到自己的网盘中。而且转存也有文件数量限制等。
现在买网盘资源，基本都是这种分享方式，而不是卖账号。
因此，分享的网盘资源，里面到底有些什么内容，其实很不方便查看

搜索了一圈，没有现成的方案，大家都在关注如何加速下载等，github上虽然百度网盘相关项目有近百个，但是没有专门导出目录信息的项目。 而且主要都还是针对自己的网盘文件，这种在群中分享的网盘资源，没有现成的访问方法。
没办法，大佬们不关注这个需求，只能自己动手了。
在参考了github中的相关项目，比较了多种技术手段（python脚本，java程序，go语言，油猴脚本）后，本人使用油猴脚本方式来实现这个功能。
功能设计： 导出分享文件库的所有目录和文件内容清单，同时对文件夹内的文件数量和尺寸进行递归统计。

针对百度网盘的油猴脚本，可导出百度网盘共享文件库目录清单
chrome浏览器+油猴脚本测试通过
油猴脚本怎么用我就不写了，请自行百度。

# 3 插件使用说明

## 3.1 安装插件

<https://greasyfork.org/zh-CN/scripts/479817-百度网盘文件库目录导出>

## 3.2 导出方法

1.进入百度网盘

1.  点击【消息】
2.  按下f12，选中【Console】，便于观察导出的日志和进度

![image.png](https://note.youdao.com/yws/public/resource/7118a972bf860164e6674f7b167271ae/WEBRESOURCE7619d57f533d1fc280bb12b75a41eb54)

2.选择资源

1.  选择一个共享群
2.  点击右上角的【文件库】(切记一定要从右上角打开文件库)
3.  然后点击进入一个目录
4.  控制台出现准备就绪字样，就可以进行下一步操作

![image.png](https://note.youdao.com/yws/public/resource/7118a972bf860164e6674f7b167271ae/WEBRESOURCE5e0735a913a12f529131c66ece8fdbd0)

3.导出资源目录

1.  勾选需要导出的目录
2.  出现导出按钮，点击导出
3.  控制台出现导出进度

![image.png](https://note.youdao.com/yws/public/resource/7118a972bf860164e6674f7b167271ae/WEBRESOURCEa6c9e7718f5f6137b992a87b7c865d55)

4.导出完成后，将目录自动下载到浏览器配置的下载路径。

# 4 导出的目录格式

例如：

```txt
总耗时：15816ms
共导出资源数：1588
共计资源大小：81.89GB = 83857.63MB

人月神话.ppt, /xxxxxx/xxxxxx/xxxxxx/人月神话.ppt, 1.53, 836611238345266
...
```

格式为：

    资源名称, 路径, 大小MB，网盘资源的fs_id

如需其他序列化格式，可自行修改脚本。

# 5 使用建议

由于文件库目录可能较为庞大，导出过程采用递归遍历的方式，可能会花费较大的时间，而插件在执行过程中只会有一个线程在跑，所以最好的做法就是，**开启多个浏览器页签**，分多个目录进行导出，实现并行过程。

# 6 性能

这是我在一次导出过程中截的图，导出3.7w的资源数，花费716秒，将近12分钟的样子，这很大程度上取决于文件目录的深度和目录数量，以及你网络带宽和cpu性能。

![image.png](https://note.youdao.com/yws/public/resource/7118a972bf860164e6674f7b167271ae/WEBRESOURCEc53b219a5a66f6c5d3d6d29ede76ad2c)

