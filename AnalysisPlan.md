# Analysis Plan – Study 2

## Primary outcome
The primary outcome is **Reliability**, modeled at the item level using
ordinal regression.

Secondary analyses examine Loyalty and Vulnerability using identical models.

---

## Data structure

Data are analyzed in long format:
- one row per interview × item
- items modeled via item-specific thresholds

---

## Main model specification

For each construct (Reliability, Loyalty, Vulnerability):

**Model**
- Bayesian cumulative ordinal regression (probit link)
- Item-specific thresholds

**Formula**
rating | thres(gr = item) ~
  1 + resistance * scenario +
  (1 + resistance | INT) +
  (1 | DET)

**Backend**
- `cmdstanr`

**Sampling**
- 4 chains
- 12000 iterations (4000 warmup)
- adapt_delta = 0.99
- max_treedepth = 12

---

## Priors (fixed a priori)

```r
prior(normal(0, 1), class = "b")
prior(exponential(2), class = "sd")
prior(lkj(4), class = "cor")
