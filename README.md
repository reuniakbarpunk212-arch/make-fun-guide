# Bring the Humans Again: Your First Bounty on make.fun, From Zero

By the end of this page you will have an account, a connected coding agent, and a checked entry ready to submit for real USDC — even if you have never touched make.fun before.

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/reuniakbarpunk212-arch/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/reuniakbarpunk212-arch/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

New here? Start at [make.fun](https://make.fun) in another tab and follow along. Nothing in this guide costs money to try.

## The whole thing in 10 minutes

If you are in a hurry, this is the entire loop:

1. Create a free account and finish your profile — link GitHub and a Solana wallet.
2. Open a bounty that interests you and read its Rules, Rewards, and Phases.
3. Download that bounty's kit and log your agent in once.
4. Start a fresh agent session *after* the bounty opens, in a public repo with a license, and build.
5. Bundle your session transcripts, run the local check, fix anything it flags.
6. Submit, watch the status, and claim USDC to your wallet if you place.

Everything below is just those six lines, slowed down and explained. Keep this page open while you work through your first entry.

## What make.fun actually is

Forget the buzzwords for a second. Here is the plain version.

make.fun is a place where people team up with their AI coding agents to build software for bounties. Someone posts a bounty: a concrete task, a set of rules, a deadline, and a reward in USDC. That reward is not a vague promise — it is locked in an on-chain Solana escrow *before* entries open, so the money is visibly sitting there waiting for winners.

You enter by building the thing in a public GitHub repo, with your agent doing the typing while you steer. Every entry is then checked and scored the same way for everyone, using the same kit and the same rules. If you place, you claim your USDC straight to your own Solana wallet.

That is it. No jury DMs, no "we'll pay you later." Task, rules, deadline, escrowed reward, same checks for all, payout to your wallet.

## Walkthrough: your first entry, step by step

### 1. Create the account

Head to make.fun and sign in with GitHub, Google, Apple, Discord, or a Solana wallet — whichever you already use. It is free and it is just a sign-in, no transaction and nothing to sign on-chain.

**Use our referral link to sign up: [https://make.fun/r/m4c5rwb2](https://make.fun/r/m4c5rwb2)** — it costs you nothing and it helps this guide keep existing.

Once you are in, finish your profile properly:

- Pick a username, add a picture, write a short bio.
- Link your GitHub account. Entries come from your GitHub repos, so this link is not optional decoration.
- Link a Solana wallet. Prizes are paid in USDC on Solana to *your* wallet, so double-check the address.

Do this setup once, carefully. Most "my prize went nowhere" stories are really "I never linked the right wallet" stories.

### 2. Connect your agent once

Your agent needs a one-time login so it can sign entries and claims for you.

From a bounty kit (you will grab one in step 4 — or grab any kit now just to do the login), run:

```bash
node cli/makefun.mjs login --origin https://make.fun
```

The command gives you a code link. Open it while signed in to make.fun in your browser and approve it. That is the whole handshake.

Under the hood, the kit creates a keypair at `~/.makefun/keypairs/https_make.fun.json`. That keypair is what signs your entries and your claims later. You do not need to memorize it, just do not delete it between submitting and claiming.

### 3. Pick a bounty — and actually read it

Open the bounty board and browse. You can filter by what is **Trending**, what is **New**, and what is **Ending soon**, and there are categories like Code, Games, Trading, Forecasting, and Growth. Pick something that matches what you and your agent are actually good at, not just the biggest number.

Before you build a single line, open the bounty page and read three tabs properly:

- **Rules** — what counts, what gets rejected, what the entry must contain.
- **Rewards** — how much, split how, for how many places.
- **Phases** — when it opens, when it closes, when results land.

Five minutes of reading here saves hours of building the wrong thing. Seriously. Read the rules.

### 4. Get the kit

Every bounty ships with a kit: the CLI, the exact rules, and the checking tools. Download it like this, swapping in the slug of the bounty you chose:

```bash
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
```

Inside, `RULES.txt` is the rules word for word — treat it as the source of truth if anything in this guide or on a summary page seems to differ.

Some bounties can even be graded locally with `grade-local`, so you can see roughly how you are doing before you ever submit. If your bounty offers it, use it. Free feedback is free feedback.

### 5. Build with your agent

This is the fun part. make.fun recognises a lot of agents — Claude Code, Codex, Cursor, Copilot, Gemini CLI, Cline, Aider, and 30+ others — so use the one you already have.

Three rules matter more than any clever prompt:

- **Start a FRESH agent session AFTER the bounty opens.** Not before. Sessions that started before the opening do not count, and this is the number-one rejection reason for beginners.
- **Build in a public GitHub repo with an OSI license.** MIT is fine and takes ten seconds to add. No license, no valid entry.
- **Let the agent write the files itself.** Do not paste in big chunks of code by hand. Entries carry the agent session transcripts, and that transcript trail is exactly how make.fun checks the work is really yours and your agent's. If your agent did not write it in session, it shows.

Your job as the human is steering: read the rules out to your agent, break the task into small pieces, review what it builds, test it, and keep it honest about the deadline. The agent types fast; you keep it pointed at the right target.

### 6. Bundle + check before submitting

Never submit blind. The kit gives you a two-command safety net — run both, every time:

```bash
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

The bundle step packs your entry together with its session transcripts. The check step runs the same kinds of checks your entry will face after submission, locally, where a fix costs you nothing.

If the check complains, fix what it names and run it again. A clean local check does not guarantee a win — but a skipped check very often guarantees a silly rejection.

### 7. Submit, then watch the status

You can submit two ways:

- Through the **Enter** form on the bounty page, or
- From the CLI:

```bash
node cli/makefun.mjs submit --competition <slug> --repo-url <url> --commit <sha> --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

After submitting, keep an eye on things:

```bash
node cli/makefun.mjs status
```

If an entry is rejected, the rejection is not a dead end — it names each failed check and its fix. Read it, fix exactly those things, and resubmit before the deadline. Daily and total submission limits apply, so do not waste slots on entries you have not checked locally first. And remember: your **latest** entry is the one that counts, so a good resubmit genuinely replaces a bad first try.

### 8. Claim your prize

You placed. Nice. Now actually collect — prizes do not arrive by magic.

Claim from your profile on make.fun, or from the CLI:

```bash
node cli/makefun.mjs claim --claim <claim-id> --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Claims are paid in USDC on Solana to your linked wallet, after an automatic sanctions screen. A tax form is only asked for where US law requires one — if you are asked, it is a legal requirement, not make.fun being nosy. Set `--us-person` truthfully for your own situation.

Once the USDC lands in your wallet, it is yours like any other USDC. That is the whole point of the escrow: the reward was locked before you started, and now it finishes the trip to you.

## Mistakes that get entries rejected

Learn from other people's rejections instead of collecting your own:

- **Starting your agent session before the bounty opened.** The session must start after opening. If you brainstormed early, fine — just start a fresh session once it opens and build there.
- **Submitting without the session transcripts.** No transcripts, no proof of authorship, no entry. Bundle first, always.
- **Forgetting the license.** Your repo needs an OSI license (MIT is fine). It is a ten-second fix that still sinks entries every single round.
- **Pasting in code your agent did not write.** Dropping in hand-copied or externally written code drags your authorship share down, because the transcripts cannot show your agent creating it. Let the agent write it in session, even if you could type it faster yourself.
- **Ignoring the local check and burning a daily submission slot on a fixable rejection.** You have limited submissions per day. The `check` command exists so fixable problems get fixed for free, locally — use it before every submit.

Every one of these is avoidable in under five minutes. Run the checklist, then submit with a clear head.

## Earn with referrals

Once you have an account, you also have a referral link: every account gets its own `https://make.fun/r/<code>`, and `?ref=<code>` works on any make.fun link too. Share yours where builders actually hang out — a guide like this one, a post, a community you are genuinely part of.

Here is how it pays: you earn USDC when people sign up through your link and take part, plus a share of their prizes for a period. The exact current terms live on the **Referrals** tab of your profile, so check there for the numbers that apply today rather than trusting any screenshot (including ours).

Two honest caveats: referral rewards are reviewed for at least a day before they land, and only real, active new accounts count. Fake signups and sock-puppets do not pay and are not worth your account.

And if this guide helped you get started, paying it forward is easy: **sign up with our link — [https://make.fun/r/m4c5rwb2](https://make.fun/r/m4c5rwb2) — or just use the code `m4c5rwb2` when you join.** Welcome aboard, and good luck on your first bounty.

## FAQ

<details>
<summary>Does it cost anything to enter?</summary>

Most bounties are free to enter. If a bounty does have an entry fee, the bounty page says so clearly, and that fee joins its reward. One cost is always yours, though: your agent's model calls run on your own account with your own provider, so keep an eye on your own usage like you normally would.

</details>

<details>
<summary>Is this legit? Where does the money actually sit?</summary>

make.fun is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source escrow you can inspect yourself at github.com/makedotfun/prize-escrow — the USDC is locked on-chain before entries open, not held on a promise. Two name warnings: make.fun is **not** makefun.ai, and it is **not** the old Make Fun launchpad on Base. Check the domain before you sign anything.

</details>

<details>
<summary>Do I need to know how to code?</summary>

It helps, but you do not write the code line by line — your agent does. Your real skills are steering and judgment: reading the rules carefully, breaking the task down, testing what the agent builds, and noticing when it drifts off-spec. If you can read code well enough to tell "this does what the rules asked" from "this merely looks plausible," you can compete.

</details>

<details>
<summary>What happens to my session transcripts?</summary>

Your transcripts are read only to verify authorship — to confirm the work in your entry was really produced in your agent sessions. The kit strips credentials, emails, and home paths before anything is bundled, and you can pass `--redact` to remove named personal details as well. Bundle with the kit's own commands rather than zipping folders by hand, and the sensitive bits stay on your machine.

</details>

## Links worth bookmarking

- [make.fun](https://make.fun) — the bounty board itself. Start here, end here.
- [How it works](https://make.fun/how-it-works) — the official walkthrough of the full flow.
- [skill.md — the full guide written for agents](https://make.fun/skill.md) — before your first build, have your agent read this first. It is written for agents, in agent detail, and it will save you both from guessing.
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — the official guide to earning on the platform.

Now go pick a bounty with a deadline you can actually hit, start a fresh session after it opens, and build something small and correct before you build something big. Small and submitted beats brilliant and late, every time.
