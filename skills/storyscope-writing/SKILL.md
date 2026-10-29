---
name: storyscope-writing
description: Write and revise prose so it does not carry the structural fingerprints of AI writing measured in StoryScope (arXiv 2604.03136). Use for ANY writing task where the output is prose a person will read, such as emails, READMEs, docs, reports, blog posts, cover letters, speeches, short stories and novels, and whenever the user says "/storyscope-writing", "make this sound less like AI", "humanize this", "de-slop this" or "write it like a person would". Also use to audit an existing draft.
---

# StoryScope writing

StoryScope (Russell, Rajendhran, Pham, Iyyer and Wieting, COLM 2026) compared 61,608 stories. A human and five LLMs each wrote to the same 10,272 prompts. With every stylistic feature removed, a classifier still told human from AI at 93.2% macro-F1 using **narrative choices alone**. Editing out clichés and purple prose (the LAMP rewriter) moved detection by only 1.6 points.

What that means for you as the writer: swapping words does not fix AI-sounding text. The tells are in what you choose to say, in what order, and what you leave unsaid. Claude was the most identifiable model in the study (77.1% attribution F1 on narrative features alone), so if you are Claude, assume your defaults are the fingerprint.

The numbers behind every rule are in `references/evidence.md`. Read it when the user asks why a rule exists or wants the evidence.

## How to run it

1. **Find out what you are writing.**
   - Fiction and narrative: Part A and Part B.
   - Personal or persuasive non-fiction (essays, blog posts, cover letters, speeches): Part A.
   - Work and technical writing (emails, Slack messages, status updates, reports, proposals, design docs, READMEs, runbooks, PR descriptions, commit messages): Part C, which says which Part A rules apply and which reverse.
   - Nobody wants a flashback in a password-reset email.
2. **Draft** with Part A in mind (plus Part B for fiction).
3. **Audit.** Go through the checklist at the bottom line by line against the actual draft. Do not audit from memory of what you meant to write. Quote the offending sentence to yourself, then fix it.
4. **Hand it over.** Do not append a note saying the text was checked against StoryScope unless the user asked for an audit report.

When the user hands you a draft to audit, return the revised text plus a short list of what you changed and which rule each change answered. Keep the list to the changes that mattered.

## Part A: every piece of writing

**A1. Never state the moral.** Cut the closing line that tells the reader what the piece meant ("Ultimately, this shows...", "The lesson here is...", "At the end of the day..."). AI narrators state the theme in 77% of stories, humans in 52%. If the point landed, the reader already has it. If it did not, fix the body.

**A2. Name things.** Real people, documents, products, places, version numbers, dates, amounts. "Postgres 16.4" beats "the latest database version". "Genette's *Narrative Discourse*" beats "classic narrative theory". Humans named specific works at almost double the AI rate (47% vs 24%). AI hides behind vague echoes (72% vs 50%).

**A3. Say the feeling.** When emotion matters, use the word: "I was annoyed", "she was scared". Do not route it through the body (tight chest, breath catching, jaw clenching, a knot in the stomach). AI used embodied emotion in 81% of stories against 38% for humans. Humans used plain labels 29% of the time; AI managed 8%.

**A4. Leave real loose ends loose.** If a question is open, say it is open. Do not fold every thread into one tidy line, and do not end on acceptance or understanding just because it feels resolved. AI resolved through "internal understanding" in 47% of stories (humans 27%) and had no subplots 79% of the time (humans 57%).

**A5. Cut the philosophy.** One big-picture sentence is plenty; usually none is needed. AI turned dialogue into philosophical debate 59% of the time (humans 34%) and scored about 20% higher on moralizing.

**A6. Talk to the reader.** "You" is allowed. An aside is allowed. Humans addressed the reader directly in 28% of stories against 7% for AI. AI writes as if no one is listening.

**A7. Go easy on the senses and the scenery.** Description has to earn its place. Do not make weather or rooms mirror someone's mood. Smell is the specific AI over-use (82% vs 57%).

**A8. Vary the rhythm and the voice.** Long paragraph, then a one-line one. A blunt sentence after a careful one. Claude's narrative voice was the most uniform of any source in the study.

**A9. Kill the surface tells too.** They are weaker evidence but cheap to fix:
- no em dashes; use a full stop, comma, colon or brackets
- none of: delve, tapestry, testament to, navigate the landscape, in today's fast-paced world, it's worth noting, a rich blend, nestled, unlock, elevate, seamless, robust (outside code), pivotal
- no "not X, but Y" sentence used more than once
- no lists of exactly three adjectives as a reflex
- no redundant exposition that repeats the previous sentence in grander words

## Part B: fiction and narrative

**B1. Break the timeline.** Open late and go back. Use a flashback, a flash-forward, a time jump. Humans scored higher on chronological discontinuity, anachrony and nonlinear framing. In the paper's words, the human mystery opens at the funeral and spirals backward; the AI one runs from first clue to grand reveal.

**B2. Make the twist rewrite the past.** A reveal should send the reader back to earlier scenes, not just close the plot. Depth of recontextualization was a human-leaning core feature.

**B3. Add subplots that rhyme or argue with the main one.** Humans integrated thematically parallel subplots 42% of the time, AI 21%.

**B4. Let the protagonist be compromised.** Morally mixed protagonists appeared in 59% of human stories and 38% of AI ones. Let outside events, luck or other people drive part of the resolution. Protagonist-driven resolution was AI-leaning (69% vs 46%).

