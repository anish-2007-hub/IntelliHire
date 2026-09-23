# IntelliHire

**An interview agent that reasons.**

> Same candidate. Two interviewers. Two completely different verdicts.

🔗 **Live demo:** https://anish-2007-hub.github.io/IntelliHire/

IntelliHire is an AI-driven HR platform that reads a job description and a candidate's resume, drafts the questions the role actually needs answered, scores every response against that role's rubric, and then reasons across past interviews and hiring policy before recommending anything, including which of two candidates to hire.

---

## The Problem

Most AI interview tools ask a preset list of questions and transcribe the answers. They have no judgment and no memory of what a rubric, a policy, or an earlier round already established. So two interviewers can sit across the same candidate and walk away with different verdicts, and neither can point to why.

## The Solution

IntelliHire is one agent, not a form. It reasons jointly over:

- the **job description**
- the candidate's **resume**
- **prior interview notes**
- the company's **hiring policy**

It generates questions from that context, scores answers against the role's actual rubric, and turns the result into a recommendation with a trail back to the evidence that produced it.

## Features

- **Role-specific question generation:** questions come from the JD, resume, and policy, not a fixed script.
- **Rubric-based scoring:** every response is scored (out of 5) per competency, with a short justification.
- **Adaptive follow-ups:** when an answer stays theoretical or repeats a gap flagged in an earlier round, IntelliHire asks a targeted follow-up instead of scoring around it.
- **Cross-source reasoning:** combines the JD, resume, this interview, hiring policy, and prior rounds into one recommendation.
- **Explainable recommendations:** each verdict lists the evidence behind it, source by source.
- **Candidate comparison:** lines up two candidates on the same rubric and recommends who to hire for the requisition, and why.

## Demo Walkthrough

The live demo includes one requisition (**ENG-1042, Senior Backend Engineer, Payments Platform**) and two candidates:

| Competency                  | Priya Nair | Arjun Verma |
| --------------------------- | :--------: | :---------: |
| Distributed systems design  |    5/5     |     4/5     |
| Incident ownership          |    4/5     |     2/5     |
| Data consistency trade-offs |    3/5     |     5/5     |
| Stakeholder communication   |    4/5     |     3/5     |

**Try it:**

1. Open a candidate's interview file.
2. Click **Generate interview questions**.
3. Click **Evaluate responses against rubric**.
4. Click **Run cross-source reasoning** to get a recommendation.
5. Evaluate both candidates, then click **Compare Priya and Arjun**.

**Outcome:** IntelliHire recommends **Priya Nair**. Arjun is the sharper answer on consistency trade-offs, but the policy makes owned incident experience non-negotiable at the senior level, and only Priya has owned one end-to-end.

## How It Works

| Stage       | What happens                                                                                                                     |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **Input**   | Job description, resume, past interview notes, hiring policy, live transcript.                                                   |
| **Process** | Generate role-specific questions, evaluate each response against the rubric, then reason jointly across every source and candidate. |
| **Output**  | One structured insight and one recommended next step, with a trail back to the evidence, on the recruiter's dashboard.           |

## Architecture

Built to ship, not to retrain a model:

- **Frontend:** React interview console and recruiter dashboard
- **Orchestration:** Node.js (Express) / FastAPI
- **Reasoning:** LLM agent for scoring and recommendations
- **Data:** PostgreSQL + pgvector for the JD, resume, and policy context

> Note: the hosted demo is a front-end prototype using sample data. The stack above describes the intended production architecture.

## Running Locally

The demo is a static site, so no build step is needed.

```bash
git clone https://github.com/anish-2007-hub/IntelliHire.git
cd IntelliHire

# open index.html directly, or serve it locally:
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Project Structure

```
IntelliHire/
├── index.html      # Demo page
└── README.md
```

*(Update this to match your actual files.)*

## Roadmap

- Connect the interview console to a live LLM reasoning agent
- Persist requisitions, resumes, and policies in PostgreSQL + pgvector
- Live transcript capture during interviews
- Recruiter dashboard with per-requisition history
- Support for comparing more than two candidates

## Contributing

Issues and pull requests are welcome. For larger changes, please open an issue first to discuss what you would like to change.

## License

Add a license of your choice (e.g. MIT) before publishing.

## Author

**Anish** · [@anish-2007-hub](https://github.com/anish-2007-hub)
