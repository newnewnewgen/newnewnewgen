# Hi, I'm Newgen

I build tools that help people navigate high-stakes moments in their careers. I'm passionate about product management, AI-powered workflows, and creating software that puts humans in the loop where it matters most.

---

## Featured Project: UltimateResume

**An AI-powered resume generation platform that optimizes for both ATS parsing and hiring manager intent.**

Most resume tools stop at keyword stuffing. UltimateResume takes a fundamentally different approach: it semantically matches your real work accomplishments to job requirements, generates targeted bullet points, and rewrites them with hiring manager psychology in mind — all with you in the driver's seat at every critical decision.

### Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | Next.js 16, React 19, TypeScript, Tailwind CSS v4, Tiptap rich text editor |
| **Backend** | FastAPI (Python), Pydantic data validation, async API design |
| **AI/ML** | Google Gemini 2.5 Flash + Pro, Gemini Embedding API, hybrid vector matching |
| **Database** | Supabase (PostgreSQL) with Row-Level Security, Supabase Auth (SSR) |
| **Deployment** | Vercel (frontend), Railway (backend API), Supabase (managed DB + auth) |
| **Export** | LaTeX-based professional resume templates |

### How It Works

The platform runs a 9-step intelligent pipeline:

1. **Ingest** your activity bank (CSV/JSON with Situation-Action-Impact format) and existing resume
2. **Analyze** the target job description to extract required skills and hiring intent signals
3. **Generate dual rubrics** — an ATS keyword rubric and a hiring intent rubric
4. **Match** your activities to job requirements using hybrid vector scoring (55% semantic similarity + 30% keyword overlap + 15% context relevance)
5. **You review and select** the best matches from the top candidates (human-in-the-loop)
6. **Generate** polished S-T-I bullet points with parallel processing (8-worker thread pool)
7. **Assemble** the ATS-optimized resume from your template
8. **Rewrite for intent** — you guide a final pass that aligns tone and narrative to hiring manager psychology
9. **Export** the finished resume

### Key Engineering Decisions

- **Hybrid matching over pure semantic search.** Combining embeddings with keyword overlap and domain context avoids the "coherent nonsense" problem where semantically similar but irrelevant matches surface.
- **Human-in-the-loop at two critical points.** Automated AI is great for scale, but match selection (step 5) and narrative tone (step 8) benefit from human judgment. The system presents options; you decide.
- **Dual-model AI strategy.** Gemini Flash handles fast extraction and JSON-structured tasks. Gemini Pro handles high-quality writing. Each model is used where its strengths matter.
- **Stateful pipeline sessions.** Pipeline state persists in Supabase, so you can pause and resume at any step across sessions.
- **Shared core logic.** Both the Streamlit prototype and the production FastAPI backend consume the same core modules (models, AI engine, vectorizer), reducing duplication and ensuring consistency.

### Architecture

```
Frontend (Next.js / Vercel)
    |
    v
FastAPI Backend (Railway)
    |
    +-- core/models.py        14 Pydantic data classes
    +-- core/ai_engine.py     Gemini API integration (1,700+ LOC)
    +-- core/vectorizer.py    Embedding + hybrid matching (380+ LOC)
    +-- core/pipeline.py      Step orchestrator
    +-- prompts/templates.py  18 structured prompt templates
    |
    v
Supabase (PostgreSQL + Auth)
```

---

*Building things to help others — one pipeline at a time.*
