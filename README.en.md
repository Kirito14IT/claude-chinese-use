# Claude Code setup and troubleshooting for Chinese-speaking users

[简体中文](README.md) · English

I wanted to try Claude Code for editing a paper. After asking a more experienced friend for advice, the first thing I got stuck on was SSH access to the VPS. I got the subscription working, then ran into timeouts and account verification. Here's the order I'd check things in if I were doing it again. [Original conversation in Chinese](docs/chat.md)

## Check availability where you are

As of November 20, 2026, mainland China is outside Anthropic's supported regions. The policy applies to Claude on the web, Claude Code, the API, and Claude offered through authorized partners. Eligibility depends on your actual location and, where applicable, your organization. Account eligibility is separate from network configuration. [Anthropic's Supported Regions Policy](https://www.anthropic.com/legal/supported-regions)

## From a VPS to Clash Verge

Use this sequence when setting up a proxy on a machine and network you're authorized to use.

### 1. Rent a Linux VPS and check that you can sign in

We used a 1 GB Ubuntu VPS. Check that the plan supports a Linux distribution you know and provides a browser console, so you can look at logs if SSH fails. Connect on the SSH port given by your provider and keep the credentials private. Make sure your local network can reach the VPS and you can open a shell before you install the panel. The original chat includes the hosting location, plan screenshots, and the referral link we discussed at the time.

DigitalVirt's Los Angeles 9929 entry tier was listed at **¥39 per month** when we chatted. If it sells out and you still want to order on that same route right away, you'll have to choose a higher-priced tier that's in stock. Check the listed prices and availability when you order. [Plan screenshot from the chat](docs/media/vps-plan.png)

I installed Codex on the small VPS as well, and the system later logged an `Out of memory` error. If you only need to ask an AI about installing something, you can do that on your own computer and leave the VPS to run the service. [The original memory log](docs/media/vps-memory-log.png)

### 2. Copy the subscription link in 3x-ui

1. Follow the project's installation guide on a VPS you administer. Sign into 3x-ui and check that Xray is running. The panel address shown during installation is where you manage the service.
2. In 3x-ui, enable the subscription service under **Panel Settings → Subscription**. In your configured inbound, find the client you set up for your device and copy its subscription link. Choose the Clash format for Clash Verge when the panel offers it.
3. Check that your local machine can reach the subscription URL. This link lets your client update its configuration and may contain access credentials. Keep it as private as the panel login.

[3x-ui installation guide](https://github.com/MHSanaei/3x-ui/wiki/Installation) · [3x-ui subscription docs](https://github.com/MHSanaei/3x-ui/wiki/Common-questions-and-problems#13-how-does-the-panel-subscription-link-work)

### 3. Import it into Clash Verge and enable the system proxy

1. Open **Subscriptions** in Clash Verge and import your subscription URL. Select the new profile and check the **Proxies** page for the expected nodes.
2. Switch to **Rule** mode and enable **System Proxy**. Try a site you already have permission to access, then look at the client's connections list to see which rule matched. System proxy applies to apps that read that setting. My friend used rule mode at home and a dedicated port for one app at work to fit the office network's requirements. For apps that ignore the system proxy, check whether your device and network allow TUN mode.
3. If a single app still fails, check its own network settings. The Claude Code CLI reads `HTTPS_PROXY` or `HTTP_PROXY` at startup for an approved HTTP(S) proxy. Follow the official instructions for Desktop Code sessions. The Desktop launch flag in the chat was a guess.

[Importing a subscription in Clash Verge Rev](https://www.clashverge.dev/guide/profile.html) · [System proxy and TUN](https://www.clashverge.dev/guide/quickstart.html) · [Claude Code network configuration](https://code.claude.com/docs/en/network-config)

### 4. When something drops, start where it first fails

| Symptom | What to check first |
| --- | --- |
| SSH drops or the remote extension host keeps exiting | Use the provider's web console. On Ubuntu, check memory with `free -h` and use `sudo journalctl -k --since today` to look for out-of-memory messages near the time of the drop. |
| SSH works but the subscription won't import or lists no nodes | Check the panel's subscription service, whether the client is enabled and still valid, the domain and certificate on the subscription URL, and whether the local client can reach it. Test nodes once the profile imports. |
| The subscription updates but the node shows `timeout` | Check the VPS status, whether the service is listening on the intended port, and firewall settings. Then check the provider's incident notices or file a support ticket. In our case a reboot didn't help. Support reported data center maintenance, and the connection later recovered. |
| Only Claude Code fails, or a Portal prompt appears | Check the service status, then your signed-in account, plan, and client network settings. If you're asked to verify, follow the prompt from your own account. |

[Support ticket from the outage](docs/media/vps-support-ticket.png) · [Claude service status](https://status.claude.com/) · [Desktop troubleshooting](https://code.claude.com/docs/en/desktop#troubleshooting)

> **If you're still stuck, the easiest thing to do is ask your AI to read the [original chat file](docs/chat.md) and walk you through it.**

## Where to open Claude Code

- **Desktop**. Install Claude Desktop from the official site, sign in with your own account, open the **Code** tab, and select your project folder. Pro and Max are two of the individual plans that support Claude Code. [Official download](https://claude.com/download) · [Desktop guide](https://code.claude.com/docs/en/desktop) · [Subscription help](https://support.claude.com/en/articles/11145838-use-claude-code-with-your-pro-max-or-ultra-plan)
- **Terminal**. Install the Claude Code CLI using the official quickstart, run `claude` from your project directory, and sign in when prompted. [CLI quickstart](https://code.claude.com/docs/en/quickstart)

When I saw Chinese in the language menu, I asked my friend if I'd downloaded the right app. If you're unsure, check where you downloaded it from and which version you're running. For a paper, ask it to review one paragraph in Chinese for gaps in the reasoning and ambiguous wording, then wait for your approval before editing the file. [Official download](https://claude.com/download)

## KYC, Portal prompts, and account restrictions

KYC refers to identity verification. Anthropic names Persona as its verification partner, and the prompt I saw in the app was labeled **Verification Portal**. We wondered about the proxy, the tools I'd used together, and whether the account had already been verified. Those were guesses. A prompt and a few weeks of use don't establish what triggered it. Use an account you registered yourself or one your organization assigned to you, and follow the official prompt that appears in your account. If verification fails or you believe your account was suspended in error, use the support or appeal links in the Help Center. Anthropic's terms prohibit sharing individual accounts and sign-in credentials. [Claude verification and appeals](https://support.claude.com/en/articles/14328960-identity-verification-on-claude) · [Anthropic Consumer Terms](https://www.anthropic.com/legal/consumer-terms#02-account-creation-and-access)

## Join the conversation

You're welcome in the **Claude discussion group on QQ (group `683921826`)**. If you're stuck getting started, editing a paper, or working in Code, tell us which client you're using and what error you see. Cover personal details and private links before sharing a screenshot. If something in this guide is out of date, feel free to open an issue.

<a href="assets/qq-group.png"><img src="assets/qq-group.png" alt="Join QQ group 683921826 by scanning this code" width="260"></a>

## License

The original text of both READMEs is available under CC BY 4.0. You can share or adapt it with attribution. Rights to the conversation and images remain with their respective owners. [Full license](LICENSE)

## Disclaimer

This guide is shared for discussion. It makes no guarantee against account suspension, KYC, or Verification Portal prompts. You are responsible for how you use it and the consequences of your actions. The author takes no responsibility for those consequences.
