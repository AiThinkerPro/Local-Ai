# Making money with a Mac mini M4 Pro (48 GB): research and recommendations
_Researched 2026-11-13_

## What the hardware actually does (community benchmarks)
| Model type | Example | Speed on M4 Pro 48 GB | Verdict |
|---|---|---|---|
| MoE ~30B (3B active) | Qwen3-30B-A3B / Qwen3-Coder-30B-A3B (MLX 4-bit) | ~35–70 tok/s | **Best fit: fast and capable** |
| Dense 32B | Qwen2.5-32B Q4 | ~11–25 tok/s | Usable for batch, slow for chat |
| Dense 70B | Llama 3.3 70B Q4 | ~11–14 tok/s, ~43 GB of weights | Barely fits, little room for context, avoid |
| Whisper large-v3 / turbo | transcription | many times faster than real time | Strong |

## What people tried and how it went
1. **Renting out compute (Darkbloom, etc.):** top-50 earners' median was about $5/day. Projections after token price cuts are about $1.23/day. **Not worth it.**
2. **Selling raw LLM API/tokens:** a single Mac can't beat cloud prices or uptime. **Avoid.**
3. **Private / on-prem AI for small professional firms (law, accounting, clinics):** many vendors sell this at $5K–$10K per install. Job posts ask for a "Mac mini + Ollama + n8n + AnythingLLM" setup at about $500 for small jobs. **Real demand.**
4. **Batch services (transcription, document extraction, translation, subtitles):** people moved Whisper work onto local Mac minis to save money. Speed doesn't matter when jobs run overnight. **Good fit.**
5. **Local automation agencies (n8n + local LLM):** freelancers charge $50–$150 per small automation, more on retainer. **Viable, low barrier.**

## Recommendations
- **#1 Private AI setup + retainer for small firms.** Use your Mac as the demo and build lab. Sell outcomes such as "chat with your client files, nothing leaves the office". Price around $1.5K–$5K for setup plus $150–$400/month for support. The client buys their own Mac mini.
- **#2 Overnight batch-processing service.** Offer transcription, summaries, PDF/invoice to spreadsheet, or translation. Charge per hour of audio or per document. Your marginal cost is close to zero.
- **#3 Hybrid content/automation pipeline.** Do bulk drafting and classification locally, and send only the final polish to a cloud API.

## Fixing speed and reliability
- Use **MLX** (LM Studio or oMLX) with **Qwen3-30B-A3B 4-bit** as the default. Use dense 32B only for batch work, and don't use 70B.
- Raise the GPU memory limit: `sudo sysctl iogpu.wired_limit_mb=40960`.
- Keep context to 8–32K tokens and use RAG instead of huge prompts.
- Treat the model as a job queue, not a chat. Use structured JSON output, validation, and retries, and fall back to a cloud API on failure.
- Keep the Mac awake for 24/7 jobs (`caffeinate`, or Energy settings > prevent sleep).

## 30-day validation plan
- Week 1: build one demo, for example "ask questions over 500 PDFs" plus a transcription pipeline.
- Week 2: contact 30 local accountants, lawyers, or clinics, or post on the n8n community job board and Upwork.
- Weeks 3–4: deliver 1–2 paid pilots. Double down on whatever someone paid for.
