# Nonpara — Nonparametric FRB Population Analysis
This repository provides a Jupyter Notebook demonstrating nonparametric estimates of the energy function and cosmic event-rate evolution of **apparently non-repeating fast radio bursts** in CHIME/FRB Catalog 2. It accompanies the research analysis described in **Dong et al. (2026)**.

The notebook illustrates the analysis of the **non-repeating sample only**. 


## Contents
| File | Purpose |
| --- | --- |
| `CHIME_Cat2_NR_Nonparametric_emcee.ipynb` | Jupyter Notebook: energy–redshift plot, Efron–Petrosian $k$–$\tau$ scan, Lynden-Bell $C^{-}$ cumulative distributions, reconstructed cosmic event rate, and `emcee` power-law fit |
| `NonrepeatingFRBsdata.txt` | Input data for the non-repeating sample (3,057 rows; two whitespace-separated columns) |
| `requirements.txt` | Python dependencies |
| `LICENSE` | MIT license for the software and original documentation |
| `CITATION.cff` | Machine-readable citation metadata for the software release |

### Input data
`NonrepeatingFRBsdata.txt` is a plain-text, whitespace-delimited table **without a header**. Each row represents one apparently non-repeating FRB used in this analysis:

1. **Column 1:** estimated redshift $z$ (dimensionless; model-derived, not necessarily a spectroscopic redshift).
2. **Column 2:** isotropic-equivalent burst energy $E$ (erg).

The sample is derived from **CHIME/FRB Catalog 2**, with the redshift and energy estimates and sample selection described in the associated paper. Please cite the CHIME/FRB Catalog 2 source and Dong et al. (2026) when reusing the compiled sample. Verify the final bibliographic details in the paper before publication of this release.

## Run the notebook
Python 3.10 or later is recommended. From the directory containing the notebook and data file:

```bash
python -m pip install -r requirements.txt
jupyter notebook CHIME_Cat2_NR_Nonparametric_emcee.ipynb
```

In Jupyter, select **Run All**. Keep the input `.txt` file beside the notebook. The notebook computes intermediate quantities **in memory**, displays plots inline, and does not write intermediate text files.

## Analysis outline
1. Plot the observed energy–redshift distribution and the adopted completeness boundary.
2. Scan the energy-evolution exponent $k$ using the Efron–Petrosian $\tau$ statistic. The original grid-search and midpoint zero-crossing convention are preserved.
3. Estimate cumulative energy and redshift distributions with the Lynden-Bell $C^{-}$ method.
4. Derive binned cosmic event-rate estimates under the specified cosmology, completeness threshold, and normalization assumptions.
5. Fit the normalized rates with $\rho(z)=A(1+z)^B$ using `emcee`. The log-space likelihood includes an extra-scatter term $\ln f$; the Notebook displays posterior summaries and a corner plot.

The cosmology, fluence threshold, redshift scanning resolution, bin endpoints, and MCMC settings are defined in the notebook. Changing these choices can change the numerical results. MCMC posterior quantiles can vary slightly across runs.

## Scope and limitations

The input redshifts are estimates, and the adopted sharp fluence threshold is an approximation to the actual CHIME selection function. The notebook does not model full observational completeness, declination/width-dependent sensitivity, or the additional selection effects associated with identifying repeaters. Please consult the associated paper for methodological assumptions and robustness tests. The published release is a research example for the non-repeating sample, not a general-purpose survey selection-function pipeline.

