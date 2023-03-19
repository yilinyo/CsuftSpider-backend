# 🕷CSUFT SPIDER🕷

------

后端基于SpringBoot的中南林业科技大学教务系统爬虫💡

前端基于Ant Design Pro React🎨

前后端分离项目👑

**功能**：免校园网/VPN访问✈，成绩查询🙋‍♂️、成绩起伏变化分析📈、成绩统计✍、成绩单PDF导出📄、课表查询👀、考试信息查询📜...

**功能上新** 成绩更新通知📢、校历📆、教务通知🔊、知网入口📚、一键评教🕹

此仓库源码仅适用于CSUFT学子，其它学校仅供参考



### 服务端环境💻

配置能连接学校内网的centos系统服务器，配置教程可参考 [服务器连接校园网](https://blog.csdn.net/qq_51725966/article/details/127216999?spm=1001.2014.3001.5502)
~~现在我们学校已经提供了可以外网访问的webvpn入口，可以忽略给服务器配置内网，如果你的学校不支持，你仍然需要配置~~

2023-3-19 学校webVpn 自己过期了（应该欠费了），本项目恢复了之前的深信服VPN登录方式，并优化了登陆方式如果以后学校支持WebVpn会优先采用此登陆方式，若不支持则采用第二种（双重保障）

使用[jdk8](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html)环境最佳,已知jdk17测试存在问题

使用[NodeJs16.4](https://nodejs.org/en/)以上环境

### api配置🔊

验证码调用百度的api开放平台 [OCR](https://ai.baidu.com/ai-doc/OCR/)
~~自行获取AK,SK在 com/yilin/csuftspider/constant/ConstantData.java 中替换
密码解密前后端约定使用SM4加密，自行与前端约定在 com/yilin/csuftspider/constant/ConstantData.java 中设置密钥~~

接入bark 实现手机信息 推送服务状态，api配置抽离出来约定大于配置 在yml文件配置 ocr 密钥、bark 密钥、bark推送方式、系统默认是否开启sm4加密
```
#自定义配置
csuftspider:
#bark for ios
# https://bark.day.app/#/tutorial bark 推送到 IOS 当然你也可以不配置不会影响系统
    bark:
        title: CSUFTSPIDER #推送标题
        serverUrl: http://你的bark域名 #推送 bark url
        apiKey: 你的bark密钥 #apiKey
        level: active #推送显示方式active：默认值，系统会立即亮屏显示通知 timeSensitive：时效性通知，可在专注状态下显示通知。passive：仅将通知添加到通知列表，不会亮屏提醒。
        autoCopy: 1  #是否复制
        group: 开发通知  #分组名称
        icon: 你的bark推送图标 #推送图标默认url

# baidu api for ocr
#验证码图像识别 api https://ai.baidu.com/ai-doc/OCR/

baidu:
    ocr:
        baiduAk: 
        baiduSk: 

# 系统System Settings
system:
#系统登录
    login:
        method: 0 #0 默认开启 登录sm4加密（salt需要配置密钥）,1 不开启加密
        salt: 密钥 #SM4加密密钥 16位
```
### 客户端环境📱

进行了移动端适配

建议使用IE、Chrome、Safari浏览器



### 后端部署🛠

将仓库克隆到本地

```bash
git clone https://github.com/yilinyo/CsuftSpiderBackend.git
```

然后使用添加maven添加依赖，构建并打成jar包即可运行，默认在8082端口监听，如需修改请修改resource目录下yml文件💡



### 前端部署🛠

请查看此处部署[前端](https://github.com/yilinyo/CsuftSpiderFront)



**你需要注意前后端跨域问题，推荐使用Nginx反向代理**⏰



### 使用介绍🔊

以下功能移动端和PC端交替展示

1. 导航栏功能模块(PC端💻)

![image-20221008221342593](https://yilin-1307688338.cos.ap-nanjing.myqcloud.com/blog/image-20221008221342593.png)



<img src="https://yilin-1307688338.cos.ap-nanjing.myqcloud.com/blog/image-20221008220303617.png" alt="image-20221008220303617" style="zoom: 80%;" />

2. 成绩展示（移动端📱）和导出 (PC端💻)

![image-20221008220640866](https://yilin-1307688338.cos.ap-nanjing.myqcloud.com/blog/image-20221008220640866.png)

3. 成绩分析（移动端📱）

![image-20221008221004628](https://yilin-1307688338.cos.ap-nanjing.myqcloud.com/blog/image-20221008221004628.png)

4. 课表查看（移动端📱）

   ![image-20221008221559609](https://yilin-1307688338.cos.ap-nanjing.myqcloud.com/blog/image-20221008221559609.png)

5. 考试信息查看(PC端💻)

   ![image-20221008222346010](https://yilin-1307688338.cos.ap-nanjing.myqcloud.com/blog/image-20221008222346010.png)

 6. 成绩更新通知（移动端📱）

    ![](https://yilin-1307688338.cos.ap-nanjing.myqcloud.com/blog/20230316160853.png)

    7. 一键评教 （移动端📱）

       ![image-20230316161205606](https://yilin-1307688338.cos.ap-nanjing.myqcloud.com/blog/image-20230316161205606.png)

       

    

### 高级🧩

截止2023-3-16，官方项目用户人数5k+，未来考虑迁移小程序。如果你有其他想法，欢迎对源码进行修改
具体构建原理及过程可以看这篇文章 [CsuftSpider爬虫构建](https://blog.csdn.net/qq_51725966/article/details/127218540?spm=1001.2014.3001.5502)

二次开发注意登录本项目进行了加密，如不需要请自行在yml 配置。



### 免责声明🧱

本项目与学校官方无关，仅个人通过本项目加深网络爬虫、网络接口、开发设计理解应用，请勿用于违法犯罪或商务活动。




## Star ✨
[![Star History Chart](https://api.star-history.com/svg?repos=yilinyo/CsuftSpiderBackend&type=Date)](https://star-history.com/#yilinyo/CsuftSpiderBackend&Date)

