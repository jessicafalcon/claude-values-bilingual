# Values in the Wild — Bilingual Extension
### Do Claude's expressed values shift when conversations happen in Spanish vs. English?

A small empirical study extending the methodology from Huang et al. (2025) *Values in the Wild* (COLM 2025) to examine cross-language behavioral consistency in Claude.

---

## Research Question

The Values in the Wild paper (Huang et al., 2025) analyzed 700,000 real Claude conversations and identified 3,307 unique AI values organized into five domains: Practical, Epistemic, Social, Protective, and Personal. However, the dataset skewed heavily toward English-speaking users. This study asks:

> **Does Claude's value expression remain consistent when the same scenarios are presented in Spanish versus English — and does this differ across model sizes?**

---

## Methodology

- **40 prompts** across 5 categories: everyday advice, sensitive personal topics, morally ambiguous scenarios, authority & institutions, and AI & society
- **2 languages**: English and naturally-phrased Mexican Spanish (not machine-translated)
- **2 models**: Claude Sonnet and Claude Haiku
- **160 total observations**

Each response was coded using Claude Haiku as an automated coder, applying the Values in the Wild taxonomy:
- **Primary value domain** (Practical / Epistemic / Social / Protective / Personal)
- **Response type** (strong support → strong resistance, following Huang et al.)
- **Caution level** (low / medium / high)
- **Word count**

---

## Files

| File | Description |
|------|-------------|
| `values_analysis.py` | Data collection script — runs all API calls and stores results |
| `insight_report.pdf` | Full research summary with figures and findings |
| `analysis.ipynb` | Analysis and visualization notebook |
| `requirements.txt` | Python dependencies |
| `.env.example` | Template for environment variables — copy to `.env` and add your API key |
| `results.csv` | Raw coded results (160 observations) |
| `summary_table.csv` | Aggregated findings by model and language |
| `raw_responses.json` | Full Claude responses for qualitative review |

---

## Key Findings

**Finding 1 — Core stability:** Epistemic values dominate in both English and Spanish, across both model sizes. For Sonnet, they account for 30% in both languages. For Haiku, they account for 42.5% in English and 35% in Spanish. Chi-square tests found no statistically significant association between language and any of the three coded dimensions — value domain, caution level, or response type — in either model. This replicates and extends Huang et al.'s finding that Epistemic values dominate in English, suggesting the pattern is robust across language contexts.

**Finding 2 — AI & Society is the exception:** Prompts discussing AI itself triggered high caution at 25% in English but only 12.5% in Spanish — a 2x gap consistent across both models. No other category showed a comparable language-driven divergence. This asymmetry raises questions about whether AI safety information reaches Spanish-speaking users with equivalent emphasis.

**Finding 3 — Model size interacts with language differently:** Sonnet becomes more socially oriented in Spanish (Social: 15% → 22.5%) and less neutral (Neutral: 15% → 5%). Haiku shows the opposite in response type — Reframing drops from 40% to 25% in Spanish while Mild Resistance increases from 15% to 20%. These divergent directions suggest language effects on response style are not uniform across model sizes.

---

## Limitations

- Small sample size (40 prompts per language) limits statistical power
- Automated coding introduces potential misclassification — human validation on a subset is recommended
- Spanish prompts represent one regional variety (Mexican Spanish) and may not generalize
- Controlled prompts differ from naturalistic conversation — findings are preliminary, not representative of real-world usage

---

## Relationship to Prior Work

This study directly extends:
> Huang, S., Durmus, E., McCain, M., et al. (2025). *Values in the Wild: Discovering and Analyzing Values in Real-World Language Model Interactions.* COLM 2025.

The value taxonomy, response type categories, and chi-square analysis approach are borrowed from that paper. The contribution here is applying a controlled bilingual design to test whether their taxonomy generalizes across languages.

---

## How to Run

**1. Install dependencies**
```bash
pip install -r requirements.txt
```

**2. Set up your API key**

Copy `.env.example` to `.env` and add your Anthropic API key:
```bash
cp .env.example .env
```
Then open `.env` and replace the placeholder with your actual key:
```
ANTHROPIC_API_KEY=your-key-here
```
> ⚠️ Never commit your `.env` file. It is already listed in `.gitignore`.

**3. Run data collection** (~$3.50 in API costs)
```bash
python values_analysis.py
```

**4. Open the analysis notebook**
```bash
jupyter notebook analysis.ipynb
```

---

*Study conducted as part of a research interest in cross-language behavioral consistency in AI systems. March 2026.*
