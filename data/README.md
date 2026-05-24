# `data/` — corpus directory

Anything dropped in `sample_docs/` is fair game for ingestion via:

```bash
uv run python scripts/ingest.py
```

Supported file types: `.pdf`, `.txt`, `.md`, `.markdown`, `.rst`.

## What ships in `sample_docs/`

A small, hand-authored corpus designed for the Workshop 8 demo. Together
these documents exercise all three loader paths (`.md`, `.txt`, `.pdf`),
give the retriever multiple distinct topics to disambiguate between, and
contain at least one deliberate gap so students can show the system saying
"I don't know" when asked outside the corpus.

| File | Format | Topic | Good demo question |
|------|--------|-------|--------------------|
| `rag_primer.md` | md | What RAG is and why it exists | "What is RAG?" |
| `chromadb_overview.txt` | txt | ChromaDB internals, persistence | "How does ChromaDB persist data?" |
| `embeddings_explained.md` | md | Dimensions, cosine vs L2 | "Why use cosine similarity over L2?" |
| `prompt_design_notes.md` | md | Grounded prompting patterns | "How do you reduce hallucination in RAG?" |
| `evaluation_basics.md` | md | How to evaluate a RAG system | "How should I evaluate retrieval?" |
| `rag_paper_summary.pdf` | **pdf** | Lewis et al. 2020 RAG paper, summarised | "What did the original RAG paper contribute?" |
| `apache_foundation_faq.md` | md | Apache Software Foundation FAQ (illustrative) | "How is the Apache Software Foundation governed?" |

All content is hand-written for this repo — no third-party redistribution.

### Suggested demo arc (Workshop 8)

1. **Ingest** the whole corpus: `uv run python scripts/ingest.py --clear`.
2. **One that works well.** Ask *"What is RAG?"* — the answer pulls from
   `rag_primer.md` and `rag_paper_summary.pdf`. Show the sources panel.
3. **Show the sliders matter.** Drop `top_k` to 1 in the UI, ask again.
   Push it to 8, ask again. The answer changes visibly.
4. **Show metadata variety.** Ask a question about the Apache Foundation —
   sources should come almost entirely from `apache_foundation_faq.md`.
   This proves retrieval is *selective*, not just "throw everything in."
5. **Failure mode.** Ask *"Who won the 2026 World Cup?"* — corpus is
   silent. Per the prompt template, the model should decline rather than
   hallucinate. This is the punchline of the workshop.

## Adding your own documents

```bash
cp ~/papers/my-paper.pdf data/sample_docs/
uv run python scripts/ingest.py --clear     # re-index from scratch
uv run python scripts/query.py "what does the paper say about X?"
```

> **Storage:** embeddings live in `.chroma/` at the repo root. That directory
> is git-ignored. Delete it any time to start fresh — the next ingest run
> rebuilds it.
