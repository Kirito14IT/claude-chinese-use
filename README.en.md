# Getting started with Claude as a Chinese-speaking user

[简体中文](README.md) · English

I wanted to try Claude for editing a paper, so I asked a more experienced friend for advice. We ended up talking about proxies, dropped SSH connections, and account verification. If you're just starting out, pick the app that fits your task and try it on a short passage first. If you hit an error, check the service, the network, and your account separately. [Read the redacted conversation in Chinese](docs/chat.md)

## Check availability where you are

As of November 20, 2026, mainland China is outside Anthropic's supported regions. The policy covers Claude on the web, Claude Code, the API, and access through authorized cloud providers and resellers. Check your actual location and your organization's eligibility before getting started. The steps below are for users who meet the policy. [Anthropic's Supported Regions Policy](https://www.anthropic.com/legal/supported-regions)

## Where should I start if I want to edit a paper?

- **For a paragraph or two**, sign into Claude on the web with your own account, paste a passage you can share, and ask in Chinese. You can find the display language setting in your profile. [Claude on the web](https://claude.ai/) · [Language help](https://support.claude.com/en/articles/10769299-how-to-use-claude-in-your-preferred-language)
- **To work with local files**, install Claude Desktop from the official download page, sign in, open the **Code** tab, and select the project folder you want to work with. Pro and Max are two of the individual plans with Claude Code. [Official download](https://claude.com/download) · [Desktop guide](https://code.claude.com/docs/en/desktop) · [Subscription help](https://support.claude.com/en/articles/11145838-use-claude-code-with-your-pro-max-or-ultra-plan)
- **If you prefer a terminal**, follow the official guide to install the Claude Code CLI, run `claude` from your project folder, and sign in when prompted. [CLI quickstart](https://code.claude.com/docs/en/quickstart)

For a paper, I'd start with one paragraph and see how Claude explains its suggestions. Here's a prompt you can try.

> Please review this paragraph in Chinese. Point out any jumps in the reasoning and anything a reader could misinterpret, then suggest a revision. Keep the original data and citations and flag anything you're unsure about. Show me your suggestions and wait for my approval before editing the file.

## Proxies and dropped connections in the chat

In the conversation, the VPS provided a network exit, 3x-ui managed nodes and subscriptions, and Clash Verge routed traffic locally according to rules. My friend used rule mode with a system proxy at home and a dedicated port for Claude Code at work to fit the office network's requirements.

If you already have an approved HTTP(S) proxy, the Claude Code CLI supports `HTTPS_PROXY` and `HTTP_PROXY`. The Desktop launch flag mentioned in the chat was a guess. The right setting depends on how your Desktop session runs. [Claude Code network configuration](https://code.claude.com/docs/en/network-config) · [Desktop network requirements](https://code.claude.com/docs/en/desktop#network-access-requirements)

1. **Both the web app and Code are unreachable.** Check the official status page, then check your connection. [Claude service status](https://status.claude.com/)
2. **Only Code shows an error.** Check the account you're signed into and whether your plan includes Claude Code, then check the session's network settings. [Desktop troubleshooting](https://code.claude.com/docs/en/desktop#troubleshooting)
3. **SSH keeps dropping too.** Use your hosting provider's web console to check the server and its resource usage. The 1 GB VPS in our chat logged an out-of-memory error, so resource usage was worth checking first.

## What if Claude asks me to verify my account?

I asked my friend after seeing the **Verification Portal** prompt. We talked about the proxy, the tools I'd been using together, and the account. We were guessing at the cause. If you see a prompt, open the verification flow from your own account and follow the official instructions. Use the Help Center for questions or failed verification, and keep sign-in, payment, and verification links within your own official flow. [Identity verification on Claude](https://support.claude.com/en/articles/14328960-identity-verification-on-claude) · [Account sign-in help](https://support.claude.com/en/articles/13189465-log-in-to-your-claude-account)

## Join the conversation

You're welcome in the **Claude discussion group on QQ (group `683921826`)**. If you're stuck getting started, editing a paper, or working in Code, tell us which client you're using and what error you see. Cover personal details and private links before sharing a screenshot. If something in this guide is out of date, feel free to open an issue.

<a href="assets/qq-group.png"><img src="assets/qq-group.png" alt="Join QQ group 683921826 by scanning this code" width="260"></a>

## License

The original text of both READMEs is available under CC BY 4.0. You can share or adapt it with attribution. Rights to the conversation and images remain with their respective owners. [Full license](LICENSE)
