
![](https://img2024.cnblogs.com/blog/3038670/202501/3038670-20250104031540172-1161563949.jpg)


 峰哥镇楼\~\~\~!!




---


 **之前写过一个博客，介绍 ob\_tools包 来实施抓取 observer 层的 gv$ob\_sql\_audit 的SQL，还提供一些分析SQL来通过不同维度分析缓慢的业务SQL语句，免得和应用扯皮说数据库执行SQL慢。**


**但是分析出服务端业务SQL语句执行时间还不够，应用也有可能会和你扯皮说obproxy转发慢，也不是不能查obproxy的日志来佐证，就日志里面的内容很难看，我经常懒得去看很烦，所以搞了个 format\_obproxy\_digest\_log 工具来看proxy的转发耗时。**


**这样一来proxy(网络层)、server(服务端层) 有了一套完整分析业务SQL语句请求耗时的解决方案，妈妈再也不怕我和开发扯皮了，狠狠地给我怼死开发。🤞🤞🤞**


**\*\*\*\*\*\*注意**\*\*\*\*\*\***：这个工具只能用来分析 obproxy obproxy\_digest.log ，我是基于obproxy 433版本的**obproxy\_digest.log日志格式**写的工具，4\.X的obproxy应该能用，以后的版本不敢保证。**


 


**先介绍下obproxy obproxy\_digest.log 日志**


　　obproxy\_digest.log 是 OceanBase 数据库代理（OBProxy）的审计日志文件，主要用于记录执行时间超过指定阈值的 SQL 请求以及错误响应的请求。


1. 记录慢查询和错误请求：


	* 慢查询：当 SQL 请求的执行时间超过 `query_digest_time_threshold` 参数设置的阈值时，该请求会被记录到 `obproxy_digest.log` 中。默认情况下，该阈值为 100 毫秒（在主站环境中默认值为 2 毫秒）。
	* 错误请求：所有执行错误的请求（包括 OBProxy 自身错误和 OBServer 返回的错误）也会被记录到该日志中。
2. 日志内容：


	* 日志中包含了请求的详细信息，如日志打印时间、应用名、TraceId、RpcId、物理库信息（cluster:tenant:database）、数据库类型（OB 或 RDS）、逻辑表名、物理表名、SQL 命令、SQL 类型（CRUD）、执行结果（success 或 failed）、错误码、SQL 执行总耗时、预执行时间、链接建立时间、数据库执行时间等。


　　ob官网链接：[obproxy\_digest.log\-V4\.3\.3\-OceanBase 数据库代理文档\-分布式数据库使用文档](https://github.com)


 


**看完上面介绍的同学就知道 obproxy\_digest.log 日志里面的内容有多难看了，神烦，就直接开始介绍 format\_obproxy\_digest\_log 工具。**


**文件下载：**


通过网盘分享的文件：format\_obproxy\_digest\_log链接: https://pan.baidu.com/s/14QvqWyV83yn3xhO\_PGqqOQ?pwd\=j9j4 提取码: j9j4 \-\-来自百度网盘超级会员v9的分享


如果分享地址失效了，可以邮箱联系我发给你：842107948@qq.com



**下载到**format\_obproxy\_digest\_log**文件后上传到Linux服务器，先赋个权限：**




```
chmod +x format_obproxy_digest_log
```


![](https://img2024.cnblogs.com/blog/3038670/202501/3038670-20250104023600912-111512134.png)


 


 **如果不知道这玩意整么用可以执行一下命令：**




```
./format_obproxy_digest_log
```


![](https://img2024.cnblogs.com/blog/3038670/202501/3038670-20250104024154061-1100617874.jpg)


 


**使用方式很简单，最后演示下这个输出的日志：**


![](https://img2024.cnblogs.com/blog/3038670/202501/3038670-20250104024641964-1085470420.png)


![](https://img2024.cnblogs.com/blog/3038670/202501/3038670-20250104025010839-1135009291.png)


 


**最后想说一下，虽然我文章开头吐槽了一下**OB**，但是吐槽的是OB的日志格式内容不好看，用过**OB**的人都知道，无论是observer还是obproxy，那日志内容恶心得一批。**


**之前我玩其他数据库出了问题经常看日志，但是自从搞了**OB**以后，我养成了不看日志的习惯。😂😂😂😂**


**无可否认，在当前的国产信创数据库产品中，无论从架构设计、易用性、性能、兼容性，公司研发实力，还是配套生态等方面来看，就目前在我心目中来说，**OceanBase**是当之无愧的国产第一数据库（发自内心的真心话！！！！）**


**诸多因素后面决定不在OB干了，还是希望公司的发展能越来越好，产品能越来越完善。**


 \_\_EOF\_\_

       - **本文作者：** [小至尖尖SQL优化空间](https://github.com)
 - **本文链接：** [https://github.com/yuzhijian/p/18651324](https://github.com):[wgetcloud全球加速器服务](https://wgetcloud6.org)
 - **关于博主：** I am a good person!
 - **版权声明：** 本博客所有文章除特别声明外，均采用 [BY\-NC\-SA](https://github.com "BY-NC-SA") 许可协议。转载请注明出处！
 - **声援博主：** 如果您觉得文章对您有帮助，可以点击文章右下角**【[推荐](javascript:void(0);)】**一下。
     
