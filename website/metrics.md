# Metrics

> __Note__: For all models logs, there will be a folder named `eval/`. This contains individual `.csv` files for each relevant metric (e.g., RMSE, SpecDiv).


TCBench provides four types of metrics: (1) Deterministic, which evaluate deterministic forecasting tasks such as intensity and track prediction; (2) Probabilistic, which evaluate probabilistic, ensemble-based forecasts; (3) Track-specific metrics, which evaluate the predicted storm tracks; and (3) Rapid Intensification metrics, which evaluate the TCBench forecast skill for extreme events such as rapid intensification. We note that while most of TCBench is configured as a regression problem, we have formulated rapid intensification as a binary classification problem. This means rapid intensification models will be tasked with making a simple “yes/no" prediction for the occurrence of rapid intensification. 

1. __Deterministic:__
    - [x] **Root mean square error (RMSE)**:
    - [x] **Mean absolute error (MAE)**:
    - [x] **R-Squared Score (R<sup>2</sup>)**:

2. __Probabilistic:__
    - [x] **Continuous Ranked Probability Score (CRPS)**: Quantifies the accuracy of probabilistic predictions by measuring the difference between the predicted and observed cumulative distribution functions, with lower values indicating better predictions. For track predictions, CRPS was adjusted following S1 of Fernandez et al. (2025). 
    - [x] **Brier Skill Score (BSS)**: Measures the improvement of the forecast probability over a reference forecast, with values ranging from -∞ to 1, where 1 indicates a perfect forecast and 0 indicates no improvement over the reference. 
    - [x] **Probability Integral Transform (PIT) Histogram**: Provides a probabilistic estimate of model calibration. A PIT histogram with a uniform distribution indicates a well calibrated model, while a PIT histogram with a skewed or peaked distribution indicates a poorly calibrated model. (CITE)
    - [x] **Interquartile Range (IQR)**: 
    
3. __Track-Specific:__
    - [x] **Direct Position Error (DPE)**: The simplest form of track forecast error, DPE is calculated as the great circle distance between the forecast and observed positions of the TC at the same verification time (VT). While DPE provides a basic measure of positional accuracy, it does not convey information about directional biases (e.g., whether the forecast is too fast, slow, left, or right). DPE is calculated using standard great circle distance formulas (e.g., haversine).
    - [x] **Cross-Track Error (CTE)**: CTE represents the component of track error perpendicular to the observed track direction. To compute CTE, start by extrapolaing a vector from the observed position at the VT to the observed position 12 hours earlier. Draw a line perpendicular to this vector from the forecast position at the VT. Identify the intersection point of the perpendicular track with the extrapolated observed track. The great circle distance between the forecast position and the intersection point is defined as the CTE. Note that the sign of CTE is hemisphere-dependent: in the Northern Hemisphere, a positive value indicates a forecast to the right of the observed track (looking along the direction of TC motion); in the Southern Hemisphere, this is reversed.
    - [x] **Along-Track Error (ATE)**: ATE quantifies the error in timing, i.e., whether the forecast storm position is ahead of or behind the observed position along the direction of motion. To compute ATE, use the same extrapolated observed track and intersection point as in the CTE calculation. Compute the great circle distance between the observed position at the VT and the intersection point. A positive ATE indicates the forecast position is ahead (i.e., faster) along the track; a negative ATE indicates it is behind (i.e., slower). *Note that CTE and ATE require an observed position 12 hours prior to the VT; thus, they are undefined for the first valid time of a TC.**
        
4. __Rapid Intensification:__
    - [x] **Critical Success Index (CSI)**: Also known as the Threat Score, measures the ratio of correctly predicted positive observations to the sum of all predicted positives, actual positives, and minus true positives. 
    - [x] **Peirce Skill Score (PSS)**: The Peirce skill score (also known as the Hansen and Kuipers discriminant, or the true skill statistic) is an estimate of how well the forecast separates "yes" events from "no" events. It ranges from -1 to 1, with +1 being a perfect score and 0 indicating no skill. PSS is generally considered to be better for rare events, though for extremely rare events it tends to 0. 
    - [x] **Odds Ratio (OR)**: The odds ratio provides the ratio of the odds of a "yes" forecast being correct versus a "yes" forecast being incorrect. The odds ratio ranges from 0 to $\infty$, with $\infty$ being a perfect score and 1 having no skill. (We can also use the log of the odds ratio, meaning it would range from $-\infty$ to $\infty$ and 0 would indicate no skill). The odds ratio takes prior probabilities into account and is less sensitive to hedging, though it cannot be used if any section of the contingency table is 0.
    
