<img src="header.svg" alt="Gabriel Gómez García" width="100%">

Computer engineer from the University of Cantabria, now on a double master's in Computer Engineering and Applied AI at UC3M. I am looking for an internship or a first job in AI and data.

Almost everything I have built sits around the same problem: putting the right fragment in front of a language model, writing the prompt that keeps it honest, and then measuring whether the answer was any good.

---

## LaredocMind

LAREDO is the MLOps platform of the ISTR research group at the University of Cantabria. It exists so that people who are not machine learning engineers can build and deploy pipelines. When I started, it had no documentation whatsoever, and users were hunting for pages that had never been written.

So I wrote them. Nine guides in Markdown, in English, because retrieval over an English corpus behaved better in my tests. Then I built the assistant that reads them.

The conversation runs as a LangGraph state graph. A small model rewrites and translates the question, two retrievers query two separate ChromaDB collections at the same time, and Gemini answers from the combined context. Past six messages a cheaper model folds the history into a running summary, so the window never fills up. Flask serves it over Server-Sent Events. The widget is React, isolated with Shadow DOM, published on npm.

I spent more time on the evaluation than on the graph itself. ROUGE-L and BLEU against a gold set, plus a model scoring context relevance, faithfulness and answer relevance from 1 to 5, sweeping temperature, top-p and chunk size one parameter at a time. The metrics landed on a temperature of 0.10. The people who tried both versions preferred the one at 1.0, which came out warmer. I shipped 0.2.

It was my bachelor's thesis, it turned into [a paper at JISBD 2025](https://hdl.handle.net/11705/JISBD/2025/80), and the code was later folded into [istr-uc/LaredoMLOps](https://github.com/istr-uc/LaredoMLOps).

[Repository](https://github.com/Gabiz053/LaredocMind) and [thesis](https://hdl.handle.net/10902/37133).

## Traffic congestion in Madrid

The city publishes what its traffic sensors record: around 4,700 of them, one reading every fifteen minutes. I took six months of that, 44 million rows, and tried to predict whether a given point would be jammed at a given hour.

Fitting the model was the short part. First I had to drop every M-30 sensor, since none of them were recording the target variable. Speed was missing on most streets, which left load as the only signal present everywhere. Intensity and occupancy turned out to be derivable from load, so they added nothing.

Then the threshold. One cutoff for the whole city would have been wrong, because a ring road absorbs loads that would gridlock a street in the centre, so urban roads and the M-30 got different ones.

Congestion happens 7.4 % of the time. Predict "no jam" forever and you score 92.6 % accuracy, which is why I evaluated on F1 and on the area under the precision-recall curve. The split is chronological and March 2026 stayed sealed until the very end. On that month the random forest catches 85.9 % of the real jams, and 44.6 % of its alarms are false. Since the point is to divert drivers before a jam forms, I would take that trade.

[Repository](https://github.com/Gabiz053/prediccion-trafico-madrid).

## Tele-diario

I send a voice note to a Telegram bot from my phone. Gemini transcribes and analyses it in a single call, and a few seconds later the entry is sitting in my Obsidian vault as Markdown with YAML frontmatter, synced to a private repository. No server anywhere: it all runs on Google Apps Script.

The prompt is where the work went. It forces a JSON object with twenty-seven keys and spells out, field by field, how a new entry merges with the earlier ones from the same day. Which arrays accumulate without duplicating, which values get overwritten, which get rewritten whole. Four numeric scales are defined level by level so the scoring does not drift with the model's mood, and there is a checklist the model walks before it answers.

I have used it every day since April 2026.

[Repository](https://github.com/Gabiz053/tele-diario).

---

## Also here

[ARmonia](https://github.com/Gabiz053/armonia-ar), an augmented reality sandbox in Unity 6 where you build a voxel garden on the surfaces your camera detects, with hand tracking through MediaPipe. [Sistema solar VR](https://github.com/Gabiz053/sistema-solar-vr), an educational game for Meta Quest 3 built by four of us. And [Depths of Betrayal](https://github.com/Gabiz053/depths-of-betrayal), a multiplayer murder mystery I led with a team of six.

---

I am on [LinkedIn](https://www.linkedin.com/in/gabrielgomezgarcia/).
