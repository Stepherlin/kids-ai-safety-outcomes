# KORA HERLIN — Reconstruction Prompt for Claude.ai

Use this prompt to reconstruct the KORA GenAI Developmental Outcomes visualization in Claude.ai artifacts.

---

## BRIEF

Build an interactive D3 v7 visualization called **KORA HERLIN — GenAI Developmental Outcomes**.

The viz has **4 tabs**: Outcomes · Industry Impact · Safety · Mechanisms

---

## TYPOGRAPHY & COLORS

- Font stack: `'Inter', 'Segoe UI', sans-serif`
- Background: `#fafaf8` (warm off-white)
- Text primary: `#1c1917`
- Accent: `#78716c` (stone-500)
- Tab active border: `#a16207` (amber-700)

---

## SPHERE DATA (8 spheres + 1 ENV ring)

| id | label | n_studies | studies_pos | studies_neg | nodeR | color |
|----|-------|-----------|-------------|-------------|-------|-------|
| academic | Academic & Learning | 287 | 198 | 41 | 48 | #3b82f6 |
| neurocognitive | Neurocognitive | 203 | 134 | 38 | 43 | #8b5cf6 |
| affective | Affective & Emotional | 417 | 89 | 241 | 52 | #ef4444 |
| psychosocial | Psychosocial | 112 | 44 | 51 | 33 | #f97316 |
| creative | Creative & Expressive | 68 | 49 | 9 | 27 | #10b981 |
| environmental | Environmental Context | 74 | 31 | 22 | 28 | #06b6d4 |
| sensorimotor | Sensorimotor | 48 | 18 | 19 | 22 | #f59e0b |
| metacognitive | Metacognitive | 18 | 11 | 4 | 20 | #6366f1 |

### nodeR scale
```javascript
const _nodeRScale = d3.scaleSqrt()
  .domain([0, d3.max(SPHERES, d => d.n_studies)])
  .range([0, 52]);
SPHERES.forEach(s => { s.nodeR = Math.max(20, _nodeRScale(s.n_studies)); });
```

### Directional fill
```javascript
function dirFill(d) {
  const sig = (d.studies_pos - d.studies_neg) / d.n_studies;
  if (sig > 0.20) return 'rgba(187,247,208,0.75)';
  if (sig > 0.06) return 'rgba(220,252,231,0.65)';
  if (sig < -0.12) return 'rgba(254,202,202,0.75)';
  if (sig < -0.02) return 'rgba(254,226,226,0.62)';
  return 'rgba(255,251,235,0.55)';
}
function dirStroke(d) {
  const sig = (d.studies_pos - d.studies_neg) / d.n_studies;
  if (sig > 0.06)  return '#166534';
  if (sig < -0.02) return '#991b1b';
  return '#78716c';
}
```

---

## INDUSTRY IMPACT DATA

| sphere | n_ind | pos_ind% | n_industry | pos_industry% | gap_pp |
|--------|-------|----------|------------|---------------|--------|
| academic | 231 | 67% | 56 | 90% | +23pp |
| neurocognitive | 168 | 63% | 35 | 88% | +25pp |
| affective | 389 | 22% | 28 | 15% | -7pp |
| psychosocial | 98 | 37% | 14 | 23% | -14pp |
| creative | 62 | 71% | 6 | ~116% | +45pp |
| environmental | 70 | 40% | 4 | 50% | +10pp |
| sensorimotor | 48 | — | 0 | — | n/a |
| metacognitive | 18 | — | 0 | — | n/a |

Visualize as a slope chart: left = independent rate, right = industry rate.

---

## 22 MECHANISMS (4 groups)

**Cognitive (7):** Working Memory Load · Attention Modulation · Executive Function · Metacognitive Scaffolding · Cognitive Offloading · Pattern Recognition · Dual Coding

**Affective (5):** Emotional Regulation · Social Comparison · Empathy Simulation · Stress/Arousal · Reward Circuitry

**Social (5):** Peer Interaction · Identity Formation · Parasocial Bonding · Digital Literacy · Social Norm Encoding

**Developmental (5):** Scaffolded Learning · Autonomy Support · Embodied Cognition · Sleep Displacement · Attention Span Erosion

---

## SAFETY CLUSTERS (4 clusters, 37 nodes)

**Cognitive Risks (9):** Attention fragmentation · Working memory overload · Critical thinking erosion · Cognitive dependency · Metacognitive bypass · Decision fatigue · Over-reliance · Epistemic bubbles · Creativity suppression

**Psychosocial Risks (10):** Social skill atrophy · Identity diffusion · Parasocial substitution · Peer comparison harm · Loneliness amplification · Empathy erosion · Authority confusion · Trust miscalibration · Role model distortion · Boundary dissolution

**Developmental Risks (9):** Sleep displacement · Physical inactivity · Sensorimotor delay · Language acquisition gap · Executive function lag · Emotional regulation gap · Autonomy stunting · Motivation erosion · Academic dependency

**Systemic Risks (9):** Data exploitation · Algorithmic bias · Privacy erosion · Consent violation · Equity gap · Surveillance normalization · Regulatory gap · Parental oversight erosion · Teacher authority displacement

---

## EVIDENCE FRAMEWORK

**Przybylski tiers:**
- Strict (score=5): pre-registration + peer-reviewed + n>100 + effect size + replication
- Moderate (score=3): peer-reviewed + n>30 + effect size
- Loose (score=0.1): any other included study

**Effect direction:** positive · negative · null · mixed

**Industry classification:** institution matches any of: OpenAI · Google · Meta · Microsoft · Apple · DeepMind · Anthropic · Khan Academy · Duolingo · edtech · AI lab

---

## IMPLEMENTATION NOTES

- D3 v7: `https://d3js.org/d3.v7.min.js`
- Lazy build flags: `industryVizBuilt`, `mechVizBuilt`
- Dimensions from `window.innerWidth / window.innerHeight`
- ENV_SPHERE = outer ring only, NOT a force node
- Mechanism band: `innerRadius(nodeR+1), outerRadius(nodeR+5)`
- Tab IDs: `tab-spheres`, `tab-industry`, `tab-safety`, `tab-mech`
- View filter buttons: All · Strict · Moderate (Przybylski tiers)

---

## KEY FINDING

Industry funding shows domain-specific bias: +23–45pp positive in academic/cognitive spheres, −7 to −14pp in affective/psychosocial. Suggests strategic publication bias.

---

*KORA HERLIN Framework — Stéphie Herlin — corpus v9 — May 2026*
