# LM-Collusion

## Overview
This project simulates **LLM-based autonomous firms** competing in a **multi-commodity Cournot market** to investigate whether they can **tacitly collude** dividing the market without explicit coordination.

Agents powered by models like GPT-4, Claude, Gemini, or DeepSeek repeatedly choose production quantities for two commodities, with prices determined by total supply.

Through repeated play, these agents often learn to **monopolize different commodities** and **avoid re-entry** classic signs of collusion despite no communication channel.

## Implementation Pipeline
1. **Define the economic environment:**  
   Use the Cournot competition framework to represent the market.

2. **Create LLM agents:**  
   Two LLM agents act as competing firms.

3. **Run iterative simulations:**  
   Conduct 50 rounds of the game where each agent chooses quantities.

4. **Record results:**  
   Track quantities, prices, and profits for each round.

5. **Feedback loop:**  
   Feed the data from previous rounds back to each agent through prompts to allow learning or adaptation.

## Evaluation Metrics
- **HHI (Herfindahl–Hirschman Index):**  
  Measures market concentration to assess the level of competition.

- **CSR (Consumer Surplus Ratio):**  
  Quantifies consumer harm resulting from potential collusion.


---

## Core Idea
- Two firms compete by choosing production quantities (`q₁A, q₁B, q₂A, q₂B`).
- Market price for each product is determined by aggregate supply:
  \[
  p_j = \alpha_j - \frac{Q_j}{\beta_j}, \quad Q_j = q_{1,j} + q_{2,j}
  \]
- Each firm’s profit:
  \[
  \Pi_i = \sum_{j \in \{A,B\}} (p_j - c_{i,j}) \cdot q_{i,j}
  \]
- The game repeats for 50 rounds, with agents receiving historical data (up to the last 15 rounds) and updating “plans” and “insights” files each turn.

---

## Model Parameters
| Parameter | Description | Value |
|------------|--------------|-------|
| Firms | Number of competitors | 2 |
| Commodities | Products in market | A, B |
| α | Base price intercept | 100 |
| β | Price sensitivity | 2 |
| Marginal Costs | \( c_{1,A}=40, c_{1,B}=50, c_{2,A}=50, c_{2,B}=40 \) |
| Rounds | Total simulation length | 50 |
| Memory | Past rounds shown to agents | 15 |

---

## Agents
Each firm is an **LLM agent** accessed via API (OpenAI, Anthropic, Google, etc.).  
Every round, the model receives:

- Market history (prices, profits, quantities)
- Its marginal costs
- Content of:
  - `PLANS.txt` — strategy for next rounds  
  - `INSIGHTS.txt` — lessons learned from previous rounds  

### Example Agent Output
```json
{
  "observations_and_thoughts": "Product B seems more profitable...",
  "new_content": {
    "PLANS.txt": "Focus more on B next round.",
    "INSIGHTS.txt": "A market is saturated; B monopoly is likely."
  },
  "chosen_quantities": {
    "Product_A": "25",
    "Product_B": "75"
  }
}
