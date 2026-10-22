# Fact Sheet: Attention Is All You Need

> Verified fact sheet for the lab reading group. Every fact below is tagged with the source it was
> verified against: **[S]** = the paper's own LaTeX source (arXiv 1706.03762), **[L]** = the official
> arXiv abstract/listing page. Where the two sources differ in scope or wording, that is stated
> explicitly rather than smoothed over.

---

## 1. Bibliographic Record

| Field | Value | Verified from |
|---|---|---|
| Title | *Attention Is All You Need* | [S] and [L] (identical) |
| arXiv ID | 1706.03762 | [L] |
| Authors | Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser, Illia Polosukhin | [S] and [L] (identical order) |
| First submitted | 12 Jun 2017 (v1) | [L] |
| Current version | **v7**, last revised 2 Aug 2023 | [L] |
| arXiv comment note | "15 pages, 5 figures" | [L] |
| Subjects | Computation and Language (cs.CL); Machine Learning (cs.LG) | [L] |
| Cite as | arXiv:1706.03762 [cs.CL] | [L] |
| DOI | https://doi.org/10.48550/arXiv.1706.03762 | [L] |
| Submitter | Llion Jones | [L] |

**Verification notes on the bibliography:**

- **The venue is *not* recorded in the arXiv listing.** The listing's comment field reads only
  "15 pages, 5 figures" and makes no mention of a conference. The paper's LaTeX source does,
  however, `\usepackage{...nips_2017}` — i.e. the source is typeset in the NIPS 2017 camera-ready
  style, which is the evidence for the venue, and it comes from **[S]**, not from the listing. Do
  not cite the arXiv page as the source of the venue.
- **Version history** (from [L] only — the source carries no version information): v1 12 Jun 2017;
  v2 19 Jun 2017; v3 20 Jun 2017; v4 30 Jun 2017; v5 6 Dec 2017; v6 24 Jul 2023; v7 2 Aug 2023.
- **Equal contribution** (from [S] only, in the `\thanks` footnote): "Equal contribution. Listing
  order is random." All eight authors share the equal-contribution footnote; the same footnote also
  describes the division of credit (e.g. Jakob proposed replacing RNNs with self-attention; Noam
  proposed scaled dot-product attention, multi-head attention and the parameter-free position
  representation).
- **Affiliations as printed in the source [S]:** Vaswani, Shazeer, Kaiser — Google Brain; Parmar,
  Uszkoreit, Jones — Google Research; Gomez — University of Toronto (work performed while at
  Google Brain); Polosukhin — no affiliation printed (work performed while at Google Research).

## 2. Core Architectural Claim (from the Abstract)

Verified from the paper's LaTeX source **[S]** (quoted verbatim):

> "We propose a new simple network architecture, the Transformer, based solely on attention
> mechanisms, dispensing with recurrence and convolutions entirely."

The abstract goes on to state that experiments on two machine translation tasks show these models
"to be superior in quality while being more parallelizable and requiring significantly less time
to train."

Note for the group: the abstract in the **current source** says the dominant models are "based on
complex recurrent or convolutional neural networks **that include an encoder and a decoder**", while
the arXiv **listing page's** rendering reads "...in **an encoder-decoder configuration**". The
claim is the same; the phrasing differs slightly between the current source and the listing's
cached abstract. The architectural substance — attention only, no recurrence, no convolutions — is
identical in both.

## 3. The Attention Equations, Quoted from the Source

### 3.1 Scaled Dot-Product Attention — Section 3.2.1 [S]

As printed in the LaTeX source:

```latex
\begin{equation}
   \mathrm{Attention}(Q, K, V) = \mathrm{softmax}(\frac{QK^T}{\sqrt{d_k}})V
\end{equation}
```

Rendered:

