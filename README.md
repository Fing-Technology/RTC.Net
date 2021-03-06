# RTC.Net SDK V1.2 
###Update:2016-11-24 17:49
用于操作实时猫（`RealTimeCat`）服务端API，官方网站：https://shishimao.com/
<hr \>
专注于WebRTC技术的实时音视频云服务平台<br \>
实时猫提供 以视频通讯功能为核心的系统开发解决方案，简化和增强WebRTC开发的公有云平台，以及行业领先的WebRTC私有云服务<br \>
实时猫是专注于WebRTC技术的实时云视频技术服务商，致力于为企业提供专业的实时通讯技术云和端服务，使语音视频开发更加稳定、快速、简易、可定制。<br \>
专业、高水平、执行力强的技术团队为客户的业务快速发展可靠的核心技术产品,实时猫的愿景是让实时音视频通讯开发触手可得。<br \>
此SDK基于.Net 4.0环境开发

v4.0增加RtcProject类及接口对应的方法

#SDK开发示例

##简单配置
请使用Nuget或其他工具安装`Microsoft.Net.Http`和`Newtonsoft.Json`包及引用<br \>
Nuget包已经发布，欢迎使用！<br \>
<code>
PM>Install-Package RTC.Net
</code>

```c#
using RTC.Net;
//项目相关参数
Config.ApiKey = "d1383590-7f1b-4242-86ee-*******";
Config.ApiSecret = "579d679f-84b8-4125-bc34-********";
```
##会话操作
```C#
获取会话列表
var res1 = RTCSession.GetSessions(1,25,30);
建立一个会话
var res2 = RTCSession.CreateSession(new CreateSessionParameter()
{
    label = "testtestes111",
    data = "",
    live_days = 4,
    permanent = false,
    type = SessionType.P2P
});
获取永久会话
var res3 = RTCSession.GetSessionsPermanent();
获取临时会话
var res4 = RTCSession.GetSessionsNoPermanent();
获取一个会话
var res5 = RTCSession.GetSession("c8a8559d-5552-4fbd-****-ddce83ab0f76");
修改一个会话
SessionResult sr = res5.Body;
sr.label = "a123458T";
sr.live_days = 2;
var res6 = RTCSession.UpdateSession(sr.ToParamter());
删除一个会话
var res7 = RTCSession.DeleteSession(sr.uuid.ToString());
```
##令牌操作
```c#
//获取session_id下令牌列表
var res8 = RTCToken.GetTokens("80588ca1-b81f-****-ad0d-6d7b7543101f");
//获取session_id下临时令牌列表
var res9 = RTCToken.GetSessionsNoPermanent("80588ca1-b81f-****-ad0d-6d7b7543101f");
//获取session_id下永久令牌列表
var res10 = RTCToken.GetSessionsPermanent("80588ca1-b81f-****-ad0d-6d7b7543101f");
//创建一个session_id下的令牌
var res12 = RTCToken.CreateToken(new CreateTokenParameter()
{
    label = "Token23",
    live_days = 1,
    session_id = "80588ca1-b81f-****-ad0d-6d7b7543101f",
    type = TokenType.PUB
});
//获取一个令牌
var res11 = RTCToken.GetToken("8604b20d-9e24-4804-ad87-c8230390c7ba");
//修改一个令牌
TokenResult tr = res11.Body;
tr.label = "xxxxxxTxxxxxxx";
var res13 = RTCToken.UpdateToken(tr.ToParamter());
//删除一个令牌
var res14 = RTCToken.DeleteToken("8604b20d-9e24-4804-ad87-c8230390c7ba");
```

#关于错误返回
1.请求返回异常的代码统一为`408`<br \>
2.错误详情<br \>
如：var res1 =RTCSession.GetSessions();<br \>
错误详情为`res1.ReasonPhrase`<br \>
判断一个请求是否成功，可以通过`res1.IsSuccessStatusCode`来判断。<br \>
想定位到准确的错误返回码，可以检查`res1.Code`<br \>

#changelog
##1.2
1.升级至0.4版接口
2.增加 Project类接口

##1.1.5
1.服务端API接口增加分页功能

##1.1.0
1.类型、方式等常量采用枚举类型；<br \>
2.增加几个类的扩展方法以优化代码结构；<br \>
3.采用反射方法增强对象转换代码效率；<br \>
4.修复一些比较隐蔽的BUG；<br \>

##1.0.2
1.优化错误显示；<br \>
2.增加Http请求超时设置参数<br \>

##1.0 
1.基础版本上传,主要操作会话和令牌;<br \>
2.录像接口待服务端API完善后再添加！
