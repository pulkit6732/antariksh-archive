# DRISHTI

**Hackathon:** Bharatiya Antariksh Hackathon 2026 (PS-15: Solar Flare Nowcasting/Forecasting)
**Team:** HELIOGUARD — Pulkit Kr Srivastava 
**Result:** Did not place

## What we built

A solar flare nowcasting/forecasting system using Aditya-L1's SoLEXS (soft
X-ray) and HEL1OS (hard X-ray, non-thermal) instruments. GOES, the world's
operational space-weather system, only sees soft/thermal X-ray and misses
the non-thermal signal that precedes a flare's energy release. DRISHTI fuses
both bands into a calibrated 15-30 min nowcast plus a 24h forecast.

## Why it's different

Hard X-ray monitoring used to exist operationally via RHESSI, which has since
retired. Aditya-L1's HEL1OS is one of the few instruments that can fill that
gap in real time. On 51 real M/X flares, the HEL1OS non-thermal signature
measurably precedes the soft X-ray peak by ~6 minutes on average (up to ~18
minutes onset-to-peak) — that lead time is the actual product.

## Tech stack

Python 3.11, astropy (FITS parsing), NumPy, Matplotlib, logistic regression
with isotonic calibration. Data from ISRO PRADAN/ISSDC (SoLEXS + HEL1OS),
validated against NASA DONKI and NOAA GOES. Runs on a standard laptop, no
GPU or specialized compute required.

## Results / what we measured

TSS +0.31 vs a persistence baseline's +0.26, ECE ~0.06 (a forecast that says
"75%" happens ~73% of the time in practice). Validated with paired bootstrap
on the TSS delta specifically because N=51 real flares is a small sample —
the confidence interval exists to avoid overclaiming skill the sample size
can't actually support.

## What we're proud of

The honesty of the validation, not the headline number. It would've been
easy to report a single point-estimate TSS and stop there. Running the
bootstrap and reporting the CI meant being upfront that 0.31 comes with real
uncertainty at this sample size — that mattered more to us than a bigger
number we couldn't back up.

## What we'd fix or do differently

- The 51-flare sample is the real bottleneck — HEL1OS is a newer instrument
  and doesn't have years of accumulated flare history yet. There was no way
  to simulate around this honestly (you can't fabricate a real flare
  catalogue), so the fix is just: more real data over time as Aditya-L1
  keeps operating.
- No live working demo — the submission was a validated methodology on a
  real dataset, not a deployed pipeline. Would build the operator dashboard
  out fully next time instead of leaving it as a mockup.

## Links

- Submission deck: available on request
- Repo: not currently public

## Note on missing pieces

Local project files were lost after the hackathon; this writeup was
reconstructed from the original submission deck.
