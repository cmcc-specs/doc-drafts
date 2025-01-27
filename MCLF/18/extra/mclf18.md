https://github.com/MCLF-CN/docs/issues/18
于 2025/1/27 的存档
---
### 检查项

- [x] 我充分理解提交的建议可能无法所有启动器作者参与，并尊重所有启动器开发者的选择
- [x] 我确认在Issues列表中并无其他人已经提出过与此问题相同或相似的问题
- [x] 我确认该反馈并非针对单个启动器的，如果是，我将会去该启动器的反馈页面反馈

### 您是什么类型的用户

第三方网站管理/负责人（MC相关的）

### 请简单的说一下您的想法

Yggdrasil Connect 是基于 OpenID Connect 协议的全新用户身份认证协议，为 authlib-injector 外置登录提供了一种基于 OAuth 2.0 和 OpenID Connect 的用户身份认证解决方案，目的是取代 Yggdrasil API 中的 Auth Server 部分。

目前 LittleSkin 已实现支持 OAuth 2.0 设备代码流的 Yggdrasil Connect 服务端。

### 它能解决什么样的问题/带来什么样的帮助

在 Yggdrasil API 的 Auth Server 部分中，用户需要将自己的用户名和密码直接暴露给第三方应用，才能通过第三方应用访问 Yggdrasil API，这增加了用户账户关键信息泄露的风险；且该部分的 API 在设计上几乎没有考虑到二步验证，无法良好地保障用户账户的安全。并且，由于各个第三方应用在该部分 API 的实现存在差异，用户在不同应用之间的登录体验存在较大割裂，时常出现应用实现不完整导致用户无法正常登录、用户体验低下的问题（例如 Hex-Dragon/PCL2#3519、Xcube-Studio/Natsurainko.FluentLauncher#281）。

Yggdrasil Connect 的目的即是解决这些问题。通过 OAuth 2.0 和 OpenID Connect 协议，Yggdrasil Connect 可以实现用户在不同应用间的登录体验的统一，同时方便各验证服务器自行设计用户身份认证方式，以保障用户账户的安全。

### 期望的结果

启动器需要实现一个 OpenID Connect 客户端（可由 OAuth 2.0 客户端扩展而来），允许用户通过 OAuth 2.0 登录 authlib-injector 外置登录账号，就像登录微软正版账号一样。

大致流程：通过 OAuth 2.0 请求授权 -> 解码 ID Token / 请求 UserInfo Endpoint 拿角色信息（不需要再处理角色选择！）-> 把 OAuth 的 Access Token 直接传进游戏里

Yggdrasil Connect 的登录流程相较微软正版登录的流程要简单很多，而且 OAuth 2.0 客户端部分的大部分代码应该都可以复用。

### 是否有对这个方案的相关链接？

Yggdrasil Connect 规范（公开评审版本）：yushijinhun/authlib-injector#268

该规范包含服务端规范和客户端规范，目前仍为公开评审版本，但应该不会有比较大的变更。欢迎各位就公开评审版本提出评审意见或建议。

启动器作者如果觉得完整的规范太长，想要个《启动器要怎么做才能实现 Yggdrasil Connect 客户端》，可以先看完整规范的「服务发现」章节、「授权流程」章节和「用户信息获取」章节，可以结合 LittleSkin 的 OAuth 2.0 设备代码流文档一起看：https://manual.littlesk.in/advanced/oauth2/device-authorization-grant

### 附注

HMCL 有一个 PR 针对 LittleSkin 实现了 Yggdrasil Connect 客户端：HMCL-dev/HMCL#3491，各位可以前往 Actions 中下载编译好的版本来体验：https://github.com/HMCL-dev/HMCL/actions/runs/12237584465

![Image](https://github.com/user-attachments/assets/5766ff08-e840-4167-9e3e-b4586a5f2ef2)