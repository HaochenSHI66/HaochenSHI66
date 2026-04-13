![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=200&section=header&text=Haochen%20Shi&fontSize=50&fontColor=fff&animation=fadeIn&fontAlignY=38&desc=CS%20%40%20PolyU%20|%20Multimodal%20AI%20Research%20|%20Full-Stack%20Engineering&descAlignY=58&descSize=17)

<div align="center">

[![Website](https://img.shields.io/badge/shc66.com-Personal%20Site-blue?style=flat-square&logo=googlechrome&logoColor=white)](https://shc66.com)
[![GitHub](https://img.shields.io/badge/GitHub-HaochenSHI66-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/HaochenSHI66)
[![Email](https://img.shields.io/badge/Email-haochen8.shi-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:haochen8.shi@connect.polyu.hk)

<br/>

![Typing SVG](https://readme-typing-svg.herokuapp.com?font=Fira+Code&pause=1000&color=2E9EF7&center=true&vCenter=true&width=550&lines=Full-Stack+Developer;Multimodal+AI+%26+VLM+Researcher;Open+to+Summer+Research+Opportunities)

</div>

---

## About Me

CS undergrad at PolyU, GPA **3.85**. Currently running URIS-funded research on whether a layered VLM architecture — detector + tracker + on-demand reasoning — actually beats end-to-end querying for grounded, multi-turn home environment dialogue. Shorter answer: it depends on how you define "beats."

I tend to build things all the way through, not just the model part. Looking for summer research in 2026, multimodal AI or NLP.

> [!IMPORTANT]
> **Research Affiliation:** URIS — Undergraduate Research and Innovation Scheme, PolyU
> Competitive university-wide scheme open to all undergraduates. **100 students selected per cohort** across all faculties. Within the CS department, only **5–6 CS students** were matched with a CS-track supervisor — making this one of the rarest undergraduate research placements in the university. [View Official Awardee List ↗](https://www.polyu.edu.hk/gs/ug-research/uris/approved-projects/)

---

## Publications

> [!IMPORTANT]
> Two papers currently under review at **ACM MM 2026** and **KDD 2026** — both A* / A-ranked venues in their respective fields.

**CCD-VQA: Benchmark Construction and Evaluation for Traffic Circumstances Understanding in Multimodal Large Language Models**
Zhou Letian, **Haochen Shi**, Wei Lou
***ACM International Conference on Multimedia (ACM MM) 2026 — Under Review***

199 accident videos (filtered from 1,500 via YOLOv8 kinematic analysis), 1,194 QA pairs across six dimensions: Weather/Light, Traffic Environment, Road Configuration, Accident Type, Accident Cause, and Accident Prevention. Sentence-BERT controls distractor quality; a Benchmark Suitability Score (BSS) grounded in Item Response Theory suppresses random-guessing shortcuts. Key numbers: gemini-3.1-pro-preview reaches 77.55% overall; best open-source models cluster around 64% on perception — but all drop 20–25% on causal reasoning tasks (Q4–Q6), the "Perception-Reasoning Gap."

---

**SurveyLens: A Research Discipline-Aware Benchmark for Automatic Survey Generation**
Beichen Guo, Zhiyuan Wen, Gu Jia, Senzhang Wang, Ruosong Yang, Shuaiqi Liu, **Haochen Shi**
***ACM SIGKDD Conference on Knowledge Discovery and Data Mining (KDD) 2026 — Under Review***

Existing ASG benchmarks are biased toward CS and use generic metrics. SurveyLens-1k covers 10 disciplines (Biology, Business, CS, Education, Engineering, Environmental Science, Medicine, Physics, Psychology, Sociology) with 100 human-written surveys each. Evaluation uses discipline-aware rubric scoring (LLM-as-judge with Bradley-Terry preference-aligned weights) and canonical alignment metrics (RAMS + TAMS for content coverage and redundancy). Tested 11 methods; notable finding: Deep Research agents produce richer narratives but lose structural precision, while vanilla LLMs outperform specialised ASG systems in humanities fields.

---

## Research

### Multimodal LLM-Based Home Environment Interaction System
> **Role:** Sole developer &nbsp;|&nbsp; **Scheme:** URIS, PolyU

> [!NOTE]
> **URIS Selection:** 100 awardees selected university-wide across all faculties. Only **5–6 CS students** were matched with a CS-track supervisor in this cohort. Research output includes **two LoRA adapters published on Hugging Face**.

The core question: does keeping the VLM out of the loop for most frames (YOLOv8 + tracker for object state, Qwen2.5-VL called only on demand) give better latency and more interpretable failures than querying end-to-end? Built this to find out.

**Architecture**

| Layer | Component | Role |
|-------|-----------|------|
| Perception | YOLOv8 + pluggable tracker | Real-time object detection; adapter-ready for ByteTrack / OC-SORT |
| Memory | Object Registry | Temporal event log tracking count changes and scene stability transitions |
| Dialogue | Reference Resolver | Spatial and ordinal disambiguation with automatic clarification on ambiguity |
| Reasoning | Qwen2.5-VL (on-demand) | Per-query invocation with prompt caching and Fast Mode for latency control |
| Evaluation | Evaluation Lab | Structured JSON output: `json_valid_rate`, `clarification_rate`, `reference_resolution_rate`, `cache_hit_rate` |

**Research Questions**
1. Whether a layered detector-tracker-VLM pipeline achieves lower latency and higher interpretability than end-to-end VLM querying.
2. Whether temporal memory improves reference resolution accuracy in multi-turn dialogue.
3. Whether prioritising clarification requests over speculative answers reduces hallucination rate.

**Fine-tuning:** Two LoRA adapter variants — `Qwen2.5-VL-URIS-Final-LoRA` and `Qwen2.5-VL-URIS-Predictive-LoRA` — trained on domain-specific home environment instruction data and published on Hugging Face.

`Python` `Qwen2.5-VL` `YOLOv8` `OpenCV` `PyTorch` `HuggingFace PEFT` `Streamlit`

---

## 🌟 Featured Project

> [!IMPORTANT]
> **PolyInterview** is a PolyU institutional project supervised by the university's **Vice President**.

### **PolyInterview — AI-Powered Mock Interview Platform**
> **Role:** Backend engineer &nbsp;|&nbsp; **Affiliation:** PolyU Key Project &nbsp;|&nbsp; [Repository ↗](https://github.com/ACCFOOL/PolyInterview)

The platform generates interview questions from a job description, runs a lip-synced digital avatar over WebRTC, and scores the candidate's responses using SKTE/FABE. I did the backend: schema design, auth, TTS pipeline, and speech scoring.

**System Architecture**

![PolyInterview Architecture](https://raw.githubusercontent.com/HaochenSHI66/HaochenSHI66/main/polyinterview-architecture.png)

**Core Technical Challenges**

| Challenge | Solution |
|-----------|----------|
| Real-time avatar synchronisation | Async-pipelined TTS → Wav2Lip → WebRTC to minimise end-to-end latency for a live interview feel |
| Structured evaluation from LLM output | Prompt-engineered JSON schema constraints for SKTE/FABE scoring with fallback parsing for partial outputs |
| Multi-engine TTS consistency | Tone-parameter normalisation layer to preserve voice identity when switching between EdgeTTS and GPT-SoVITS |

**Contributions:** Relational schema design (SQLite) · Full auth and session management · TTS tone-selection pipeline · Speech evaluation module aligned with SKTE framework

`Python` `Flask` `Vue.js` `SQLite` `OpenAI API` `DashScope` `LiveTalking` `Wav2Lip` `WebRTC` `EdgeTTS` `GPT-SoVITS`

---

## Projects

### 🎓 Teaching-Learning — AI Slide Lecture Assistant
> **Role:** Sole developer

Upload a slide deck, get page-by-page explanations in a split-screen view. One Qwen model reads the visual layout and diagrams, another generates the explanation text. Prior-slide summaries are passed forward so the explanation stays coherent across a long deck. No cloud VM, just Cloudflare Tunnel.

**System Architecture**

![Teaching-Learning Architecture](https://raw.githubusercontent.com/HaochenSHI66/Teaching-Learning-v/main/docs/architecture.png)

**Core Technical Challenges**

| Challenge | Solution |
|-----------|----------|
| Dual-pipeline VLM coordination | Vision model extracts visual structure per slide; text model synthesises cross-slide narrative using accumulated prior-slide summaries passed as context |
| Scalable generation on long decks | Per-slide result persistence in SQLite (WAL) enables incremental caching and resumable full-document generation without redundant API calls |
| Zero-infrastructure public deployment | Cloudflare Tunnel routes public HTTPS traffic to the local FastAPI server, handling WebSocket connections and large file uploads without a cloud VM |

`Next.js 15` `React 19` `TypeScript` `FastAPI` `SQLite (WAL)` `Qwen-VL` `Qwen-Chat` `Tailwind CSS` `Cloudflare Tunnel`

---

### 📓 SmartJournal — AI-Powered Diary and Scheduler
> **Role:** Sole developer

Diary app for iOS/macOS where you write what you're planning and GPT-4o turns it into calendar events. The tricky parts: resolving "next Tuesday afternoon" into an actual timestamp, and keeping state consistent when the device goes offline.

**Core Technical Challenges**
- Time expression parsing: handling relative expressions (e.g. "next Tuesday afternoon", "in two hours") with correct anchor resolution at query time
- Offline-first sync: local-first state management with Supabase, conflict resolution on reconnect

`React Native` `Expo` `TypeScript` `Supabase` `OpenAI GPT-4o`

---

### Other Projects

<table>
<tr>
<td width="50%" valign="top">

**📈 AI Investment Terminal**

US equity research terminal combining deterministic financial models, SEC/IR data, and LLM-assisted analysis in one place.

`Python` `Pandas` `Financial APIs`

</td>
<td width="50%" valign="top">

**🎮 Graph Gomoku AI**

Full-stack Gomoku with a Minimax and Alpha-Beta pruning engine, paired with real-time D3.js game-tree visualisation over WebSocket.

`Java` `Spring Boot` `React` `TypeScript` `D3.js`

</td>
</tr>
</table>

---

## Skills

<div align="center">

**Languages**

![Python](https://img.shields.io/badge/-Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![TypeScript](https://img.shields.io/badge/-TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Java](https://img.shields.io/badge/-Java-007396?style=for-the-badge&logo=openjdk&logoColor=white)
![C++](https://img.shields.io/badge/-C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![Go](https://img.shields.io/badge/-Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![SQL](https://img.shields.io/badge/-SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white)

**AI / ML**

![PyTorch](https://img.shields.io/badge/-PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![HuggingFace](https://img.shields.io/badge/-HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)
![YOLO](https://img.shields.io/badge/-YOLOv8-00FFFF?style=for-the-badge&logoColor=black)
![OpenCV](https://img.shields.io/badge/-OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![LangChain](https://img.shields.io/badge/-LangChain-1C3C3C?style=for-the-badge&logoColor=white)

**Full-Stack**

![React](https://img.shields.io/badge/-React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Next.js](https://img.shields.io/badge/-Next.js-000000?style=for-the-badge&logo=next.js&logoColor=white)
![Flask](https://img.shields.io/badge/-Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![Spring](https://img.shields.io/badge/-Spring-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![Node.js](https://img.shields.io/badge/-Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Docker](https://img.shields.io/badge/-Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

**Databases**

![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/-MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![SQLite](https://img.shields.io/badge/-SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)

</div>

---

## Contact

<div align="center">

📧 [haochen8.shi@connect.polyu.hk](mailto:haochen8.shi@connect.polyu.hk) &nbsp;·&nbsp; 🌐 [shc66.com](https://shc66.com) &nbsp;·&nbsp; 💻 [github.com/HaochenSHI66](https://github.com/HaochenSHI66)

*Open to summer research opportunities — drop me an email.*

</div>

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=100&section=footer)
