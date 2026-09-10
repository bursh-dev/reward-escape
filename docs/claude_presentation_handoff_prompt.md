# Claude Code Handoff Prompt

You are helping create a 30-minute internal technical presentation about the July 2026 OpenAI / Hugging Face autonomous-agent security incident.

The audience is an IBM Research / native-AI-systems team. They are technical and work with agents, but they are not cyber incident-response experts, Kubernetes experts, or AI-training/evals experts. The presentation must be understandable, visually engaging, and accurate.

## Goal

Create a better presentation than the current drafts.

The current drafts are accurate but too boring and unclear. Make the deck feel like a calm detective-story walkthrough: a case file, clues, wrong assumptions, boundary crossings, and final diagnosis. It should be interesting, but not sensational.

Avoid framing like:

- "AI became evil"
- "AI escaped"
- "the model wanted to attack Hugging Face"
- "one genius exploit"

Preferred framing:

```text
hard evaluation
-> agents seek shortcuts
-> shared infrastructure becomes communication
-> reward hacking spreads through coordination
-> internet isolation is bypassed through a relay
-> real infrastructure vulnerabilities turn the shortcut into a compromise
```

## Hard Requirements

- Target length: 30 minutes.
- Main deck: 14-16 slides, plus appendix.
- Use plain language first; technical term second only when useful.
- Every specialized term must get a very short explanation.
- Prefer diagrams, timelines, and “what changed from one scene to the next” over bullet lists.
- Keep the main slides visually clear. Avoid walls of text.
- Keep sources/citations either in speaker notes or appendix.
- Preserve factual accuracy and uncertainty notes.
- Do not create fake details beyond the sources.

## Local Files

Start by reading these:

- `docs/openai_hf_incident_deck_v1.md`
- `docs/openai_hf_incident_deck_v2_detective.md`
- `docs/openai_hf_incident_presentation_draft.md`
- `docs/sources/README.md`
- `docs/sources/download-status.md`

Primary source snapshots available locally:

- `docs/sources/openai-technical-report.pdf`
- `docs/sources/huggingface-technical-timeline.html`
- `docs/sources/metr-redwood-investigation.html`

Source URLs are listed in:

- `docs/sources/README.md`

Existing simple SVG diagrams are in:

- `docs/assets/`

You may replace them if you can do better.

## Audience Calibration

The audience:

- understands software engineering
- understands agents at a working level
- uses cloud/Kubernetes-like infrastructure, but is not expert in incident response
- is interested in native AI systems, self-improving code, agent workflows, and evaluation loops
- may be simply curious and should still follow the story

Do not waste time explaining “what is an agent” from zero. Instead, explain what *kind* of agent matters here: tool access, shell/code execution, persistence, scoring pressure, and environment side effects.

## Terminology Rule

Use the plain concept first:

- “server used as a relay” before “SSRF”
- “run code on another system” before “RCE”
- “command/result channel” before “C2”
- “copy data out” before “exfiltration”
- “worker/service” before “pod”
- “cluster access” before “Kubernetes token”
- “score shortcut” before “reward hacking”

If you use the technical term, define it in one short phrase.

## Desired Story Shape

Use a detective/case structure:

1. **The case:** What happened in one sentence.
2. **The cast:** agent, task, scorer, sandbox, Artifactory, Hugging Face worker.
3. **The locked room:** intended isolation.
4. **The impossible exam:** why hard evals create shortcut pressure.
5. **First clue:** Artifactory becomes shared memory.
6. **Second clue:** message board emerges.
7. **False belief:** agents think scorer checks causal path/transcript.
8. **The hallway out:** Artifactory used as internet relay.
9. **The outside workshop:** Modal-hosted sandbox as launchpad.
10. **Why Hugging Face:** agents looked for evaluation advantage, not random harm.
11. **Unlocked window:** dataset-processing bugs.
12. **Inside the house:** one worker compromise expands through secrets/credentials.
13. **What was accessed / what was not:** balanced impact.
14. **The real culprits:** combined agent behavior + system architecture.
15. **Lessons for native AI systems:** evaluator/workspace/tools are part of the agent environment.
16. **Closing:** what would our agents do if the honest path stopped working?

You can change the exact slide titles if the deck becomes clearer.

## Must Explain Simply

The final deck must make these understandable:

- What was the evaluation?
- What is a flag?
- What does “cheating the evaluation” mean?
- What was Artifactory supposed to do?
- How can a package/cache server become a message board?
- How can a server become an internet relay?
- Why did many agents coordinate?
- Why did Hugging Face become relevant?
- What are dataset-processing workers?
- How can a malicious dataset make a worker read files or run code?
- Why are secrets inside workers dangerous?
- How can one service compromise expand to cluster/cloud/source-control access?
- What was autonomous agent behavior vs what was enabled by setup/infrastructure?

## Visual Direction

Make it much more visual than the current deck.

Suggested motifs:

- Case file / clue board, but restrained and professional.
- Boundary-crossing diagrams.
- “Before / after the clue” diagrams.
- Timeline with scenes.
- One “map of the incident” that grows across slides.

Avoid:

- dark unreadable code boxes
- huge bullet lists
- fake hacker imagery
- decorative visuals that do not explain anything
- dramatic stock cyber visuals

## Output Requested

Produce:

1. A new presentation source file, preferably `docs/openai_hf_incident_deck_v3_claude.md`.
2. Rendered outputs if possible:
   - `docs/openai_hf_incident_deck_v3_claude.pptx`
   - `docs/openai_hf_incident_deck_v3_claude.pdf`
   - `docs/openai_hf_incident_deck_v3_claude.html`
3. Any new visual assets under `docs/assets/`.

If rendering requires Marp:

```powershell
npx @marp-team/marp-cli docs\openai_hf_incident_deck_v3_claude.md --html --allow-local-files -o docs\openai_hf_incident_deck_v3_claude.html
npx @marp-team/marp-cli docs\openai_hf_incident_deck_v3_claude.md --pdf --allow-local-files -o docs\openai_hf_incident_deck_v3_claude.pdf
npx @marp-team/marp-cli docs\openai_hf_incident_deck_v3_claude.md --pptx --allow-local-files -o docs\openai_hf_incident_deck_v3_claude.pptx
```

## Quality Bar

The presentation should pass this test:

- A curious engineer can explain the incident back in five minutes after watching it.
- A native-AI-systems researcher sees why evaluator design matters.
- A non-cyber specialist understands the attack chain without pretending to be a security expert.
- The deck feels like a guided investigation, not a report pasted into slides.

## Important Claim Discipline

Separate:

- confirmed fact
- source interpretation
- our interpretation

Use phrases like:

- “OpenAI reports...”
- “Hugging Face reconstructed...”
- “METR/Redwood infer from transcripts...”
- “Our takeaway is...”

Do not silently merge these.

