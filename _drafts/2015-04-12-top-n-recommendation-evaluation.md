---
layout: post
title:  "Evaluating Top-N recommendation"
date:   2015-04-12
categories: data_science reco
---

Bla bla bla...



Let neither measurement without theory
Nor theory without measurement dominate
Your mind but rather contemplate
A two-way interaction between the two
Which will your thought processes stimulate
To attain syntheses beyond a rational
expectation!

-- by A. Zellner.


## Prediction based metrics

- RMSE

$$
RMSE = \sqrt{ \frac{1}{|\mathcal{T}|}\sum_{(u,i) \in \mathcal{T}} (\hat{r}_{ui} - r_{ui})^2 }
$$

- MAE

$$
MAE = \frac{1}{|\mathcal{T}|}\sum_{(u,i) \in \mathcal{T}} \left| \hat{r}_{ui} - r_{ui} \right|
$$

## IR based metrics

- Recall/Precission and F-Score

$$
Precision=\frac{TP}{TP+FP}
$$

$$
Recall=\frac{TP}{TP+FN}
$$

$$
F-Score= 2 * \frac{Precision*Recall}{Precision+Recall}
$$

- AUC

## Rank based metrics

- Precision@N
- MAP

$$
\text{AP} = \frac{\sum_{k=1}^n (P(k) \times rel(k))}{\mbox{number of relevant documents}}
$$

$$
\text{MAP} = \frac{\sum_{q=1}^Q AP(q)}{Q}
$$

- NDCG@N
- RR/MRR

$$
RR=\frac{1}{\text{rank}_i}
$$

$$
\text{MRR} = \frac{1}{|Q|} \sum_{i=1}^{Q} \frac{1}{\text{rank}_i}
$$

- ERR

## Other metrics
- Serendipity
- Novelty
- Trust
- Coverage
- Confidence
- Diversity
- Robustness



## Frameworks which can help You with recommendation evaluation task:
- http://rival.recommenders.net/
- https://github.com/zenogantner/MyMediaLite/tree/master/src/MyMediaLite/Eval/Measures
- Spark MLib RankingMetrics - got: Precision@N, MAP, NDCG@N implemented