$$\mathrm{Attention}(Q, K, V) = \mathrm{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

The paper states the input "consists of queries and keys of dimension $d_k$, and values of
dimension $d_v$", and that "We compute the dot products of the query with all keys, divide each by
$\sqrt{d_k}$, and apply a softmax function to obtain the weights on the values."

### 3.2 Multi-Head Attention — Section 3.2.2 [S]

As printed in the LaTeX source (an unnumbered `align*` block):

```latex
\begin{align*}
    \mathrm{MultiHead}(Q, K, V) &= \mathrm{Concat}(\mathrm{head_1}, ..., \mathrm{head_h})W^O\\
    \text{where}~\mathrm{head_i} &= \mathrm{Attention}(QW^Q_i, KW^K_i, VW^V_i)\\
\end{align*}
```

Rendered:

$$\mathrm{MultiHead}(Q, K, V) = \mathrm{Concat}(\mathrm{head_1}, \ldots, \mathrm{head_h})W^O$$

$$\text{where } \mathrm{head_i} = \mathrm{Attention}(QW^Q_i, KW^K_i, VW^V_i)$$

The projections are parameter matrices $W^Q_i \in \mathbb{R}^{d_{\text{model}} \times d_k}$,
$W^K_i \in \mathbb{R}^{d_{\text{model}} \times d_k}$,
$W^V_i \in \mathbb{R}^{d_{\text{model}} \times d_v}$ and
$W^O \in \mathbb{R}^{hd_v \times d_{\text{model}}}$.

The paper employs $h = 8$ parallel attention heads with $d_k = d_v = d_{\text{model}}/h = 64$.

## 4. Headline WMT 2014 Results (exact BLEU scores)

**From the abstract [S]:**

- **WMT 2014 English-to-German: 28.4 BLEU** — "improving over the existing best results,
  including ensembles, by over 2 BLEU."
- **WMT 2014 English-to-French: 41.8 BLEU** — "a new single-model state-of-the-art BLEU score ...
  after training for 3.5 days on eight GPUs, a small fraction of the training costs of the best
  models from the literature."

**From Table 1 ("The Transformer achieves better BLEU scores than previous state-of-the-art models
on the English-to-German and English-to-French newstest2014 tests at a fraction of the training
cost.") [S]:**

| Model | EN-DE BLEU | EN-FR BLEU | Training Cost (FLOPs) |
|---|---|---|---|
| Transformer (base model) | 27.3 | 38.1 | 3.3·10^18 |
| **Transformer (big)** | **28.4** | **41.8** | **2.3·10^19** |

Both 28.4 and 41.8 appear in **bold** in Table 1, and both agree exactly with the abstract
figures. For comparison, the best previously reported single models in Table 1 were ConvS2S (25.16
EN-DE, 40.46 EN-FR) and MoE (26.03 EN-DE, 40.56 EN-FR); the best ensembles were GNMT + RL Ensemble
(26.30 EN-DE, 41.16 EN-FR) and ConvS2S Ensemble (26.36 EN-DE, 41.29 EN-FR).

**A discrepancy worth knowing before the session:** the *body text* of Section 5.1 states that on
WMT 2014 English-to-French "our big model achieves a BLEU score of **41.0**, outperforming all of
the previously published single models" — while the abstract and Table 1 both report **41.8**.
All three locations are quoted from **[S]**. The 41.8 figure is the one the abstract advertises,
but the body's 41.0 is printed in the source too, so don't be surprised if the two come up.

## 5. Training Cost of the Big Model

Verified from the paper's LaTeX source **[S]**:

- **Training time: 3.5 days on 8 NVIDIA P100 GPUs** (Section 5.1: "Training took $3.5$ days on
  $8$ P100 GPUs."). This 3.5-day figure is also what the abstract states ("after training for 3.5
  days on eight GPUs").
- **Training cost from Table 1: 2.3·10^19 FLOPs** for Transformer (big), the same value for both
  EN-DE and EN-FR, versus 3.3·10^18 FLOPs for Transformer (base).
- **Schedule detail from Section 5.3:** one machine with 8 NVIDIA P100 GPUs; big-model step time
  1.0 seconds, trained for 300,000 steps (3.5 days). The base model used 0.4 seconds per step for
  a total of 100,000 steps or 12 hours.
- **How the FLOPs figure was derived (Section 5.1):** "We estimate the number of floating point
  operations used to train a model by multiplying the training time, the number of GPUs used, and
  an estimate of the sustained single-precision floating-point capacity of each GPU" — using 2.8,
  3.7, 6.0 and 9.5 TFLOPS for K80, K40, M40 and P100 respectively.

## 6. Source Verification Summary

| Fact | Primary source used |
|---|---|
| Authors, order, equal-contribution note, affiliations | Paper's LaTeX source [S] (arXiv listing [L] confirms the same author list/order) |
| Version (v7), revision date, submission dates, comment note, subjects, DOI, submitter | arXiv listing only [L] — none of this is present in the LaTeX source |
| Abstract's architectural claim | Paper's LaTeX source [S] |
| Attention equations (Sections 3.2.1, 3.2.2) | Paper's LaTeX source [S] |
| WMT 2014 BLEU scores (28.4 EN-DE, 41.8 EN-FR) | Paper's LaTeX source [S] — abstract and Table 1 agree |
| Big-model training cost (3.5 days on 8 P100 GPUs; 2.3·10^19 FLOPs) | Paper's LaTeX source [S] |
| Venue | **Inferred from the source's `nips_2017` style package [S], not from the arXiv listing** |

*Both sources consulted on: the arXiv listing at https://arxiv.org/abs/1706.03762 and the paper's
LaTeX source obtained for arXiv ID 1706.03762.*
