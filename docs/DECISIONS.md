# Decisions

## 2026-11-11
- **Topic:** translation error detection in English to Hebrew subtitles. Chosen over two other ideas (canon consistency in Harry Potter fan fiction, step-level error detection in math solutions) because real data exists for the correct pairs, Hebrew makes it novel, and it is easy to evaluate.
- **Solo project.**
- **Data source:** OpenSubtitles (OPUS) for correct pairs; errors injected by an LLM.
- **Error types (v1):** meaning error, literal idiom, omission, wrong tone.
- **Size (v1):** ~6,000 pairs, ~150 hand-labeled real pairs for testing.
- **Scope:** single line, no scene context. Context-dependent wordplay is out of scope.
