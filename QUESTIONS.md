Key design questions to answer before building this:

1) Product scope
What exact experiences are in v1: 1:1 chats only, or also group chats, voice, stickers, media?
Is the goal historical replay (what they likely would have said then) or live hypothetical conversation (what they might say now)?
What does “real WeChat feel” require for you: UI mimicry, response timing, typing indicators, etc.?
2) Consent, ethics, and legal
Do you have explicit consent from each person whose persona is modeled?
What happens if someone asks to opt out or delete their twin?
Which legal regimes apply (e.g., privacy/data laws), and what’s your compliance plan?
How will the system clearly signal this is an AI simulation, not the real person?
3) Data ingestion and identity resolution
How will chat history be exported/imported reliably from WeChat (format, completeness, timestamps)?
How will you map multiple nicknames/accounts to the same person over time?
Which data types are included in persona building: text only, or emoji, images, voice, files, reactions?
4) Persona modeling approach
What defines a “digital twin” for your use case: tone, vocabulary, beliefs, response style, interests, memory?
What is the minimum data threshold per person to create a usable twin?
How will you handle sparse/noisy histories or personality shifts across years?
Should each twin know only chat history, or also inferred/background knowledge?
5) Architecture choices
One base model + persona memory (RAG), or per-person fine-tuning/adapters?
How do you store memory: raw logs, structured profile, embeddings, time-weighted retrieval?
How do you orchestrate multi-agent chats (turn-taking, context windows, consistency)?
6) Safety and misuse prevention
How do you prevent abuse (impersonation scams, harassment, coercive content)?
What policy filters should block sensitive outputs?
What audit logs and abuse-reporting flows are needed?
7) Fidelity and evaluation
How will you measure “realism” (style similarity, factual consistency, human ratings)?
How will you detect and reduce hallucinations about real people?
What fallback behavior should happen when model confidence is low?
8) UX and controls
How does a user “become” a persona and switch roles safely?
What controls exist to edit/delete twin memory or constrain topics?
How transparent are prompt/settings so users understand why a twin replied a certain way?
9) Security and operations
Where is data stored, and how is it encrypted at rest/in transit?
Who can access raw chat logs and generated personas?
What are latency/cost targets per message, and what scale do you expect?
10) Governance
Who owns the persona model and outputs?
What retention policy applies to imported histories and generated conversations?
How do you handle disputes (“this twin misrepresents me”)?
If helpful, next I can turn these into a concrete system design spec template (requirements, architecture, data schema, model pipeline, and MVP milestones).

You can ignore security and operations, this is purely for personal use


Worked for 28s
Understood — if we ignore security/operations for now, these are the core design questions you should answer first.

1) Product behavior (what “Ghost WeChat” actually does)
Is v1 only 1:1 chat, or also group chat?
Are you simulating how someone would reply now, or replaying how they’d likely reply in the past context?
What does “take on persona” mean exactly: manual switch, role dropdown, or full account-style identity swap?
Should responses include “WeChat-like” style signals (short messages, emoji habits, pauses, typing cadence)?
2) Data ingestion from WeChat history
What export format are you starting from (SQLite/db backup, txt/json export, screenshots + OCR)?
Which message types must be parsed in v1: text only, or also emoji/stickers, voice-to-text, images, files?
How do you normalize timestamps/timezones and preserve chat threading/order?
How will you clean noise (system messages, recalls/deletes, forwarded snippets, duplicates)?
3) Identity resolution
How do you map changing nicknames/remarks to a single person across time?
How do you separate people with similar names?
In group chats, how will you attribute each line to the correct sender reliably?
4) Persona modeling
What traits define each twin: tone, vocabulary, emoji style, topics, beliefs, reply length, politeness, humor?
What is the minimum amount of history needed to build a usable twin?
How do you handle sparse users (few messages) vs heavy users (huge histories)?
Should persona be one static profile, or time-aware (e.g., 2019 persona vs 2025 persona)?
5) Memory and context strategy
Should each twin use only chat history with you, or all chats where they appear?
How much context is used per reply (recent turns + retrieved long-term memories)?
What retrieval strategy works best: semantic search, recency weighting, or hybrid?
How should the model respond when it lacks evidence (“I don’t know” vs plausible guess)?
6) Conversation engine (multi-person simulation)
For group simulation, who speaks next and when?
How do you avoid one twin dominating conversation?
How do twins maintain consistency across long sessions (facts, tone, relationship dynamics)?
7) UX controls for personal experimentation
How do you inspect/edit a twin profile (“persona card”)?
Can you toggle between “strictly evidence-based” and “creative extrapolation” modes?
Can you delete or regenerate a twin if it feels inaccurate?
8) Evaluation (is it actually good?)
How will you score realism: style similarity, phrase overlap, human judgment?
How will you measure consistency over long dialogs?
What are your acceptance criteria for MVP (e.g., “8/10 realism for top 10 contacts”)?
