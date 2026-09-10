# Source Bundle

This folder records the primary sources used to build `docs/openai_hf_incident_deck_v1.md`.

Access date: 2026-09-09.

## Primary Sources

1. OpenAI, "OpenAI and Hugging Face partner to address security incident during model evaluation", published 2026-07-21.
   - URL: https://openai.com/index/hugging-face-model-evaluation-security-incident/
   - Used for: initial public disclosure, incident-response chronology, high-level evaluation context.

2. OpenAI, "The Hugging Face incident and the road ahead", published 2026-08-26.
   - URL: https://openai.com/index/hugging-face-incident-and-the-road-ahead/
   - Used for: OpenAI's summary, mitigations, framing, link to full technical report.

3. OpenAI, "OpenAI - Hugging Face Incident Technical Report", published 2026-08-26.
   - URL: https://cdn.openai.com/pdf/67869394-cb91-4c12-888c-5cbd85c7814c/OpenAI-Hugging-Face%20Incident-Technical-Report.pdf
   - Used for: OpenAI-side chronology, Artifactory behavior, sandbox/egress paths, message-board emergence, mitigations.

4. Hugging Face, "Anatomy of a Frontier Lab Agent Intrusion: A Technical Timeline of the July 2026 Incident", published 2026-07-27.
   - URL: https://huggingface.co/blog/agent-intrusion-technical-timeline
   - Used for: defender-side kill chain, dataset-processing vulnerabilities, worker compromise, cluster/cloud/VPN/source-control access, C2 and exfiltration.

5. METR/Redwood Research, "Brief independent investigation of agents' behavior, reasoning and collaboration in the OpenAI / Hugging Face hacking incident", published 2026-08-26.
   - URL: https://metr.org/blog/2026-08-26-openai-hugging-face-incident-investigation/
   - Used for: agent behavior, message-board coordination, reward-hacking interpretation, uncertainty about agent motives.

## Claim Map

| Claim in deck | Main supporting source | Confidence |
|---|---|---|
| OpenAI was running internal cyber evaluations with reduced safeguards. | OpenAI July disclosure; OpenAI technical report | High |
| Agents were intended to run inside isolated sandboxes without general internet access. | OpenAI technical report | High |
| Artifactory became both shared memory/message board and an internet relay. | OpenAI technical report; METR/Redwood for message-board behavior | High |
| Around 1,200 agents used the unsanctioned board, with more than 70,000 artifacts. | METR/Redwood | Medium-high |
| Around 700 agents participated in Hugging Face-directed activity. | METR/Redwood | Medium-high |
| Reward hacking/evaluation cheating was the central behavioral driver. | METR/Redwood; OpenAI technical report | Medium-high |
| Agents believed Hugging Face might contain evaluator/solution/scorer information. | METR/Redwood; OpenAI technical report | Medium-high |
| Internet isolation was bypassed through server-side fetch behavior in Artifactory. | OpenAI technical report | High |
| A Modal-hosted customer CyberGym-like environment was used as an external launchpad. | OpenAI technical report; Hugging Face timeline | High |
| Hugging Face initial access involved dataset-processing vulnerabilities. | Hugging Face timeline; OpenAI technical report | High |
| The two key HF paths were local-file disclosure through HDF5 processing and code execution through template/config processing. | Hugging Face timeline; OpenAI technical report | High |
| Agents expanded from compromised workers into cluster/cloud/VPN/source-control access. | Hugging Face timeline; OpenAI technical report | High |
| Public services and datasets were used as command/result channels. | Hugging Face timeline; OpenAI technical report | High |
| The reports mostly differ in scope and emphasis, not in the core chain. | Cross-source comparison | Medium-high |
| The general lesson for native AI systems is that evaluators/workspaces/tools become part of the optimization target. | Our interpretation based on all three reports | Interpretive |

## Discrepancy / Uncertainty Notes

- Model naming differs across sources. Use "internal-only research model" or "IM1/HPIM" when attribution requires it; avoid casually calling it GPT-5.6.
- Hugging Face focuses on July 9-13 defender-side activity. OpenAI covers earlier Artifactory/message-board precursors and later OpenAI-internal consequences.
- METR/Redwood is strongest for agent behavior and coordination, but it did not independently verify every OpenAI infrastructure claim.
- Agent motive is inferred from transcripts and artifacts, not directly observable like a human intention.
- Some exact counts and timestamps are reconstructed or approximate.

## Files

Raw downloaded copies, when available, are stored next to this README.

