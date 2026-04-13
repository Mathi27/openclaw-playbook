# Frequently Asked Questions

---

### Do I need a Mac mini or any external hardware?

No. The entire course runs on a cloud VPS (Virtual Private Server). You rent one from Hostinger using their one-click OpenClaw template, and Day 1 walks you through it. All you need is a laptop or desktop with a browser and a Telegram account on your phone.

Some experienced users run OpenClaw on a Mac mini at home. That works well, and you can always port to hardware once you have learned how OpenClaw works. But most people get overwhelmed with the hardware setup requirements and end up never configuring their Claw properly. This course is designed to save you from that overwhelm: you learn the concepts and build a working setup first, on infrastructure that is ready in minutes.

 
### Why does the course start with security?

Because the features that make OpenClaw useful are the same features that create risk. An agent that runs continuously, reads your email, and sends messages on your behalf has a larger attack surface than a tool you open and close. The community learned this the hard way through uncontrolled agent actions, malicious skills on ClawHub, and prompt injection through email.

Day 1 locks down the gateway before anything else gets connected. Every day after that adds capability incrementally, with guardrails in place before each new integration goes live. This is deliberate. You understand what each capability does and where the risks are before you turn it on.

---

### Is my data private?

Yes. OpenClaw runs on a VPS that you control. Your conversations, emails, files, and API keys stay on your server. Nothing is routed through a third party beyond the AI provider you choose for model inference (Anthropic, OpenAI, or Google). The course does not use any shared infrastructure.

---

### Can I use any AI provider?

OpenClaw supports Anthropic (Claude), OpenAI (GPT), Google (Gemini), DeepSeek, and local models. You pick the provider and model you want during setup and can switch later. The course recommends starting with a mid-tier model (Claude Sonnet, GPT-5.4, or Gemini Flash) for daily use, and explains when to upgrade or downgrade for specific tasks.

---

### How much does this cost to run?

Three costs to consider:

1. **VPS hosting**: About INR 2.5K /month on Hostinger.
2. **AI API usage**: Depends on your provider and how much you use your Claw. Mid-tier models are significantly cheaper than top-tier. We cover which providers work well and how to reduce your costs in the [API key guide](getting-your-api-key.md).
3. **The course itself**: Free. Always will be.

---

### What if I am not technical?

Zero prior experience with servers, Docker, or AI agents is required. The course is AI-first: you read the concepts in `learn.md`, then hand the `build.md` file to an AI coding agent (Claude Code, Cursor, or Codex on Days 1 and 2, then your own Claw from Day 3 onward). The agent handles the technical setup. You focus on understanding what each piece does and why.

---

### Can I skip days or do them out of order?

Not recommended. Each day builds on the previous one. Day 3 requires the security setup from Day 1 and the identity files from Day 2. Day 6 requires the channel from Day 3. The progressive layering is the point: you verify each capability works before adding the next.

If you already have a running OpenClaw instance, you can skim the learn files for earlier days and focus on the builds for the days that cover what you have not set up yet.


[← Back to Course Overview](README.md)
