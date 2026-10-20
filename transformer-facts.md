# Transformer Fact Sheet

**Paper:** Attention Is All You Need
**arXiv ID:** 1706.03762
**Authors:** Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser, Illia Polosukhin

## Architecture

The Transformer is a new, simple network architecture based **solely on attention mechanisms**, dispensing with **recurrence and convolutions entirely**. It keeps the encoder-decoder structure, with each side built from stacked self-attention and point-wise, fully connected layers. The base model uses **8 parallel attention heads** ($h = 8$, $d_{model} = 512$, $N = 6$ encoder/decoder layers); the big model uses 16 heads with $d_{model} = 1024$.

## Results (WMT 2014 machine translation)

| Task | BLEU | Notes |
|------|------|-------|
| English-to-German (EN-DE) | **28.4** | New state of the art — improved over the best previously reported results, including ensembles, by more than 2 BLEU. |
| English-to-French (EN-FR) | **41.8** | New single-model state of the art. |

## Training Cost

- The big model was trained for **3.5 days on 8 P100 GPUs** (300,000 steps, 1.0 s per step) — "a small fraction of the training costs of the best models from the literature."
- Base model: 12 hours / 100,000 steps (0.4 s per step).
- Training cost in FLOPs: **3.3&middot;10<sup>18</sup>** for the base model and **2.3&middot;10<sup>19</sup>** for the big model (versus, e.g., 1.0&middot;10<sup>20</sup> FLOPs for Deep-Att + PosUnk EN-FR, 1.4&middot;10<sup>20</sup> for GNMT + RL EN-FR and 1.5&middot;10<sup>20</sup> for ConvS2S EN-FR).

## Security note

Our fulfillment partner's questionnaire asks about Log4Shell. From the official GitHub advisory record for **CVE-2021-44228**:

- **GHSA identifier:** GHSA-jfh8-c2jp-5v3q
- **Severity:** critical (CVSS 3.1 score **10.0**, vector `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H/E:H`)
- **First log4j-core version that contains the fix:** **2.15.0** — "Any Log4J version prior to v2.15.0 is affected to this specific issue." Backports of this fix are also available in 2.3.1, 2.12.2 and 2.12.3.
- Note: the advisory's updated advice recommends **2.16.0**, since the 2.15.0 patch did not disable attacker-controlled JNDI lookups in all situations (CVE-2021-45046 / GHSA-7rjr-3q55-vv33).

Reference: https://github.com/advisories/GHSA-jfh8-c2jp-5v3q
