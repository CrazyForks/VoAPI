[![./images/head.png](./images/head.png)](https://demo.voapi.top)

**🎉VoAPI全新架构V1.0已全量发布**
## 介绍
全新的高颜值、高性能、高扩展的AI模型接口管理与分发系统

|功能|社区版|Pro版|
|-|-|-|
|基础功能|✅|✅|
|用户名、邮箱注册/登录|✅|✅|
|多用户管理|✅|✅|
|规则引擎支持（ES5/ES6规范的JS语法引擎自定义规则）|✅|✅|
|API数据转发核心模块|✅|✅|
|API令牌|✅|✅|
|多余额机制|✅|✅|
|多货币机制（内置两种，Pro支持自定义）|✅|✅|
|每日签到|✅|✅|
|多用户等级（内置5层等级）|✅|✅|
|用户实时RPM、TPM支持|✅|✅|
|渠道实时RPM、TPM支持|✅|✅|
|渠道单密钥实时RPM、TPM支持|✅|✅|
|训练场自定义多外部页面嵌入|✅|✅|
|远程模型、厂商数据同步|✅|✅|
|渠道分组支持|✅|✅|
|渠道分组固定倍率、定时倍率支持|✅|✅|
|渠道重试|✅|✅|
|渠道密钥错误禁用（可禁用单密钥、或密钥中本次请求的模型）|✅|✅|
|渠道密钥错误禁用自动恢复机制|✅|✅|
|渠道请求熔断超时机制|✅|✅|
|渠道IP、UA规则限制|✅|✅|
|渠道全局/独立代理配置，支持HTTP[S]、Socket5协议|✅|✅|
|兑换码系统|✅|✅|
|自定义菜单|✅|✅|
|第三方登录（Github、Gitee、LiunxDO）|✅|✅|
|安全过滤|✅|✅|
|API线路展示与测速|✅|✅|
|API节点状态监控展示|✅|✅|
|自定义SEO、主题色调与全局样式、脚本等|✅|✅|
|一键第三方系统数据迁移导入|✅|✅|
|多优先级计费方式|✅|✅|
|日志分表（可按照天/周/月/年四个维度进行自动分表）|✅|✅|
|i18n国际化（已内置中文、英文）|✅|✅|
|模型多条件计费（阶梯计费）支持，且可按照固定价格和基础倍率两种模式计费|✅|✅|
|Pro专属功能，暂不公布|❌|✅|
|实际功能不止上述描述，快去体验体验吧～|✅|✅|

## 部署
### 架构镜像
- Linux amd64: `voapi/voapi`
- Linux arm64: `voapi/voapi-linux-arm64`

### Docker Compose部署
> linux-arm64用户请将docker-compose.yml中的镜像替换为`voapi/voapi-linux-arm64`
```sh 
git clone https://github.com/VoAPI/VoAPI.git
cd VoAPI
docker-compose up -d
```
部署完成后，访问 http://localhost:6800 （请根据实际情况修改域名和端口号）即可进入系统，注册第一个用户即为管理员账号

### Docker 单容器部署
> 请确保您已经准备好了MySQL和Redis数据库，并且正确配置了config.yml文件

> linux-arm64用户请将镜像替换为`voapi/voapi-linux-arm64`
```sh
docker run -d --name voapi --restart always -p 6800:6800 -e TZ=Asia/Shanghai -v ./config.yml:/config.yml -v ./file:/file -v ./public:/public voapi/voapi:latest
```

## 配置文件
- config.yml
```yaml
app:
  port: 6800 # 应用监听端口
mysql:
  dsn: root:@tcp(db-voapi:3306)/voapi # 主数据据库
  log-dsn: root:@tcp(db-voapi:3306)/voapi-log # 日志分离数据库
  log-body-dsn: root:@tcp(db-voapi:3306)/voapi-body-log # 请求体日志分离数据库
  log-sharding: # 日志分表方式，支持 day/week/month/year 四种方式
    enable: false
    mode: y # d = day, w = week, m = month, y = year
redis:
  dsn: redis://redis-voapi:6379/0
  pool-size: 0 #redis连接池大小，等于0时使用默认值，默认值为CPU数量*100
```

## 后台快速配置第一个渠道
- 注册的第一个用户即为管理员账号，登录后点击右上角紫色的齿轮图标进入后台管理界面
- 先到「模型供应商」模块下的「模型列表」、「供应商列表」中点击远程同步，同步官方预置的模型和供应商
- 然后到「模型供应商」模块下的「规则引擎」新建一个空白规则引擎，名称随意，非必填内容无需填写，则为完全透传
- 然后就可以去「渠道管理」-「渠道分组」中新建一个渠道分组
- 最后就可以在「渠道管理」-「渠道列表」中新建一个渠道了，选择刚才新建的规则引擎和渠道分组即可

## AI客户端推荐
> [!NOTE]
> 🌻 GoAmzAI支持众多强大的功能：
> - 最低1C1G的服务器就能流畅运行
> - 宝塔极速可视化部署、配置简单易懂
> - 站点完全自适应支持PC、平板、手机
> - 低内存占用，Golang开发原生高并发支持
> - 包含AI对话、AI绘画、AI音乐、AI视频、AI生成PPT、PDF解析对话、AI应用支持等众多AI模块
> - 具有非常完善的运营机制，包括但不限于套餐系统、兑换码系统、邀请奖励、签到福利、推广返利等等
> - [🫱 点我立即了解及体验](https://d.goamzai.com)

## 加群交流
> 您也可以扫描下方二维码加入QQ交流群以获取最新的开发动态和相关事件
> 
> 点击链接加入群聊：https://qm.qq.com/q/QFibUxMPEQ

<img width="235" alt="image" src="https://github.com/user-attachments/assets/d4798bae-03e5-4fce-aa03-e6dadd9ac748">

## 界面截图
### PC端
![](./images/1.png)
![](./images/2.png)
![](./images/3.png)
![](./images/4.png)
![](./images/5.png)
![](./images/6.png)
![](./images/7.png)
![](./images/8.png)
![](./images/9.png)
![](./images/10.png)
![](./images/11.png)