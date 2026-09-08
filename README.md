# MAGI System: Multi-Agent Ethical Debate Framework

**Automated Clinical Ethics Deliberation via Iterative Multi-Agent Consensus**

---

## 📌 Overview

This repository hosts the official implementation of the **MAGI Framework** (*Mitigation and Governance of AI in Healthcare*), an AI-powered multi-agent consensus system engineered to evaluate complex medical-ethical and intraoperative decision-making dilemmas.

When confronting high-stakes clinical scenarios, healthcare professionals must balance competing oncobiological imperatives, statutory legal requirements, and moral principles. This system simulates an interdisciplinary ethics committee by deploying specialized LLM agents (*personas*) that iteratively deliberate over a given clinical dilemma until mathematical consensus is reached or irreconcilable normative divergences are formally cataloged.

MAGI does **not** determine or prescribe clinical conduct; its objective is to serve as an **evaluative cognitive guardrail and criticality triage sentinel**, exposing ethical tensions and preventing passive **automation bias**.

---

## 📄 Scientific Preprint & Citation

Our methodology, multi-persona design, and experimental validation are detailed in our preprint submitted to **arXiv.org**:

> **MAGI System: A Multipersona Framework for Ethical Deliberation and Criticality Triage in Clinical Decision-Support Guardrails**
> *Gerson Hiroshi Yoshinari Júnior*
> Preprint submitted to arXiv.org.
> **arXiv Identifier / DOI:** `[PENDENTE: ADICIONAR DOI / LINK ARXIV APÓS APROVAÇÃO]` 

### BibTeX Citation

```bibtex
@article{yoshinari2026magi,
  title={MAGI System: A Multipersona Framework for Ethical Deliberation and Criticality Triage in Clinical Decision-Support Guardrails},
  author={Yoshinari J{\'u}nior, Gerson Hiroshi},
  journal={arXiv preprint},
  year={2026},
  note={DOI: [PENDING - INSERT DOI HERE]}
}

```

---

## 🧠 Cognitive Engine: Strategic Reasoning Architecture

The deliberative engine operates on advanced reasoning models (such as **GPT-5.6-Terra** / **GPT-5.6-Luna**) configured with native intermediate reasoning effort (`reasoning_effort="medium"` / `reasoning={"effort": "medium"}`).

### Impact on Deliberative Quality

* **Argumentative Depth Without Premature Concession:** Requiring intermediate reasoning forces agents to execute internal chains of thought before generating output tokens. Consequently, the Biologist, Jurist, and Moralist formulate rigorous domain arguments without collapsing into superficial compromises.


* **Semantic Rigor in Content Analysis:** Category extraction and convergence metrics require high semantic precision. Enhanced reasoning enables the Coordinator to reliably identify subtle thematic conflicts and compute convergence scores.


* **Balance Between Latency and Cost:** The *medium* reasoning parameter provides an optimal balance for multi-round workflows (up to 5 rounds), preserving deep analytical rigor while maintaining execution efficiency.



---

## 🔬 Theoretical and Methodological Foundations

```
+-----------------------------------------------------------------------------------+
|               CLINICAL INPUT: DEONTOLOGICAL NORMALIZATION                         |
|                 Auto-prefix: "Is it ethical to [case narrative]..."               |
+-----------------------------------------------------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|              MAGI MULTIPERSONA GUARDRAIL (Medium Reasoning Effort)                |
|                                                                                   |
|    +--------------------+   +--------------------+   +--------------------+       |
|    |   Legal Persona    |   | Religious Persona  |   | Biological Persona |       |
|    |      (Jurist)      |   |     (Moralist)     |   |    (Biologist)     |       |
|    +--------------------+   +--------------------+   +--------------------+       |
|              \                       |                       /                    |
|               v                      v                      v                     |
|        +----------------------------------------------------------+               |
|        |     Coordinator: Bardin Content Analysis & Scoring       |               |
|        |  JSON: {themes, convergence_score, justification,        |               |
|        |         round_summary}                                   |               |
|        +----------------------------------------------------------+               |
+-----------------------------------------|-----------------------------------------+
                                          |
                        Is Convergence Score >= 80%?
                                          |
                     +--------------------+--------------------+
                     |                                         |
               YES (<= 2 rounds)                         NO / Tardy (> 2 rounds)
                     |                                         |
                     v                                         v
       +----------------------------+            +----------------------------+
       |   ALERT LEVEL 1: LOW       |            |   ALERT LEVEL 2 / 3        |
       | Unified Consensus Report   |            | Paused / Mandatory Lockout |
       | Routine Human Verification |            | Divergence Report Generated|
       +----------------------------+            +----------------------------+
                                                               |
                                                               v
                                                 +----------------------------+
                                                 | EXCLUSIVE HUMAN COMMITTEE  |
                                                 |        DELIBERATION        |
                                                 +----------------------------+

```

### 1. Specialized Persona Agents (Co-Designed with Domain Experts)

* **Biological Analyst (`Biologist`):** Co-designed with biological science expertise. Evaluates the dilemma strictly through oncobiology, cellular survival, tissue preservation, systemic homeostasis, and evolutionary physiological dynamics.


