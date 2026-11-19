# 中文用户怎么用 Claude

简体中文 · [English](README.en.md)

我本来只是想试试用 Claude 改论文，找师兄一问，聊着聊着就聊到了代理、SSH 掉线和账号验证。如果你也刚起步，可以先选一个顺手的入口，拿一小段文字试一下。遇到报错，再分开看是服务、网络还是账号的问题。[查看脱敏对话原文](docs/chat.md)

## 先确认所在地区

截至 2026 年 11 月 20 日，中国大陆未列入 Anthropic 的支持地区。Claude 网页版、Claude Code、API 以及授权云平台和转售商提供的 Claude 都在这项政策的范围内。请按实际所在地和组织资格核对支持范围。下面的上手方法适用于符合政策的用户。[Anthropic 支持地区政策](https://www.anthropic.com/legal/supported-regions)

## 想改稿的话，先从哪儿用？

- **想改一两段文字**，用自己的账号登录网页版，贴一段方便分享的文字，直接用中文提问。界面显示语言可以在个人资料里查看。[Claude 网页版](https://claude.ai/) · [官方语言说明](https://support.claude.com/en/articles/10769299-how-to-use-claude-in-your-preferred-language)
- **需要让它读本地文件**，从官网安装 Claude Desktop，登录后打开 **Code** 标签，选中这一轮需要的项目文件夹。个人订阅里，Pro、Max 等支持 Claude Code。[官方下载](https://claude.com/download) · [桌面端说明](https://code.claude.com/docs/en/desktop) · [订阅说明](https://support.claude.com/en/articles/11145838-use-claude-code-with-your-pro-max-or-ultra-plan)
- **习惯用终端**，按官方指南安装 Claude Code CLI，在项目目录运行 `claude`，按提示登录。[CLI 快速入门](https://code.claude.com/docs/en/quickstart)

拿改论文举个例，我会先让它读一段，看看它为什么这么改。你可以试试这句。

> 请用中文帮我检查这一段。先指出哪句话的逻辑跳得太快、哪处表述容易误读，再给一版修改建议。保留原来的数据和引用，拿不准的地方标出来。先把建议发给我，我确认后再改文件。

## 聊天里说的代理和掉线

对话里的 VPS、3x-ui 和 Clash Verge 分别负责网络出口、管理节点和订阅、本地按规则分流。师兄在家用系统代理的规则模式，在公司按工作网络要求，只给 Claude Code 单独走一个代理端口。

已有获准使用的 HTTP(S) 代理时，Claude Code CLI 支持 `HTTPS_PROXY` 和 `HTTP_PROXY`。聊天里提到的桌面端启动参数是当时的猜测。桌面端的实际设置取决于会话怎么运行，可以查官方文档。[Claude Code 网络配置](https://code.claude.com/docs/en/network-config) · [桌面端网络要求](https://code.claude.com/docs/en/desktop#network-access-requirements)

1. **网页和 Code 都连不上。** 先看官方服务状态，再看自己网络的连接情况。[Claude 服务状态](https://status.claude.com/)
2. **只有 Code 报错。** 看当前会话用的是哪个账号、方案是否支持 Claude Code，再查这个会话的网络设置。[桌面端排错](https://code.claude.com/docs/en/desktop#troubleshooting)
3. **SSH 也反复断开。** 可以先用服务商的网页控制台检查服务器状态和资源占用。聊天里那台 1 GB 的 VPS 出现过内存不足的日志，值得先排查资源问题。

## 碰到账号验证怎么办？

我当时看见 **Verification Portal** 才来问师兄，对话里提到了代理、工具联动和账号状态，好几个都是当时的猜测。碰到验证提示，从自己账号里的入口进去，按官方指引完成。有疑问或验证失败，可以走帮助中心的支持渠道。登录、付款和验证链接请留在自己的官方流程里。[Claude 身份验证说明](https://support.claude.com/en/articles/14328960-identity-verification-on-claude) · [账号登录说明](https://support.claude.com/en/articles/13189465-log-in-to-your-claude-account)

## 有问题可以进群聊

**Claude 使用交流群（QQ 群号 `683921826`）**。安装、改稿或使用时卡在哪儿了，都可以带上客户端和报错来聊。截图发之前记得遮住个人信息和链接。发现文档里有地方过时了，也欢迎开 Issue。

<a href="assets/qq-group.png"><img src="assets/qq-group.png" alt="QQ 群 683921826 的入群二维码" width="260"></a>

## 许可

两份 README 的原创文字采用 CC BY 4.0，欢迎注明出处后转载或改写。聊天记录及图片的权利归各自权利人。[许可全文](LICENSE)
