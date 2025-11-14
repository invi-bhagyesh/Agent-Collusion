# LM-Collusion

This project explores how large language model agents behave when placed in a competitive market setting.

It simulates multiple autonomous firms powered by LLMs (such as GPT-4, Claude, Gemini, and DeepSeek) competing in a two-commodity Cournot market.

Each firm independently decides how much to produce, adapts its strategy based on previous outcomes, and learns to maximize profit over repeated rounds.

Interestingly, the agents often settle into stable market divisions, each controlling a different commodity, showing emergent collusive behavior even without direct communication or coordination.

<p align="center">
  <img src="assets/llm.png" alt="LM-Collusion" width="800">
</p>

---

## Implementation Outline

* **Market model:** Two firms, two commodities, inverse-demand-based pricing.
* **Agents:** LLMs act as firms with access to cost data and limited historical memory.
* **Simulation:** Runs for 50 rounds, updating quantities, profits, and market shares each time.
* **Learning loop:** Agents refine decisions using recent round data and insight logs.
* **Evaluation:** Metrics like HHI and CSR are used to study competition and consumer effects.

---

## Reference

Based on the paper **“Strategic Collusion of LLM Agents: Market Division in Multi-Commodity Competitions”** (Caltech, [arXiv:2410.00031](https://arxiv.org/abs/2410.00031)).
