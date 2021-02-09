[![Powered by Wechaty](https://img.shields.io/badge/Powered%20By-Wechaty-brightgreen.svg)](https://wechaty.js.org)

# wechat-operation-assistant
一个使用小微商户+微信聊天机器人构建的可付费私域运营助手

一直以来在私域流量运营领域都有这样一个需求：自动通过好友，并在新好友支付一定的费用之后，依据新好友所发送的关键字，将其拉到对应的微信群。关键字与微信群对应，并且微信群满员以后可以自动扩建。

有人想过这样的解决方法，先让潜在用户添加人工客服微信，转帐或扫码支付，人工验证之后，再拉TA入群。但是这个方法人工成本高，人工成本高，就意味着会拉高入群票价。

还有一个变通的方法，采用微商城，让用户在商城内自助完成支付，然后通过钩子设置发给用户一个四位数字的验证码，就是虚拟发货。完成这一步后，再引导用户拿着验证码添加机器人助手微信，机器人助手收到验证码以后，先到数据库里验证订单真伪，核实后再拉人入群。

这个方案看起来相当美好了，但是仍然有很大问题。一句话概括，就是太复杂。需要数据库，需要微商城等，部署成本高了自然也会推高入群票价。有人可能还会想到，可以使用知识星球或类似产品，这个产品确实很棒，但有时候我们就只想在微信中聚集私域流量，怎么办呢？

能否有这样一个简单的方案：机器人助手自动通过好友后，依据新好友发送的关键字，自主判断是否需要付费，如果需要，发给新好友一个支付二维码，待新好友完成扫码支付后，自动将TA拉入微信群。整个过程没有第三方跳转，完全在微信窗口内完成。还有，整个方案不涉及Web服务、数据库服务等，只需要部署一个微信机器人就可以了。

答案是可以的，于是作者写了这个开源项目。我给它取名为：一个使用小微商户+微信聊天机器人构建的可付费私域运营助手。

这是一个实验性的小项目，还不完善，但可行性是具备的，完全可运行，收到的款项也会自动转到个人微信卡。希望这个项目能给你启发，但不提供任何技术保证和使用许诺。

该项目基于微信小微商户+Wechaty实现，并借鉴于Wechaty的示例代码（https://github.com/wechaty/wechaty-getting-started）。

接下来介绍一下它需要准备什么，如何使用，未尾有作者录制的视频，方便你快速查看项目的交互效果。

## 主要功能

主要支持的功能交互指令：

1. 申请加入xx群，可以加入群，将xx换成具体的关键字，例如书法
2. #查询2021xxx，用于查询旧订单，如果支付了可以补拉进群
3. 指定的管理员，可以使用”@xxx 勿发“这样的群消息指令，让机器人踢出某人

## 使用准备

在使用之前需要Wechaty的token和小微商户的MCHID和SECRET。前者可在 https://qiwei.juzibot.com/corpPremium/wechaty 购买，是月租付费形式，更稿时每月200。后者在 https://pay.xunhuweb.com/ 申请，一次性付费。

拿到启动材料后，需要在本地bash中配置一下系统变量：

```
export WEPAY_MCHID=xxx
export WEPAY_SECRET=xxx
export WECHATY_PUPPET_HOSTIE_TOKEN=xxx
```
这是Linux/Mac下的配置，在Windows下需要自行修改一下配置方法。

## 如何启动

启动简单：

```
git clone https://github.com/rixingyike/wechat-operation-assistant.git --depth=1
cd wechat-operation-assistant
npm i
npm run serve
```

## 投石问路版本

v1.0：https://github.com/rixingyike/wechat-operation-assistant/releases/tag/v1.0

当然了这个版本还存在一些问题，例如机器人助手依据昵称管理员权限，这存在漏洞。Wechaty中Contact对象有一个alias方法，可以设置/获取联系人备注，可以使用这个方法代替name检验管理员权限。

后续作者可能对这个项目进行不断完善，如果你有什么建议，欢迎提出来，也欢迎提交PR。

## 使用视频

作者为这个版本的使用录了一个视频：https://mp.weixin.qq.com/s/TUKmK7IgJElECt7hNq5QEA

这里还有一个Youbute版本：https://youtu.be/Rujwzt0B9K8

有问题请关注微信公众号“程序员LIYI”联系作者。

![](https://yishulun.com/post-images/1610260345230.jpg)