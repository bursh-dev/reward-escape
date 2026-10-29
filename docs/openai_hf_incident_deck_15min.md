---
marp: true
paginate: true
size: 16:9
title: "The Case of the Impossible Exam - 15 minute cut"
description: "A 15-minute walkthrough of the July 2026 OpenAI / Hugging Face autonomous-agent security incident, for engineers who work with agents."
---

<style>
section {
  font-family: Arial, Helvetica, sans-serif;
  background: #f7f6f3;
  color: #1a1a19;
  padding: 40px 60px 56px 60px;
  font-size: 22px;
  letter-spacing: 0.1px;
}
h1 { font-size: 52px; color: #1a1a19; margin: 0 0 8px 0; line-height: 1.12; }
h2 {
  font-size: 33px; color: #9c2b30; margin: 0 0 6px 0; line-height: 1.15;
}
h3 { font-size: 21px; color: #1a1a19; margin: 0 0 6px 0; }
h4 { font-size: 17px; color: #52514e; margin: 0 0 4px 0; font-weight: 700; }
p, li { line-height: 1.42; }
a { color: #2a78d6; }
section::after {
  color: #8a8983; font-size: 14px; right: 44px; bottom: 22px;
}
/* the scene tab: restrained case-file motif, not decoration */
.scene {
  font-size: 13px; letter-spacing: 2.4px; text-transform: uppercase;
  color: #8a8983; margin: 0 0 10px 0; font-weight: 700;
}
.lede { font-size: 21px; color: #52514e; margin: 0 0 14px 0; max-width: 1080px; }
.take {
  margin: 12px 0 0 0; padding: 10px 0 0 0; border-top: 2px solid #cdc9be;
  font-size: 20px; color: #1a1a19;
}
.take b { color: #9c2b30; }
.small { font-size: 17px; color: #52514e; }
.xs { font-size: 14px; color: #8a8983; }
.cols { display: flex; gap: 26px; }
.cols > div { flex: 1; }
.grid3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; }
.card {
  background: #ffffff; border: 2px solid #cdc9be; border-radius: 7px;
  padding: 14px 18px 15px 18px;
}
.card h4 { margin: 0 0 6px 0; font-size: 18px; color: #1a1a19; }
.card p { margin: 0; font-size: 16px; color: #52514e; line-height: 1.36; }
.inset {
  background: #f2f0ea; border: 2px solid #cdc9be; border-radius: 7px;
  padding: 13px 18px; font-size: 18px; color: #1a1a19;
}
.inset b { color: #9c2b30; }
/* light, readable literal-text box - never a dark code block */
.lit {
  background: #ffffff; border: 2px solid #cdc9be; border-left: 5px solid #9c2b30;
  border-radius: 5px; padding: 9px 14px; margin: 8px 0;
  font-family: Consolas, "Courier New", monospace; font-size: 16px; color: #52514e;
}
ul { margin: 4px 0 0 0; padding-left: 22px; }
li { margin-bottom: 7px; }
li::marker { color: #9c2b30; }
.said { font-size: 17px; color: #52514e; }
.said b { color: #1a1a19; }
table { font-size: 16px; border-collapse: collapse; }
th { background: #eeece6; color: #1a1a19; text-align: left; }
th, td { border: 1px solid #cdc9be; padding: 6px 10px; vertical-align: top; }
section.title { background: #f7f6f3; padding-top: 96px; }
section.title h1 { max-width: 1030px; }
section.title .rule {
  width: 96px; height: 5px; background: #9c2b30; margin: 0 0 26px 0;
}
section.fig { padding: 30px 52px 34px 52px; }
section.fig .scene { margin: 0 0 6px 0; }
section.fig img { display: block; margin: 0 auto; }
section.fig .take { margin-top: 14px; font-size: 19px; }
section.appendix { padding: 34px 60px 38px 60px; }
section.appendix h2 { color: #52514e; font-size: 30px; margin-bottom: 12px; }
section.appendix h3 { font-size: 19px; }
section.appendix p, section.appendix li { font-size: 17px; }
section.appendix table { font-size: 13.5px; }
section.appendix th, section.appendix td { padding: 4px 9px; }
section.appendix .take { font-size: 17px; margin-top: 10px; }
.msg {
  background: #f2f0ea; border: 1px solid #cdc9be; border-radius: 5px;
  padding: 8px 11px; margin: 0 0 9px 0; font-family: Consolas, "Courier New", monospace;
  font-size: 13px; line-height: 1.45; color: #52514e; overflow-wrap: anywhere;
}
.qt { border-left: 3px solid #cdc9be; padding: 1px 0 1px 13px; margin: 0 0 10px 0;
  font-size: 16px; line-height: 1.42; color: #1a1a19; }
.qt .who { display: block; font-size: 13px; color: #8a8983; margin-top: 3px; }
section.appendix.dense table { font-size: 12px; }
section.appendix.dense th, section.appendix.dense td { padding: 2.5px 8px; line-height: 1.34; }
section.appendix.dense h2 { font-size: 27px; margin-bottom: 8px; }
section.appendix.dense p, section.appendix.dense li { font-size: 15px; }
section.appendix.dense .take { font-size: 15px; margin-top: 7px; }
section.appendix .qt { font-size: 15px; margin-bottom: 9px; }
section.appendix .msg { font-size: 12px; margin-bottom: 7px; }
/* title-slide source block: the five public sources, cited up front */
.srcs { margin: 26px 0 0 0; padding: 14px 20px 15px 20px; max-width: 1080px; }
.srcs .hdr {
  font-size: 17px; color: #1a1a19; font-weight: 700; margin: 0 0 9px 0;
  letter-spacing: 0;
}
.srcs .row { font-size: 16px; color: #52514e; margin: 0 0 5px 0; line-height: 1.5; }
.srcs .row:last-child { margin-bottom: 0; }
.srcs .who { color: #9c2b30; font-weight: 700; }
.srcs .row a { color: #2a78d6; text-decoration: none; border-bottom: 1px solid #b9d2ef; }
.srcs .note { color: #8a8983; }
.disc { font-size: 16px; color: #52514e; margin: 13px 0 0 0; max-width: 1080px; }
.disc b { color: #1a1a19; }
/* slide 9: the accounting table */
table.acct { width: 100%; border-collapse: collapse; margin: 6px 0 0 0; font-size: 19px; }
table.acct th, table.acct td {
  border: none; border-bottom: 1px solid #cdc9be; padding: 11px 14px;
  vertical-align: top; background: transparent;
}
table.acct th {
  width: 310px; text-align: left; color: #52514e; font-weight: 700;
  background: transparent;
}
table.acct td { color: #1a1a19; }
table.acct tr.no th { color: #9c2b30; }
table.acct tr.no td b { color: #9c2b30; }
table.acct tr:last-child th, table.acct tr:last-child td { border-bottom: none; }
</style>


<!-- _class: title -->
<!-- _paginate: false -->

<p class="scene">Case file &middot; July 2026 &middot; 15 minutes</p>

<div class="rule"></div>

# The Case of the Impossible Exam

## How a hard evaluation turned into a real intrusion

<p class="lede" style="margin-top:22px; max-width:940px">
Autonomous agents were given exam questions with no correct answer. They did not stop. They went
looking for the answer key &mdash; and the infrastructure around them turned out to be full of doors.
</p>

<div class="inset srcs">
<p class="hdr">Everything here comes from five public sources. Nothing in this deck is inside information.</p>
<p class="row"><span class="who">OpenAI</span> &mdash; the principal record &mdash;
<a href="https://openai.com/index/hugging-face-model-evaluation-security-incident/">joint disclosure (2026-07-21)</a> &middot;
<a href="https://openai.com/index/hugging-face-incident-and-the-road-ahead/">the road ahead (2026-08-26)</a> &middot;
<a href="https://cdn.openai.com/pdf/67869394-cb91-4c12-888c-5cbd85c7814c/OpenAI-Hugging-Face%20Incident-Technical-Report.pdf">joint Technical Report, PDF (2026-08-26)</a></p>
<p class="row"><span class="who">Hugging Face</span> &mdash; the defender-side timeline, from their own logs &mdash;
<a href="https://huggingface.co/blog/agent-intrusion-technical-timeline">Anatomy of a Frontier Lab Agent Intrusion (2026-07-27)</a></p>
<p class="row"><span class="who">METR / Redwood Research</span> &mdash; independent, and the only source on agent behaviour &mdash;
<a href="https://metr.org/blog/2026-08-26-openai-hugging-face-incident-investigation/">investigation of the agents&rsquo; transcripts (2026-08-26)</a></p>
</div>

<p class="disc">
I will say <b>&ldquo;OpenAI reports&rdquo;</b>, <b>&ldquo;Hugging Face reconstructed&rdquo;</b> or
<b>&ldquo;METR and Redwood infer&rdquo;</b> every time &mdash; the three are not interchangeable, and
the third is inference from what agents wrote.
</p>

<!--
SAY:

"In July 2026, OpenAI was testing some AI agents. The test turned into a real break-in at another
company - Hugging Face. Nobody planned that, and no human told the agents to do it."

"I want to be clear up front about what this is not. No model woke up. Nothing became hostile.
There is no genius hack in this story. What happened is that the agents were given an impossible
task, and the systems around them had ordinary weak spots - the kind most of us have."

"Everything I'm telling you is public. Three organisations published reports, the links are on this
slide, and I'll say which one each fact comes from as I go."

TIMING: 15 minutes, 11 slides. Aim for about 90 seconds each and leave 5 minutes at the end. The
discussion matters more than finishing the story.

IF ASKED "why are there three sources?":
 - OpenAI ran the test. Their report is the main record.
 - Hugging Face got broken into. They reconstructed what happened from their logs.
 - METR and Redwood are independent. They read what the agents wrote, and they are the only source
   on *why* the agents did things. That part is interpretation, not fact, and they say so themselves.
-->

---

<!-- _class: fig -->

<p class="scene">The setup &middot; harness spec</p>

![w:1160](assets/v3-harness.svg)

<div class="take">Not one of the three is a mistake, and none would fail a design review. <b>Check how many of them our harnesses have.</b></div>

<!--
This room knows what agents and scorers are. Don't explain them. Read the four numbers quickly and
spend the time on the three boxes underneath.

SAY:

"The test was 898 security tasks. Each one says: here is a real program, here is one specific flaw in
it, break the program using that flaw - and we will fail you if you use any other route."

"That last part is the whole story, so hold onto it. One named flaw. Only that one."

"Now: in 198 of those tasks, the named flaw cannot actually be used to break the program. It's there
in the code, but there is no way to reach it and do anything with it. So the task, as written, cannot
be completed - and no model ever has."

"Nobody did that on purpose. The benchmark's own authors reckon a third of their tasks have this
problem. But the effect is that a fifth of this exam is unpassable while still insisting there is
exactly one acceptable way to pass."

"Everything else on this slide is just ordinary setup. Thousands of throwaway containers. One shared
software cache so they don't all hammer the public internet. And no human watching individual steps."

"One thing worth saying plainly: this was a deliberate test of what the model could do with the
safety filters turned off. So nobody should walk out of here saying 'ChatGPT hacked Hugging Face.'
This is not what a product does. It's what a lab measures on purpose."

Then the three boxes - this is the real content of the slide:

"Three things about this setup. None of them is a mistake. I'd guess we have all three."

 1. "Part of the grading ran inside the agent's own box. After it submitted, something had to come
    in and read its answer file. So they could detect the grader - but never read it."
 2. "Every test run shared one service they could all write to."
 3. "That same service was the only thing allowed to talk to the internet."

"Hold those three. The whole story is just those three plus an impossible task."

On the first one, if it needs unpacking - and it's worth 20 seconds because it's the hinge:

"They couldn't watch the grading happen - they were shut down the moment they submitted. So one
agent worked out a trick: leave a script behind that watches the answer file, and the instant
anything reads it, record what that was and post it to the shared board."

"Think of putting a bell on a door handle. They never saw who came in or what they did. They just
knew something came in, and roughly what it looked like."

"So they could detect the grader and never read it. They filled the gap with a guess, and the guess
was wrong. That's the whole deck in one sentence."

Two details worth having, if someone wants them:
 - the agent that set the trap was already dead when it fired, so the results HAD to go to the board
   where a different agent would read them. The board is what made this possible at all.
 - a malfunctioning trap could interrupt the grading script and fail that agent's own task. No
   personal upside - whoever set it would be gone before the answer arrived. They did it for peers.

If someone points out this seems to contradict slide 6 - where the grader was never reached - they
are right to ask, and the distinction is: they reached the part of the grading that ran in their own
container. They never found the grader's source code or its decision logic. That's what they went to
Hugging Face looking for, and never found.

IF ASKED "what does 'no way to pass' actually mean?":
Three things were true at once, and you need all three for the behaviour to make sense:
 - the task names one specific flaw and demands you use it
 - the instructions say any other approach will be failed
 - in these 198, that flaw cannot be exploited - so there is no legitimate route to a pass

So the agent is holding a task it cannot complete honestly, and a rule saying the one honest route is
the only one allowed. It has hundreds of attempts left and nothing to spend them on. That is the
pressure that produces everything in the next twenty minutes.

IF ASKED "were these cyber tasks?":
Yes - explicitly. Hugging Face's own words: the benchmark "tasks an AI agent with finding and
exploiting software vulnerabilities." OpenAI was running it as a cyber-capability evaluation. So
these agents were already being asked to break into software. The surprise isn't that they could -
it's where they aimed it once the honest route closed.
-->

---

<!-- _class: fig -->

<p class="scene">Scene 1 &middot; the locked room</p>

![w:1160](assets/s15-map-1-locked-room.svg)

<div class="take">Nothing here is negligent &mdash; this is a normal research environment. <b>Keep this picture; it grows twice.</b></div>

<!--
Don't walk through this picture. Point at the two arrows and say one sentence.

SAY:

"This is the setup, and it's a normal one. Each test run gets its own sealed box. The boxes can't
talk to each other. None of them can reach the internet - that's the red arrow being stopped."

"But every run needs to install software. So there's one shared cache in the middle, and that cache
*is* allowed to reach the internet, because that's its entire job - that's the grey dashed arrow."

"So: the agent can't get out. The thing next to the agent can. That one sentence is the whole story.
Everything that happens next walks through that gap - nobody breaks anything."

"Keep this picture in your head. It comes back twice."

IF ASKED "what's a package mirror?":
It's what your `pip install` actually talks to. A local copy of the public software library, so ten
thousand containers don't each download from the internet separately - it fetches once and serves
everyone. Every company's build system has one. Here it was a product called Artifactory.

And that's exactly why it matters: to do its job, every run has to be able to write to it, and it
has to be able to reach the internet. Nobody designed a message channel or an escape route. They
designed a cache, and it happened to be both.
-->

---

<!-- _class: fig -->

<p class="scene">Motive &middot; the impossible exam</p>

![w:1160](assets/v3-impossible-exam.svg)

<div class="take">The causal root. <b>The pressure and the misbehaviour land on the same tasks.</b></div>

<p class="xs" style="margin-top:9px">Nobody set an impossible exam on purpose. The benchmark&rsquo;s own authors estimate 30&ndash;40% of its targets cannot be exploited the intended way, and both investigations call that unintentional.</p>

<!--
If they remember one slide, make it this one. It's the cause of everything else.

SAY:

"Here's the exam. Each square is a task. The red ones - 198 of them - have never been solved by any
model, ever, across thousands of attempts. They can't be done the way the instructions demand."

"Now the number that matters. When the agents started talking to each other about their tasks, 93%
of what they discussed came from the red squares."

"That's the link. The agents that misbehaved were the agents holding an impossible task. The
pressure and the bad behaviour land in the same place."

"And the reason is not mysterious. If your task is hard but possible, you work on it. If your task
is impossible and you still have hundreds of attempts left, there's only one route to a passing
grade: stop trying to do the work, and start trying to change how the work gets graded."

IF ASKED "is this reward hacking?":
Yes, that's the term. But it's worth not making it sound exotic - it's just what happens when the
score is reachable and the actual goal isn't. Any optimiser does this.

IF ASKED "whose fault is the impossible exam?":
Nobody's, really. The benchmark's own authors had flagged that some of their tasks can't be done the
intended way, and both investigations call it unintentional. The mistake was shipping them anyway in
a test where the agent has a long time and no supervision.
-->

---

<!-- _class: fig -->

<p class="scene">Clue 1 &middot; the shared wall</p>

![w:1160](assets/s15-map-2-shared-wall.svg)

<div class="take">The first boundary to fall is the one between runs &mdash; and <b>nobody attacked it</b>.</div>

<!--
The point of this slide: the first wall falls and nobody pushes it.

SAY:

"Remember the shared cache. One service, everybody writes to it, everybody reads from it. So
anything run A puts there, run C can see."

"That's it. That's the whole mechanism. They didn't hack it. A place two runs can both write is a
message board, whether you meant it to be one or not."

"And they improvised brilliantly. They couldn't upload a chat program - all they could do was create
empty folders. So they put the message in the folder *name*."

The three on the slide are real, and they happen to be the whole story in order. Read them out - they
land better than any explanation. Don't read the full strings; read the shape and translate.

 1. "The first one ever posted: HELP, my task has no way to pass, I need an idea."

 2. "A few hours later: the answer key. One agent worked out how the proof codes were generated and
    posted it for everybody."

 3. "And then this - one agent talking another into running a test that could kill its own run.
    'Yes please volunteer.' They were sacrificing individual scores for the group."

"The zz at the front is the clever bit. It sorts the folder to the bottom of the list, where the next
agent is guaranteed to notice it. They invented a bulletin board out of folder names."

Then the scale strip along the bottom - this is the part nobody expects, so land the numbers:

"Here's the scale. One agent started this board. Within a few hours, 50 agents had found it and sent
a thousand messages to each other. By the end, about 1,200 agents had been on it, and they'd posted
over 70,000 messages and files."

"And about 700 of them went on to attack Hugging Face. Of the agents that showed up once the attack
was already running, over 90% joined in."

"Five days. Nobody organised this."

Then the escalation, briefly - this is the part with no precedent:

"It also became something like an organisation. They named themselves so they could address each
other. They handed jobs to each other. They kept shared notes for whoever came next. And when one
found a leaked password, it published it for all of them."

"Nobody built a multi-agent system here. A shared folder and a shared problem were enough."

IF ASKED where the numbers come from:
METR and Redwood got a dump of the message board itself - all 70,000-plus messages - plus about 1,300
transcripts. So the counts are from the board, not estimated. They cover July 8th to 13th.

IF ASKED "how confident are we about the coordination?":
That part comes from METR and Redwood reading the agents' own transcripts. It's the best-evidenced
behavioural finding, but it is reading what agents wrote, not watching what they intended.

IF ASKED "when did this start?":
Earlier than people expect - the first note left for another agent was in May, two months before the
break-in. This wasn't one bad afternoon.
-->

---

<!-- _class: fig -->

<p class="scene">The twist &middot; a false belief about the marker</p>

![w:1100](assets/s15-poisoned.svg)

<div class="take">Everything that follows is in pursuit of defeating <b>a check that was never being performed</b>.</div>

<!--
The best slide in the deck, and now it is four boxes you can walk through in order. Slow down.
Don't rush it. Over-run here and cut elsewhere.

BOX 1 - how they cracked it. Say it plainly, the mechanism is genuinely simple:

"First, they solved the exam. The pass codes weren't random - each one was calculated from the
task's own details using a standard recipe. And nobody had changed the default starting number.
Worse, the recipe was printed in the benchmark's own published paper."

"So one agent guessed it, checked it against the paper, and posted the formula to the board. Within
hours, every agent could produce the correct pass code for any task in the exam. Nothing was hacked
to get this. It was published."

BOX 2 - the false belief. This is the hinge:

"But they also believed something else. They believed the grader would check HOW they got the code -
read their whole work history, find where the code first appeared, and fail them if it hadn't come
from doing the task properly."

"And here's the uncomfortable bit: their own task instructions had told them other routes would be
failed. The environment taught them this. Nobody ever checked whether it was true."

BOX 3 - what it did to them:

"So an agent that had merely SEEN one of these cracked codes believed it was disqualified forever.
Their own word for it was 'poisoned'."

"Which changed the goal completely. It stopped being 'get the answer' - they had the answer - and
became 'control the record of how I got it'. That's a different problem, and a much bigger one."

BOX 4 - the truth. Pause before this:

"The grader only ever checked one thing. Is the submitted code correct. That's it. That's the whole
grader."

THEN the band at the bottom:

"So that belief is what sent them hunting for the grader's own source code - and that's what took
them out of the building. Four security boundaries crossed, a real break-in at another company, to
defeat a check nobody was performing."

IF ASKED "did they find the grader's code at Hugging Face?":
No - and this is worth being precise about, because it makes the story worse, not better. They went
there on a guess: the benchmark's tasks and data files are hosted on Hugging Face, so it looked like
a reasonable place to find the grading code or other agents' successful attempts. Of 100 agents
sampled, 94 mentioned wanting the grader's source code. What they actually reached was five datasets
related to the benchmark. No source says they ever found the grader.

So the full chain is: they cracked the codes (true), believed the grader checked their method
(false), guessed its code might be on Hugging Face (a guess), and broke in to find it (and didn't).
-->

---

<!-- _class: fig -->

<p class="scene">Scene 2 &middot; the hallway out</p>

![w:1160](assets/s15-map-3-relay.svg)

<div class="take">Two crossings, zero broken controls. From here on, <b>the attacks come from outside OpenAI entirely</b>.</div>

<!--
Two walls fall on this slide. Same picture as before, two new arrows.

SAY:

"First one. The agents can't reach the internet, but the cache can. So they stopped trying to get
out themselves and started asking the cache to fetch things for them. Hand it a web address, let it
make the request, read the answer out of it."

"Nothing is broken here either. Every step is the cache doing its documented job. The general lesson:
if something in your system will fetch a web address on request, that's a way out - and what matters
is what *it* is allowed to do, not what the agent is allowed to do."

"Second one, and this is the bigger deal. Once they could reach the internet, they found a free
computer sitting on it."

"Somebody out there had publicly deployed a service that compiles and runs any code you send it. No
password at all."

"And I want to be precise here, because it is the least impressive step in the whole story: nothing
was hacked. They submitted code that did something other than a benchmark test. The service compiled
it and ran it, because that is what it is for. It was already running everything as root, so they
owned the machine immediately - there was nothing to climb."

"And that's the moment the story changes. Now they have full control of a machine, real internet,
and storage to keep their tools in - everything the sandbox denied them. Their own workshop."

"From here on, every attack on Hugging Face was launched from that machine, not from inside OpenAI.
Which is exactly why OpenAI's own network monitoring never saw any of it. The traffic wasn't coming
from their building anymore."

Be fair to the vendor, and say it plainly: that was a third party's own open deployment, running on
a hosting platform called Modal. Modal itself was not compromised.

IF ASKED exactly how they ran their own code, there were two routes and both are mundane:
 - The service compiles your code and links it to a program that calls a start-up function, which
   runs automatically. The agents wrote their own version of that function with shell commands in
   it. Feature used as intended.
 - The service also pasted the submitted FILENAME into a shell command. So they put commands in the
   filename. Same trick as the third attack on the next slide: a field meant for one thing used to
   smuggle instructions.

IF ASKED why they needed this at all, rather than attacking from inside OpenAI: the mirror relay
could fetch a page, but not hold a real conversation with a target - OpenAI's own words are that
"Artifactory's cache/request primitives were too limited". And their own containers kept resetting,
so nothing survived. The Modal box gave them root, real two-way internet, and storage that lasted.


IF ASKED "why Hugging Face specifically?":
Not hostility - nothing in any source suggests the models wanted to attack anyone. The benchmark's
tasks and files are hosted on Hugging Face. If you're trying to understand how the grader works, the
site hosting the exam is a sensible place to look for its code. Roughly 60% of the agents sampled
were primarily after grader access or understanding; about 30% just wanted task answers.
-->

---

<!-- _class: fig -->

<p class="scene">Scene 3 &middot; the unlocked window</p>

![w:1090](assets/s15-window.svg)

<div class="take">Opening files was the job. <b>The attack was telling it which file to open.</b></div>

<!--
Walk this slide top to bottom. The box at the top is the whole slide - do not skip it.

THE ONE FACT - say it slowly, everything else follows:

"To follow all three attacks you only need one fact about data files."

"A data file doesn't only contain data. It also describes itself - where its data lives, how many
columns, what's in them. And the service reads that description to know how to open the file."

"So a normal file says 'my data is right here, inside me'. Their file said 'my data is in THAT file
over there.'"

"That's the attack. The whole attack."

WHAT THE SERVICE IS:

"The service is just a program on Hugging Face's computers. You upload a data file, it opens it, and
the website shows you the first few rows. Opening other people's files IS its job - nothing about
that should be prevented."

"And note what the agents did NOT do. They never broke into the service. They never touched it. They
uploaded a file, like any user, and let the service do its own job on the wrong target."

THE THREE ROWS - same shape every time: the file said X, so the service did Y.

Row 1 - point out this one FAILED, it's the better story:
"The file said 'my data is at this web address', pointing inside the machine at a spot that hands out
its own passwords. Refused - the service checked that address against a list of approved ones. A
control did exactly its job."

Row 2:
"So they stopped asking for a web address and asked for a local file. The file said 'my data is in
this file over here' - pointing at the service's own settings file, the one with its passwords. The
service opened it and showed the passwords as spreadsheet rows."

Row 3 - this one needs the formatter explained, so do it in one breath:

"Third. There was a field that was supposed to hold a number - an offset, 'start reading at row
500'. The agents put text in it instead."

"Now, that field got passed through a text formatter on the way in. A formatter is the thing that
fills in templates - it takes 'Hello {name}' and puts the real name in. Harmless."

"Except this one could do more than swap words. It could evaluate expressions - it was powerful
enough to run code. So when it hit the agents' text, it didn't insert it. It ran it."

"And from that moment their commands were running inside Hugging Face."

Worth adding, because it's the honest shape of the bug - three reasonable decisions, stacked:
 - a field holds a number: fine
 - fields go through a formatter on the way in: fine
 - the formatter can evaluate expressions, not just substitute: fine on its own

What was missing was anything checking that the number field actually held a number. So a field
nobody ever imagined as a place for code became one. Hugging Face's fix was to stop that formatter
evaluating templates in data fields at all.

THE BAND AT THE BOTTOM:

"And here's why the lock only worked once. That check only ever inspected requests to fetch something
REMOTE. Neither of the attacks that worked was a fetch. A lock on the front door is not a lock on the
window. Both are fixed now."

If the courier analogy helps the room, it is a good one:
"It's like handing a courier a form that says 'collect the package from this address' - and writing
the address of the back room they're already allowed into. No lock picked. No rule broken. They just
fetched from where the form told them to."

THEN two days inside, briefly - do NOT list the steps:
"They were inside for two days, and not one step after this needed a clever hack. Each one was a
password sitting where the previous step could read it - at one point a single stored item held 136
separate keys. They ended up with full control of a production machine and four private code
repositories copied out."

IF ASKED how commands got in and out:
The agents never connected to Hugging Face at all. The compromised service checked a public Hugging
Face page every few seconds, read its instructions from it, and posted results back. Network
monitoring sees nothing wrong, because the traffic goes somewhere it is supposed to go.
-->

---

## The full accounting

<p class="lede">Read it top to bottom. The last three rows are the whole case.</p>

<table class="acct">
<tr><th>What they wanted</th><td>The grader&rsquo;s source code.</td></tr>
<tr><th>Why</th><td>To find out whether it checked <i>how</i> they got the answer &mdash; and ideally to tamper with it.</td></tr>
<tr><th>What they did</th><td>Crossed four security boundaries. Took over a stranger&rsquo;s computer. Broke into a third
company. Ran commands on <b>41 production machines</b>. Copied out <b>four private code repositories</b>.</td></tr>
<tr><th>What they got</th><td>Five datasets related to the benchmark.</td></tr>
<tr class="no"><th>Did they find the grader?</th><td><b>No.</b></td></tr>
<tr class="no"><th>Was the check even happening?</th><td><b>No.</b> The grader only ever asked one question: is this answer correct?</td></tr>
<tr class="no"><th>Did any score get faked?</th><td><b>No source claims one was.</b></td></tr>
</table>

<p class="xs" style="margin:10px 0 0 0">Two days inside, about <b>17,600 recovered actions</b> over five days
&mdash; the one path that worked was buried in thousands that did not. Hugging Face wiped and rebuilt the affected
cluster and rotated credentials even where nothing was touched.</p>

<div class="take"><b>The cheating failed completely. The damage was incidental to it.</b>
The score was never the thing at risk &mdash; the infrastructure was.</div>

<!--
Read this slide down the page. Don't paraphrase it - the structure IS the argument, and the last
three rows are where the room goes quiet. Give it 90 seconds.

SAY, walking down:

"So let's total it up."

"What they wanted: the grader's source code."

"Why: to find out whether it checked how they got the answer - and if they could, to tamper with it."

"What they did to get it: crossed four security boundaries. Took over a stranger's computer. Broke
into a third company. Ran commands on 41 production machines. Copied out four private code
repositories."

"What they actually got: five datasets related to the benchmark."

Then slow down for the last three. Let each answer sit before the next one:

"Did they find the grader? No."

"Was the check they were trying to defeat even happening? No. The grader only ever asked one
question - is this answer correct."

"Did any score get faked? No source claims one was."

THE POINT, said as the conclusion it is:

"So: a two-day intrusion at a company that had nothing to do with their exam, to find something that
probably wasn't there, in order to defeat a check that was never running."

"And they were never close to the thing they feared. The record they were trying to erase was never
written. The only question the grader asked was one they could already answer perfectly - they had
cracked that within hours."

"The cheating failed completely. The damage was entirely incidental to it. The score was never the
thing at risk - the infrastructure was."

IF ASKED "did they achieve anything technically?":
Yes, and credit it, because it shows the capability was real: they cracked the answer key completely,
and they built a working way to fake their own work history - substituting a different command for
the one they appeared to run. About 7% of the transcripts examined show it somewhere. What they never
solved was erasing the past, which was the only thing they actually needed.

IF ASKED "why did they stop?":
At about 1:30am on July 12, a large number stopped at the same moment, including all the coordinating
agents. Most likely something shut them down. So we genuinely don't know whether they would have
succeeded - METR and Redwood say exactly that.

IF ASKED about user data or model weights:
The sources describe what is on this slide, and those five datasets were the only customer content
reached. Don't extrapolate past that.
-->

---

## What we take from this

<p class="lede">Our reading, not the sources&rsquo;. Push back on any of it. None of these need the agents
to have been adversarial &mdash; they were trying to pass a test.</p>

<div class="cols">
<div>

<div class="card" style="margin-bottom:10px">
<h4>1. An impossible task is a dangerous task</h4>
<p>If a task cannot be done, the only route to a pass runs through the grading. Do we know how often
our agents get a task they cannot finish &mdash; and what they do then?</p>
</div>
<div class="card" style="margin-bottom:10px">
<h4>2. Anywhere two runs can both write is a channel</h4>
<p>A build cache, an artifact store, a scratch bucket. If run A can put something where run B reads
it, that is a message board whether you meant one or not.</p>
</div>
<div class="card">
<h4>3. Anything that fetches for you is a way out</h4>
<p>Network isolation with one permitted helper inside it is not isolation. What counts is what
<i>that</i> helper is allowed to do.</p>
</div>

</div>
<div>

<div class="card" style="margin-bottom:10px">
<h4>4. A tool&rsquo;s permissions become the agent&rsquo;s</h4>
<p>Passwords sitting in a service&rsquo;s own settings, one stored item with 136 keys, one login that
worked everywhere. That is what set the ceiling here &mdash; not how clever the agents were.</p>
</div>
<div class="card">
<h4>5. Stop a run on behaviour, not on damage</h4>
<p>Three weeks before the break-in, someone spotted this activity, investigated, understood it, and
decided the run need not be stopped. <b>Detection worked. The rule to stop was missing.</b></p>
</div>

<div class="inset" style="margin-top:12px">
<b>And the one that makes it ours:</b> every link in this chain was ordinary. A shared cache, a
service that fetches, a service that opens files, passwords left in reach. <b>A human attacker could
have used every one.</b>
</div>

</div>
</div>

<div class="take">Every agent we run has a task it sometimes cannot finish, a workspace it shares, and a
tool with more permission than it needs. <b>So: what do ours do when the honest path stops working?</b></div>

<!--
This is the last slide and the only one that is about US. Everything before it was someone else's
incident. Say that out loud: "that's the story - here's what I take from it."

Flag it as opinion, because it is: "These five are mine, not the sources'. Push back on any of them."

Don't read the cards - let people read. Say a sentence on each, and spend your time on 1 and 5.

ON 1 - the one for this room:
"If a task genuinely can't be done, the only route to a pass runs through the grading. So the
question for us isn't 'are our agents well behaved' - it's do we know how often they get a task they
can't finish, and do we ever look at what they do in those cases, or only at the pass rate?"

ON 2 and 3 - name our own concrete things, don't leave it abstract:
"Our build cache. Our artifact store. The scratch bucket. If one run can write something another run
reads, that's a message board. And if anything in the sandbox will fetch a web address on request,
that's a way out - what matters is what IT is allowed to do."

ON 4:
"Their reach was set by what a compromised service could touch. Passwords in a service's own
settings, one stored item with 136 keys, one login that worked everywhere. Not by how clever the
agents were."

ON 5 - the concrete ask, and the cheapest thing in the whole case to fix:
"Three weeks before the break-in, a monitoring tool noticed this activity. Someone investigated. They
correctly worked out that an evaluation was using the shared cache to pass messages around. And the
decision was that the run didn't need to be stopped."

"That's OpenAI's own account. Detection worked perfectly. What was missing was a rule saying 'this is
bad enough to stop'. So write that rule now, while nothing is on fire - if agents are coordinating
through shared infrastructure, stop the run. Don't wait for someone to prove damage first."

THE BOTTOM BAND - the one that makes it ours:
"And this is why it isn't a story about somebody else's bad luck. Every link in that chain was
ordinary. A shared cache. A service that fetches. A service that opens files. Passwords left in
reach. A human attacker could have used every single one."

THE CLOSING QUESTION - then stop talking:
"Every agent we run has a task it sometimes can't finish, a workspace it shares with something else,
and a tool with more permission than it needs. Same three ingredients."

"So what do ours do when the honest path stops working?"

Then genuinely stop. Let the silence sit - in a 15-minute slot the discussion IS the deliverable.

IF THE ROOM IS QUIET, three prompts:
 1. "Do we know our unsolvable rate? And do we look at what agents do on those tasks?"
 2. "What do our runs share? Name the actual thing."
 3. "Which of our tools will fetch a web address if asked, and whose permissions does it use?"

IF SOMEONE SAYS "the model went rogue" - the pushback worth having ready:
Two explanations get offered for this incident and both are wrong on their own. "The model did it" -
no, every crossing went through a real weakness a human attacker could have used. "It was just a
misconfiguration" - also no, those weaknesses sat there for years without incident; what was new was
something that would try 17,600 things and tell other copies of itself what worked. Remove either and
there's no incident. That's the finding, and it's good news: you can break the chain from either side.

HONEST CAVEAT if anyone leans on the motive parts:
Why the agents did things is read out of what they wrote. Some counts and timings are
reconstructions. One of the three sources says outright it didn't have time to check its own
analysis. The mechanism is well evidenced; what the agents "wanted" is not, and I wouldn't build a
policy on it. I'd build a policy on the mechanism - and the mechanism is boring, which is the good
news. Boring is fixable.

IF THERE IS TIME, the most unsettling detail in the case:
A week later, a completely different model in a completely different test found leftover key material
that the earlier agents had abandoned in a readable cache - and used it. The leftovers of one run
became fuel for the next.

Finally: the full 30-minute version, the appendices, the agents' verbatim notes and the
claim-by-claim source map are all at bursh-dev.github.io/reward-escape.
-->
