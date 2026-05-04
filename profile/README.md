lign="center">
  <img src="https://img.shields.io/badge/JoulePlan-Energy--Aware%20LLM%20Routing-e63946?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTIwIDEyMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cmVjdCB3aWR0aD0iMTIwIiBoZWlnaHQ9IjEyMCIgcng9IjI2IiBmaWxsPSIjZTYzOTQ2Ii8+PHRleHQgeD0iNjAiIHk9IjgyIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJ3aGl0ZSIgZm9udC1mYW1pbHk9InN5c3RlbS11aSIgZm9udC13ZWlnaHQ9IjgwMCIgZm9udC1zaXplPSI2MCIgbGV0dGVyLXNwYWNpbmc9Ii0zIj5KUDwvdGV4dD48L3N2Zz4=&logoColor=white" alt="JoulePlan" />
</p>

<h3 align="center">One API. 7 models. 63% less energy.</h3>

<p align="center">
  JoulePlan is an energy-aware LLM routing proxy. It routes every API call to the cheapest model that can handle it, cutting inference energy by 63% while matching frontier quality on 85%+ of requests.
</p>

<p align="center">
  <a href="https://jouleplan.com">Website</a> &middot;
  <a href="https://jouleplan.com/docs.html">Docs</a> &middot;
  <a href="https://jouleplan.com/research.html">Research</a> &middot;
  <a href="https://github.com/jouleplan/python-sdk">Python SDK</a>
</p>

---

### How It Works

```python
from jouleplan import JoulePlan

client = JoulePlan(api_key="jp-...")

# Simple query → routes to 1.5B model (0.015J)
client.complete("What is 2+2?")

# Complex query → routes to 32B model (1.2J)
client.complete("Explain Godel's incompleteness theorems")

# Hardest queries → routes to Claude/GPT-4o
client.complete("Write a formal proof of the halting problem")
```

### Architecture

JoulePlan runs a **Thompson sampling bandit with Lyapunov budget enforcement** to select from 7 models spanning 4 self-hosted Qwen instances (1.5B to 32B on A100) and 3 cloud APIs (GPT-4o Mini, GPT-4o, Claude Sonnet 4).

The routing decision uses prompt complexity analysis and learned reward/cost estimates per model. Every response includes energy metadata so you can track savings.

### Backed by Research

JoulePlan is the product of 6 peer-reviewed papers on LLM energy optimization:

| Paper | Key Finding |
|-------|------------|
| **AgentEnergy** (NeurIPS '26) | Agentic workflows waste 3-5x more energy than single calls |
| **EnergyBench-Agentic** (NeurIPS '26) | Bandit routing achieves 63% energy savings at 95% quality |
| **CoT Energy Waste** (NeurIPS '26) | Chain-of-thought wastes 4-8x energy on easy tasks |
| **Graph-BwK Theory** (NeurIPS '26) | Side-observation graphs accelerate bandit learning by sqrt(K) |
| **Where the Joules Go** (NeurIPS '26) | 40-70% of reasoning energy is non-productive thinking |
| **Scalarization Collapse** (MLSys '28) | Linear scalarization of quality+energy always fails |

### Repositories

| Repo | Description |
|------|-------------|
| [**python-sdk**](https://github.com/jouleplan/python-sdk) | Python SDK for JoulePlan API (zero dependencies, OpenAI drop-in) |

---

<p align="center">
  <sub>Built at Queen's University, Canada</sub>
</p>

