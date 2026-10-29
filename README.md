# storyscope-writing

A Claude Code skill that writes, and rewrites, prose without the structural habits that give AI text away.

In March 2026 Hachette pulled the horror novel *Shy Girl* after it was flagged as roughly 78% AI-generated. Five months later, a team at the University of Maryland and Google DeepMind published [StoryScope](https://arxiv.org/abs/2604.03136) and showed something more uncomfortable than "AI overuses em dashes". They took 10,272 published short stories, had Claude Sonnet 4.6, GPT-5.4, Gemini 3 Flash, DeepSeek V3.2 and Kimi K2.5 each write their own version of every one, and then threw away every stylistic feature they could find.

The classifier still caught the AI stories 93.2% of the time.

It was reading the *choices*. AI narrators spell out the moral (77% of stories, against 52% for humans). They show fear as a tight chest instead of saying "she was afraid" (81% vs 38%). They tell the story in order, with one plot thread and no loose ends, and they gesture at "classic literature" instead of naming a book. And Claude, the model this skill runs on, was the easiest AI to identify: flat escalation, epilogues, polite respect for genre convention.

You can't fix that with a thesaurus. When the researchers ran an automated editor over the AI stories to strip out clichés and purple prose, detection dropped by 1.6 points.

So this skill works on the choices.

## What it does

When you ask Claude for anything a person will read, whether an email, a README, a report, a cover letter or a chapter, the skill:

1. drafts with a set of rules taken from the paper's 30 core features and Claude's 26 fingerprint features,
2. audits the draft line by line against a checklist (it quotes the offending sentence to itself, then fixes it),
3. hands you the text without a note saying it did any of that.

Give it a draft of your own and it returns the revision plus a short list of what changed and which rule each change answers.

For essays and posts it applies the general rules: don't state the lesson, name real sources, use plain emotion words, leave open questions open, cut the philosophising, vary the rhythm, and drop the em dashes and the "delve"s. For fiction it adds the structural ones: break the timeline, make twists rewrite earlier scenes, add a subplot that argues with the main one, let the protagonist be wrong, escalate harder, and cut the epilogue.

Work and technical writing (emails, Slack, status updates, design docs, READMEs, PR descriptions) gets its own mode, and it's the part you should be most skeptical of, because the paper never looked at a single email. Three rules carry over unchanged: no summary outro, specifics instead of vague sources, and no slop vocabulary. Two flip. In a runbook, linear and explicit is right, and an unresolved question gets its own line with an owner and a date instead of being left artfully open. The rest (lead with the ask, absolute dates, no "hope this finds you well") is ordinary good practice, and the skill is told not to cite StoryScope for any of it.

It won't put a flashback in your password-reset email.

## Before and after

You've received this email. Probably this week. The facts are in there, under the filler.

> **Subject:** Update on Infrastructure Cost Optimization Initiative
>
> Hi team,
>
> I hope this email finds you well! I wanted to reach out regarding our ongoing efforts to streamline our cloud infrastructure costs. As you know, cost optimization plays a crucial role in ensuring the long-term health of our operations.
>
> Over the past few weeks, we have leveraged a comprehensive, holistic approach to identify key areas of inefficiency. Our analysis revealed that roughly 40% of our compute spend was going to development servers that were left running overnight and on weekends, and that we were storing over 18 TB of old log files in standard storage. We have implemented several robust measures, including automated shutdown schedules for development servers and moving older logs to cheaper archive storage. Early results are promising, with our monthly bill coming down from around $21,000 to approximately $14,500.
>
> It is important to note that some decisions are still pending. In particular, Priya is looking into whether we should purchase reserved instances for the production database, and we would need a decision on that by Friday 14 November.
>
> Ultimately, this initiative demonstrates our commitment to operational excellence and responsible resource management.
>
> Let me know if you have any questions!
>
> Best,
> Sam

Here is what the skill handed back, unedited:

> **Subject:** Cloud bill down from $21,000 to about $14,500 a month; reserved-instance decision due Friday 14 November
>
> Hi team,
>
> Our monthly cloud bill has dropped from around $21,000 to about $14,500.
>
> Most of the savings came from two problems we found. About 40% of our compute spend was going to development servers left running overnight and at weekends, so those now shut down automatically on a schedule. We were also keeping more than 18 TB of old log files in standard storage, and we've moved the older ones to cheaper archive storage.
>
> Open: should we buy reserved instances for the production database? Priya is looking into it, and we need a decision by Friday 14 November.
>
> Best,
> Sam

Same facts. The number moved from the middle of paragraph two to the subject line, and the one thing anyone has to *do* got its own line.

Then it added this, which nobody asked for:

> **The date is off.** In 2026, 14 November is a Saturday. Friday is 13 November. I left the date as you wrote it, so please confirm which day you mean.

I wrote that sample email myself and didn't notice. It also pointed out that the original never says who actually makes the reserved-instance call, and that "past few weeks" had been dropped because there was no real date range to replace it with. It won't invent one.

## Install

Inside Claude Code:

```
/plugin marketplace add dev-rishabh/storyscope-writing
/plugin install storyscope-writing@storyscope-writing
```

Or from a terminal:

```bash
claude plugin marketplace add dev-rishabh/storyscope-writing
claude plugin install storyscope-writing@storyscope-writing
```

Restart Claude Code (or run `/reload-plugins`) afterwards.

## Use

It triggers on its own for writing tasks. To call it explicitly:

```
/storyscope-writing:storyscope-writing rewrite the intro of docs/launch.md
```

Phrases like "make this sound less like AI", "humanize this" or "de-slop this paragraph" work too.

## What's in the repo

```
.claude-plugin/
  marketplace.json      marketplace listing (this repo is its own marketplace)
  plugin.json           plugin manifest
skills/storyscope-writing/
  SKILL.md              the rules, the workflow and the audit checklist
  references/
    evidence.md         every number behind every rule, from Tables 2, 3, 16 and 17
```

## Where the rules come from

Jenna Russell, Rishanth Rajendhran, Chau Minh Pham, Mohit Iyyer and John Wieting, *StoryScope: Investigating idiosyncrasies in AI fiction*, COLM 2026. [arXiv:2604.03136](https://arxiv.org/abs/2604.03136). Their code and data are at [jenna-russell/storyscope](https://github.com/jenna-russell/storyscope).

This skill is not affiliated with the authors. Any mistakes in turning their tables into writing rules are mine, not theirs.

One honest limitation. The paper measures what makes AI fiction *detectable*, not what makes writing *good*, and the skill is told as much: when a rule makes a piece worse, the piece wins. Whether matching the human column of Table 16 makes a story better is a question the study leaves open, and so do I.

## License

MIT. See [LICENSE](LICENSE).
