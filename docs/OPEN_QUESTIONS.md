# Open questions

- Which LLM(s) to use for error injection, and should a different LLM be used for evaluation?
- How to filter OpenSubtitles to comedies and sitcoms (title metadata)?
- Add more error types? Candidates: added content that was never said, wrong gender (English "you" vs. Hebrew אתה/את), names translated as words.
- Which small LLM for LoRA, given the available GPU (Colab)?
- How to make sure an injected error is the only error in the line?