* **Legal Consultant (`Jurist`):** Co-designed with healthcare law expertise. Focuses on medical law, legal certainty, statutory compliance, patient autonomy, informed consent, and civil/criminal liability mitigation.


* **Ethical-Moral Analyst (`Moralist`):** Co-designed with bioethics and theological counseling. Grounded in personalist bioethics and natural law, advocating for the intrinsic dignity of the human person and the inviolability of conscience.



### 2. Bardin's Thematic Analysis & Convergence Metric

* Following each round, the automated **Coordinator Agent** processes the responses through Laurence Bardin's qualitative content analysis.


* A strict JSON object is extracted containing categorical themes, qualitative friction justifications, and a normalized **Convergence Score** ($0\% \text{ to } 100\%$):
```json
{
  "themes": ["Cellular Survival", "Patient Autonomy", "Statutory Compliance"],
  "convergence_score": 45,
  "justification": "Irreconcilable conflict between life-saving intervention and advance refusal.",
  "round_summary": "Biologist urges emergency intervention; Jurist and Moralist mandate honoring refusal."
}

```



### 3. Iterative Consensus Loop

* **Convergence $\ge 80\%$:** Consensus is reached. The Coordinator concludes deliberation and generates the **Unified Consensus Report**.


* **Convergence $< 80\%$:** The Coordinator injects the `round_summary` and previous transcripts back into the persona context for iterative counter-rebuttals (up to 5 rounds).


* **Lack of Consensus after 5 rounds:** Deliberation terminates, generating the **Divergence Report**, documenting irreducible moral conflicts for clinical ethics review.



### 4. Relational Persistence and Auditability

All interactions, intermediate themes, and convergence metrics are logged in a local SQLite database (`magi_debate_workflow.db`) across three dedicated relational tables (`Sessions`, `Round_Deliberations`, and `Coordinator_Analyses`) ensuring complete traceability.

---

## 🛡️ Ethical Governance: *Human-on-the-Loop* (HOTL) & Safeguards

### 1. Human Dignity & Automation Bias Mitigation

As AI reasoning achieves higher coherence, healthcare providers face **automation bias**—the tendency to place uncritical trust in algorithmically flawless arguments and passively delegate final moral decisions. The **Human-on-the-Loop (HOTL)** design ensures that the system serves as an advisory consultation body, never replacing human moral and clinical agency.

### 2. Graduated Alert Levels & Mandatory Dual Verification

MAGI stratifies deliberative complexity into actionable escalation levels:

| Alert Level | Operational Criteria | Framework Action & Requirement |
| --- | --- | --- |
| **Level 1 Alert (Low)** | Rapid consensus ($\ge 80\%$) achieved within 2 rounds

 | Generates Unified Consensus Report with full audit trail for routine human sign-off.

 |
| **Level 2 Alert (Medium)** | Late consensus (rounds 3 to 5) with polarity shifts

 | **Deliberation Pause**: Graphical display of points of friction prior to final synthesis.

 |
| **Level 3 Alert (Critical)** | Absence of consensus after 5 rounds (impasse)

 | **Mandatory Lockout**: Prohibits automated resolution; requires exclusively human multidisciplinary ethics committee deliberation.

 |

> While other autonomous architectures delegate dual verification to adversarial secondary models, in the MAGI framework **critical-tier validation is strictly human**.
> 
> 

### 3. Asynchronous Multilayer *Killswitch* Architecture

Operational safety requires an engineered contingency shutdown architecture:

* **Software Layer:** Asynchronous, non-blocking background thread (`asyncio` loop running in a dedicated `threading.Thread`). Triggering the killswitch sets an `abort_event` and invokes threadsafe cancellation (`loop.call_soon_threadsafe(task.cancel)`), terminating in-flight API requests immediately.


* **Persistence Layer:** Immediately commits the session state in SQLite as `status: FORCED_ABORT_BY_HUMAN` and `alert_level: DIRECT INTERVENTION (KILLSWITCH)`.


* **100% Human Transition:** Halting the deliberative pipeline transfers the entire chronological argument history to the human medical committee, preserving data integrity and human clinical sovereignty.



---

## 🚀 Getting Started

### Prerequisites

* Python 3.10+
* OpenAI API Key

### Installation

```bash
git clone https://github.com/ghyoshinari/magi_debate.git
cd magi_debate
pip install openai ipywidgets

```

### Environment Configuration

Configure your OpenAI API key in your environment or via Google Colab Secrets under the name `OPENAI_API_DEBATE`:

```bash
export OPENAI_API_DEBATE="your-api-key-here"

```

### Usage

1. Open and execute the notebook in Google Colab or Jupyter Notebook.


2. Input the clinical dilemma into the interactive widget.


> *Note:* Queries are automatically normalized with the deontological prefix *"Is it ethical to..."* if omitted.
> 
> 


3. Monitor deliberation rounds, thematic scores, and HOTL alert banners in real time.


4. Use the **🛑 KILLSWITCH** button at any time to immediately interrupt automated processing and transition the dilemma to human staff.



---

## ⚖️ License

This project is licensed under the **Apache License, Version 2.0**. See the [LICENSE](https://www.google.com/search?q=LICENSE) file for details.

```text
Copyright 2026 Gerson Hiroshi Yoshinari Júnior

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

```