**B5. Introduce people through action or dialogue.** Not a paragraph of hair, eyes and coat. External description was AI-leaning (52% vs 30%). In-dialogue introduction was the single strongest human fingerprint.

**B6. More dialogue, more places.** Humans had a higher dialogue-to-narration ratio and moved across more locations.

**B7. Point at the real world.** Name real books, songs, brands and places when the characters would. Break the fourth wall if the story can take it (humans 67% vs AI 39% on fourth-wall permeability).

**B8. Escalate, and vary the events.** These are Claude's two strongest fingerprints: the flattest event escalation of any source, and the lowest event-type diversity. Make things get worse, faster. Mix the event kinds: a fight, a lie, an accident, a lucky break, a misunderstanding, a betrayal.

**B9. Skip the epilogue.** Claude reaches for epilogues and flash-forward codas more than any other source. End on the scene. Do not default to a quiet ending either; some stories should end loud.

**B10. Take risks with convention.** Claude honoured genre conventions in 62% of stories (other sources 39 to 56%). Subvert one. A dream or vision sequence is fine; Claude avoids them, which is itself a tell.

## Part C: work and technical writing

StoryScope studied fiction only. Rules C1 to C3 below are Part A rules that carry over directly. C4 and C5 are places where the fiction evidence points the wrong way for work writing. C6 to C12 are not from the paper at all: they are standard work-writing practice that targets the same failure (text that reads as generated rather than written by someone who knows the situation). Do not cite StoryScope for C4 to C12.

**From the paper, applies as is**

**C1. No moral, no outro.** This is A1 in work clothes. Cut "In summary...", "Overall, this demonstrates...", "Hope this helps!", "Let me know if you have any questions", and the closing paragraph that restates the bullets above it. End on the last thing the reader needs: the ask, the deadline, the next step.

**C2. Specifics or nothing.** A2 matters more here than in fiction. Name the file path, the function, the version, the ticket number, the cost, the person, the date. "Latency rose from 180 ms to 2.4 s after the 14 Oct deploy of v3.2" beats "we observed performance degradation following a recent release". If you do not know the specific, ask or say you do not know. Never invent one.

**C3. Surface tells.** A9 in full, plus the work dialect: leverage, utilize, streamline, robust, seamless, comprehensive, holistic, synergy, empower, cutting-edge, game-changer, "ensure that", "it is important to note", "plays a crucial role".

**Reversed for work writing**

**C4. Linear and explicit is correct.** B1's broken timeline and the paper's preference for implicit meaning do not apply. Steps go in order. The decision is stated in plain words. Being explicit about *what was decided* is not the same as A1's moralizing about *what it all means*. Keep the first and cut the second.

**C5. Open questions get listed, not left hanging.** A4 becomes: if something is unresolved, say so in its own line with an owner and a date ("Open: who signs off the DPA? Legal, by 7 Nov"). Do not paper over it, and do not leave it implied.

**Work-writing practice (not from the paper)**

**C6. Lead with the point.** The first sentence carries the answer, decision or ask. Background comes after, and only as much as the reader needs to act.

**C7. No preamble.** Cut "I hope this email finds you well", "Great question!", "I wanted to reach out regarding", "As per my last email", and any sentence that announces what the next sentence will say.

**C8. One clear ask, with a date.** If you need something, say what, from whom, and by when. Multiple asks get numbered.

**C9. Absolute dates and real units.** "Thursday 6 Nov", not "next Thursday". "$300 a month", not "significant cost". Times with time zones when people are in more than one.

**C10. Fit the format to the length.** A four-line message has no headers and no bullets. Use bullets only for genuinely parallel items, and tables only for real comparisons. Do not bold every third phrase.

**C11. Hedge once, where it's true.** One "I think" on the uncertain claim, not "it may potentially be possible that". Certain things are stated flatly.

**C12. Write as the person who was there.** First person where you did the thing ("I reran the migration"), and say what you saw. A1 to A3 exist because generated text sounds like no one in particular wrote it.

## Audit checklist

Run this against the draft, not against your intentions.

- [ ] Last paragraph: does any sentence restate the point or the lesson? Cut it. (A1)
- [ ] Every vague source ("experts", "studies", "best practice", "classic works"): name it or delete it. (A2)
- [ ] Every body-as-emotion phrase: replace with the plain feeling, or with behaviour. (A3)
- [ ] Every open question that the draft pretends is closed: reopen it. (A4)
- [ ] Every "what this really means" passage: keep one at most. (A5)
- [ ] Is the reader ever addressed? If the form allows it and it is natural, do it once. (A6)
- [ ] Description that mirrors mood, or any smell: does it earn its place? (A7)
- [ ] Read three paragraphs in a row: are they the same length and shape? Break one. (A8)
- [ ] Search the text for "—", "delve", "tapestry", "testament". Zero hits. (A9)
- [ ] Work only: does the first sentence carry the point or the ask? Is any open question unlisted or missing an owner? Any relative date ("tomorrow", "next week")? Any preamble or "let me know if" outro? Headers or bullets on something under ten lines? (C1 to C12)
- [ ] Fiction only: is the timeline linear start to finish? Is there a subplot? Does the protagonist get to be wrong? Does tension rise? Is there an epilogue to cut? (B1 to B10)

## Judgement calls

- These rules describe what separates human from AI fiction on average. They are not a quality guarantee. A rule that makes a particular piece worse loses to the piece.
- For work and technical writing, Part C decides. Where it reverses a Part A or Part B rule, Part C wins.
- If the user's own style guide or instructions conflict with a rule here, follow the user.
- Never invent specifics to satisfy A2. A real name or nothing.
