<p align="center">
  <img src="https://img.shields.io/badge/JoulePlan-Drop--in%20OpenAI%20proxy-e63946?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTIwIDEyMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cmVjdCB3aWR0aD0iMTIwIiBoZWlnaHQ9IjEyMCIgcng9IjI2IiBmaWxsPSIjZTYzOTQ2Ii8+PHRleHQgeD0iNjAiIHk9IjgyIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJ3aGl0ZSIgZm9udC1mYW1pbHk9InN5c3RlbS11aSIgZm9udC13ZWlnaHQ9IjgwMCIgZm9udC1zaXplPSI2MCIgbGV0dGVyLXNwYWNpbmc9Ii0zIj5KUDwvdGV4dD48L3N2Zz4=&logoColor=white" alt="JoulePlan" />
</p>

<h3 align="center">Cut your AI agent bills by 5-10x. No code changes.</h3>

<p align="center">
  JoulePlan is a drop-in OpenAI-compatible proxy that picks the cheapest model and reasoning depth for every request. Same answers, a fraction of the cost.
</p>

<p align="center">
  <a href="https://jouleplan.com">Website</a> &middot;
  <a href="https://jouleplan.com/docs.html">Docs</a> &middot;
  <a href="https://jouleplan.com/research.html">Research</a> &middot;
  <a href="https://github.com/jouleplan/python-sdk">Python SDK</a>
</p>

---

### Quick start

```python
from jouleplan import JoulePlan

client = JoulePlan(api_key="jp-...")

# Easy question -> small model, one call
client.complete("What is 2+2?")
# routed_model: qwen2.5-1.5b   |   savings: 98%

# Reasoning task -> mid model, step-by-step
client.complete("Janet's ducks lay 16 eggs/day. She uses 7 and sells the rest...")
# routed_model: qwen2.5-7b     |   savings: 87%

# Formal proof -> frontier model
client.complete("Prove that sqrt(2) is irrational by contradiction")
# routed_model: claude-sonnet-4-6   |   savings: 44%
```

### How the router decides

Every request goes through a two-step decision:

1. **Which model?** JoulePlan reads the prompt, estimates difficulty, and picks the smallest model that can answer it well. The pool spans 7 models: four self-hosted Qwen instances (1.5B -> 32B) and three cloud frontier models (GPT-4o Mini, GPT-4o, Claude Sonnet 4.6).
2. **What reasoning depth?** For each picked model, JoulePlan decides whether a direct answer is enough, or whether step-by-step reasoning, self-consistency, or a multi-step agent loop will be worth the extra tokens.

Every response includes the routing decision, the dollar cost, and how much you saved vs. running the request through the heaviest available setup.

### Backed by published research

JoulePlan's routing decisions are grounded in measured benchmarks, not heuristics. The papers below cover the methodology and findings the product is built on:

| Paper | Key Finding |
|-------|-------------|
| **AgentEnergy** | Agentic workflows waste 3-5x more compute than a single LLM call on the same prompt |
| **EnergyBench-Agentic** | Bandit routing matches the heaviest setup's quality at 63% less cost |
| **CoT Cost Waste** | Chain-of-thought reasoning wastes 4-8x compute on easy tasks |
| **Graph-BwK Theory** | Side-observation graphs cut routing-policy learning time by sqrt(K) |
| **Where the Joules Go** | 40-70% of "reasoning tokens" in long-context models are non-productive |
| **Scalarization Collapse** | Linear weighting of quality+cost reliably fails; you need a hard budget instead |

Full benchmarks and methodology at [jouleplan.com/research](https://jouleplan.com/research.html).

### Repositories

| Repo | Description |
|------|-------------|
| [**python-sdk**](https://github.com/jouleplan/python-sdk) | Python SDK for the JoulePlan API. Zero dependencies, OpenAI drop-in. |

---

<p align="center">
  <sub>Built at Queen's University, Canada</sub>
</p>
