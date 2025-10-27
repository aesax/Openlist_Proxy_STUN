# 🚀 Openlist Proxy STUN：内网加速下载神器 🚀

是不是受够了没有公网使用Cloudflare的慢速下载🤔?或者是国内CDN的高昂流量费用? 或者被百度网盘这些“顽固”资源限制UA搞得头疼？别担心，`Openlist Proxy STUN` 就是你的救星！它能让你的内网服务器“破墙而出”，实现高速下载！

## 🤷‍♂️ 我为什么需要它？

*   **服务器带宽像“小水管”** 🚰，下载大文件慢到怀疑人生。
*   遇到一些“傲娇”资源（比如**百度网盘大于20M的文件**），无法简单重定向，需要特殊“通行证”（UA）。
*   **本地文件下载速度堪忧**，急需一条“高速公路”🛣️。

## 🛠️ 准备工作：组装你的神器

你需要准备一套“三件套”，并把它们安装在同一台服务器上：

1.  **🏠 一台内网服务器**：它必须支持 **STUN** 协议（这是打洞穿墙的关键！）。
2.  **📦 核心软件三件套**：
    *   `Openlist` (资源列表大脑)
    *   `Openlist-Proxy` (代理加速核心)
    *   `lucky` (网络穿透大师)

## 🚀 部署与配置：四步搞定！

### 步骤 1: 为你的Openlist开一扇“大门” 🚪

首先，得让外面的人能访问到你的Openlist服务。可以通过 **Cloudflared**、**FRP** 或 **CDN** 来实现。

*   **例如**：将 `cloudflare` 的流量引导到你的服务器 `YourServer:5244`。
*   **最终效果**：获得一个公网域名，比如 `demo.com`。

### 步骤 2: 启动核心加速引擎 🔥

启动 **Openlist-Proxy**，并做好关键配置：
*   `token`：设置一个好记又安全的密码。
*   `openlist_address`：填上 `localhost` (因为就在本机)。

### 步骤 3: 施展“网络穿透大法” ⚡

用 **Lucky** 进行STUN打洞，这是整个方案最魔法的一步！

*   设置 **STUN** 服务，把 `Openlist-Proxy` 的端口“打穿”到公网。
*   配置 **WebSocket** 通信，保持内外网信息实时同步。
*   设置 **DDNS**，绑定一个域名（比如 `down.demo.com`），这样就能通过固定地址找到你动态变化的公网IP了。
*   **💡 超级重要提示**：在Lucky获取公网IP时，记得选择 **“接口”** 而不是“网卡”！这是成功的关键！

### 步骤 4: 施展“移形换影”魔法 ✨

最后，在 **Openlist** 里配置一段神奇的JavaScript脚本：

*   这段脚本会自动把慢吞吞的下载地址，“偷梁换柱”成我们刚刚搭建好的高速通道 `down.demo.com:PORT`！
*   你只需要根据说明，替换脚本里的域名和端口参数即可。

---

**🎉 恭喜！** 全部设置完成后，你的下载速度就会像坐上了火箭一样飞速提升！再也不用看那些“傲娇”资源的脸色啦！


原文:
```
这是什么业务

当你的Openlist 服务器受限于带宽太低 并且一些资源无法通过302重定向下载 例如百度网盘 大于20M 则需要设置UA，本地文件下载速度慢的问题

准备条件：
一台内网服务器 并且支持 STUN 
软件 Openlist + Openlist-Proxy + lucky 部署在同一机器上
Openlist Web 通过 Cloudflared 或者 FRP 或者CDN 绑定好 
例如 cloudflare SERVER > YourServer:PORT5244 （这个解决方案很多 不多阐述）例 demo.com
启动 Openlist-Proxy 设置好 token openlist_address(localhost)
lucky 设置STUN 打洞 Openlist-proxy端口 配置好websocket通信 将及时信息传递到websocket服务器，并设置DDNS绑定你的域名（获取公网IP方式选择接口 而不是网卡！）假设绑定的域名为 down.demo.com

在openlist 配置好Javascript（替换 STUN打洞的端口）该项目已经开发 
替换js内的参数实现 替换down.demo.com:PORT 达到下载效果

```
