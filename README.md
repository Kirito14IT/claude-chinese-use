# 写给中文用户的 Claude Code 上手和排错

简体中文 · [English](README.en.md)

我本来只是想用 Claude Code 改论文，找师兄一问，结果先卡在了 VPS 的 SSH 上。后来订阅能用了，又遇到了节点超时和账号验证。我把当时的过程按顺序捋了一遍，方便你对照自己卡在哪一步。[原始聊天记录](docs/chat.md)

## 先确认所在地区

截至 2026 年 11 月 20 日，中国大陆未列入 Anthropic 的支持地区。政策按用户实际所在地和组织资格判断，涵盖 Claude 网页版、Claude Code、API 及授权合作方提供的 Claude。网络配置和 Claude 账号是否可用是两件事。[Anthropic 支持地区政策](https://www.anthropic.com/legal/supported-regions)

## 从 VPS 到 Clash Verge

下面是为自己有权限使用的机器和网络配置代理时，可以依次检查的步骤。

### 1. 租一台 Linux VPS，先确认能登录

对话里用的是一台 1 GB 的 Ubuntu VPS。选机器时先确认套餐能装你熟悉的 Linux，服务商有网页控制台，方便 SSH 连不上时进去看日志。下单后，用服务商给的地址和 SSH 端口连接，凭据留在本地。先确认本地网络能连到 VPS 的入口、能进终端，再装面板。原始聊天里有当时看到的机房、套餐截图和推广链接。

聊天时看到的 DigitalVirt 洛杉矶 9929，入门档标的是 **39 元/月**。如果这档已经售罄，你又想马上买同一条线路，就得选还有库存的更高价档。下单时以页面上的价格和库存为准。[当时的套餐截图](docs/media/vps-plan.png)

我当时把 Codex 也装在了小 VPS 上，系统日志后来出现了 `Out of memory`。如果只是想让 AI 给安装建议，在自己的电脑上问就行，服务器只需要运行它要提供的服务。[当时的内存日志](docs/media/vps-memory-log.png)

### 2. 在 3x-ui 里复制订阅链接

1. 在有管理权限的 VPS 上按项目说明安装 3x-ui，登录面板，确认 Xray 正常运行。安装时显示的面板登录地址用于管理服务。
2. 在 3x-ui 的 **面板设置 → 订阅** 打开订阅服务。在已配置的入站连接里找到你为设备配置的客户端，复制面板为该客户端生成的订阅链接。面板提供 Clash 格式时，给 Clash Verge 选对应格式。
3. 确认本地电脑能访问订阅地址。订阅链接用于更新节点配置，里面可能包含访问凭据，和登录管理面板一样需要妥善保管。

[3x-ui 安装说明](https://github.com/MHSanaei/3x-ui/wiki/Installation) · [3x-ui 订阅说明](https://github.com/MHSanaei/3x-ui/wiki/Common-questions-and-problems#13-how-does-the-panel-subscription-link-work)

### 3. 导入 Clash Verge，再开系统代理

1. 打开 Clash Verge 的 **订阅** 页，粘贴自己的订阅地址并导入。导入后点选新配置，在 **代理** 页确认能看到预期的节点。
2. 切到 **规则** 模式，开启 **系统代理**。先用浏览器打开一个你本来就有权访问的站点，再到客户端的连接列表看请求实际走的是哪条规则。系统代理作用于读取该设置的应用。师兄在家用规则模式，在单位按网络要求让单个应用走专用端口。需要接管不读取系统代理的程序时，再看设备和网络是否允许使用 TUN。
3. 只有某个应用连不上时，再去看它自己的网络设置。对已获准的 HTTP(S) 代理，Claude Code CLI 可以在启动时读取 `HTTPS_PROXY` 或 `HTTP_PROXY`。桌面 Code 会话按官方文档配置。聊天里提到的桌面启动参数是当时的猜测。

[Clash Verge Rev 订阅导入](https://www.clashverge.dev/guide/profile.html) · [系统代理和 TUN](https://www.clashverge.dev/guide/quickstart.html) · [Claude Code 网络配置](https://code.claude.com/docs/en/network-config)

### 4. 掉线了，从最先失败的那一步查

| 看到的情况 | 先查哪里 |
| --- | --- |
| SSH 一直断，或远程扩展主机反复退出 | 用服务商的网页控制台进服务器。Ubuntu 上用 `free -h` 看内存，用 `sudo journalctl -k --since today` 查断线附近有没有 OOM 记录。 |
| SSH 能连，但订阅导入失败或列表是空的 | 核对面板订阅服务、对应客户端是否启用或到期、订阅链接的域名和证书，以及客户端是否能访问该地址。导入成功后再测节点。 |
| 订阅能更新，节点延迟显示 `timeout` | 查 VPS 在线状态、入口服务是否运行、防火墙和正确端口，再看服务商公告或提工单。聊天那次重启没有解决，工单回复说机房临时维护，之后连接恢复。 |
| 只有 Claude Code 报错，或者屏幕上出现 Portal | 先看服务状态，再核对登录账号、方案和客户端网络设置。明确要求验证时，从账号内的提示进入对应流程。 |

[那次掉线的工单截图](docs/media/vps-support-ticket.png) · [Claude 服务状态](https://status.claude.com/) · [桌面端排错](https://code.claude.com/docs/en/desktop#troubleshooting)

> **如果你实在不会的话，就让你的 AI 读一下我这个[原始的聊天文件](docs/chat.md)，让 AI 告诉你怎么做，这是最简单的。**

## Claude Code 用哪个入口？

- **桌面端**，从官网安装 Claude Desktop，用自己的账号登录，打开 **Code** 标签并选中项目文件夹。个人订阅里，Pro、Max 等支持 Claude Code。[官方下载](https://claude.com/download) · [桌面端说明](https://code.claude.com/docs/en/desktop) · [订阅说明](https://support.claude.com/en/articles/11145838-use-claude-code-with-your-pro-max-or-ultra-plan)
- **习惯用终端**，按官方指南安装 Claude Code CLI，在项目目录运行 `claude`，按提示登录。[CLI 快速入门](https://code.claude.com/docs/en/quickstart)

我当时看到中文语言选项，还问过师兄是不是下错了。遇到这种情况，先回头核对安装来源和版本。想用中文改稿，可以先让它读一段，指出逻辑跳跃和容易误读的地方，等你确认后再动文件。[官方下载](https://claude.com/download)

## 碰到 KYC、Portal 或账号受限

KYC 指身份验证。Anthropic 的帮助中心提到验证合作方 Persona，我当时看到的则是应用里的 **Verification Portal** 提示。聊到「代理」「工具联动」「以前过没过验证」时，我们都在猜，光看弹窗和用过多少天判断不了触发原因。用自己注册或由组织正式分配的账号，按账号里出现的提示完成官方验证。如果验证失败，或觉得账号被误封，用帮助中心列出的支持或申诉入口。Anthropic 的服务条款禁止共享个人账号和登录凭据。[Claude 身份验证与申诉](https://support.claude.com/en/articles/14328960-identity-verification-on-claude) · [Anthropic 个人服务条款](https://www.anthropic.com/legal/consumer-terms#02-account-creation-and-access)

## 有问题可以进群聊

**Claude 使用交流群（QQ 群号 `683921826`）**。安装、改稿或使用时卡在哪儿了，都可以带上客户端和报错来聊。截图发之前记得遮住个人信息和链接。发现文档里有地方过时了，也欢迎开 Issue。

<a href="assets/qq-group.png"><img src="assets/qq-group.png" alt="QQ 群 683921826 的入群二维码" width="260"></a>

## 许可

两份 README 的原创文字采用 CC BY 4.0，欢迎注明出处后转载或改写。聊天记录及图片的权利归各自权利人。[许可全文](LICENSE)

## 交流声明

这篇教程仅供交流，不保证账号一定不被封禁，也不保证不会弹出 KYC 或 Verification Portal。请自行判断并承担使用和操作带来的后果，作者不对这些后果负责。
