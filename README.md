<img src="header.svg" alt="Gabriel Gómez García, computer engineer working on AI and data" width="100%">

Computer engineer from the University of Cantabria, now doing a double master's in Computer Engineering and Applied AI at UC3M. I work on the part where language models stop being a demo and have to hold up every day: retrieval, prompt design, evaluation, and the unglamorous business of documenting what you built.

Looking for an internship or a first role in AI and data.

---

## LaredocMind

A retrieval-augmented assistant for LAREDO, the MLOps platform of the ISTR research group at the University of Cantabria. LAREDO helps non-experts build machine learning pipelines, and it shipped without a single page of documentation, so people got stuck looking for information that did not exist.

I wrote that documentation from scratch, nine guides in Markdown, and built the assistant that reads it. The conversation is a LangGraph state graph: a small model rewrites and translates the question, two retrievers hit two separate ChromaDB collections in parallel, Gemini answers from the combined context, and once the history passes six messages a cheaper model folds it into a running summary. The backend is Flask and streams over Server-Sent Events; the frontend is a React widget isolated with Shadow DOM and published on npm.

The part I would defend in an interview is the evaluation. I swept temperature, top-p and chunk size against a gold set with ROUGE-L, BLEU and an LLM as a judge scoring context relevance, faithfulness and answer relevance. The metrics pointed at a temperature of 0.10; the humans preferred 1.0 for warmth. I shipped 0.2, and I can tell you why.

This was my bachelor's thesis, it produced [a paper at JISBD 2025](https://hdl.handle.net/11705/JISBD/2025/80), and the code now lives on inside [istr-uc/LaredoMLOps](https://github.com/istr-uc/LaredoMLOps).

→ [LaredocMind](https://github.com/Gabiz053/LaredocMind) · [thesis](https://hdl.handle.net/10902/37133) · [npm](https://www.npmjs.com/package/laredocmind)

## Traffic congestion in Madrid

An end-to-end classification problem on the city's open data: roughly 4,700 sensors reporting every fifteen minutes, 44 million rows across six months.

Most of the work was not the model. It was noticing that the M-30 sensors were not recording the target variable at all and dropping them; that speed was missing on most roads so load was the only usable signal; that intensity and occupancy were derivable from load and therefore useless as features. It was deciding that one congestion threshold for the whole city was wrong, because a ring road absorbs a load that would gridlock a street in the centre. And it was encoding the hour as a sine and cosine pair so that 23:00 and 00:00 stop being twenty-three units apart.

Congestion happens 7.4 % of the time, so accuracy is a trap: predicting "no jam" forever scores 92.6 %. I evaluated on F1 and the area under the precision-recall curve instead, split the data chronologically, and kept March 2026 sealed until the end. The random forest catches 85.9 % of real jams at 55.4 % precision. For a system meant to divert drivers before a jam forms, that is the trade I would choose.

→ [prediccion-trafico-madrid](https://github.com/Gabiz053/prediccion-trafico-madrid)

## Tele-diario

A serverless Telegram bot that turns a voice note into a structured diary entry inside my Obsidian vault. I send an audio from my phone, Gemini transcribes and analyses it in a single call, and the result lands in a private repository as Markdown with YAML frontmatter. It runs entirely on Google Apps Script, so there is no server and no bill.

The interesting part is the prompt. It forces a JSON object with exactly twenty-seven keys and spells out the merge rules against earlier entries from the same day, which arrays accumulate without duplicating and which fields get overwritten. Four numeric scales are defined level by level so the score does not drift with the model's mood, and there is a checklist the model has to walk before it answers.

I have used it every day since April 2026, which is the only test that matters.

→ [tele-diario](https://github.com/Gabiz053/tele-diario)

---

## Also here

[ARmonia](https://github.com/Gabiz053/armonia-ar) is an augmented reality sandbox in Unity 6: you build a voxel garden on the real surfaces your camera detects, with hand tracking through MediaPipe on the title screen. [Sistema solar VR](https://github.com/Gabiz053/sistema-solar-vr) is an educational game for Meta Quest 3, built by a team of four, and [Depths of Betrayal](https://github.com/Gabiz053/depths-of-betrayal) is a multiplayer murder mystery I led with a team of six.

---

Want to talk? I am on [LinkedIn](https://www.linkedin.com/in/gabrielgomezgarcia/).
