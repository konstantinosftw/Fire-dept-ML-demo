
# Montesinho Forest Fires Dataset

## Info
In the above reference, the output "area" was first transformed with a ln(x+1) function. Then, several Data Mining methods were applied. After fitting the models, the outputs were post-processed with the inverse of the ln(x+1) transform. Four different input setups were used. The experiments were conducted using a 10-fold (cross-validation) x 30 runs. Two regression metrics were measured: MAD and RMSE. A Gaussian support vector machine (SVM) fed with only 4 direct weather conditions (temp, RH, wind and rain) obtained the best MAD value: 12.71 +- 0.01 (mean and confidence interval within 95% using a t-student distribution). The best RMSE was attained by the naive mean predictor. An analysis to the regression error curve (REC) shows that the SVM model predicts more examples within a lower admitted error. In effect, the SVM model predicts better small fires, which are the majority.

Relevant Information:

This is a very difficult regression task. It can be used to test regression methods. Also, it could be used to test outlier detection methods, since it is unclear how many outliers are there. Yet, many examples of fires with a large burned area are very small.


## Data

Number of Instances: 517

Number of Attributes: 12 + output attribute

Note: several of the attributes may be correlated, thus it makes sense to apply some sort of feature selection.

Missing Attribute Values: None

### Attributes
- X  
  - Description: x-axis spatial coordinate within the Montesinho park map.  
  - Type: integer.  
  - Range: 1 to 9.  
  - Notes: discrete grid coordinate.

- Y  
  - Description: y-axis spatial coordinate within the Montesinho park map.  
  - Type: integer.  
  - Range: 2 to 9.  
  - Notes: discrete grid coordinate.

- month  
  - Description: month of the year.  
  - Type: categorical (string).  
  - Values: "jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sep", "oct", "nov", "dec".  
  - Notes: use one-hot or cyclic encoding for models (e.g., sin/cos) if preserving seasonality.

- day  
  - Description: day of the week.  
  - Type: categorical (string).  
  - Values: "mon", "tue", "wed", "thu", "fri", "sat", "sun".  
  - Notes: treat as categorical or map to weekday index.

- FFMC  
  - Description: Fine Fuel Moisture Code (FFMC) from the Fire Weather Index (FWI) system; estimates moisture content of litter and fine fuels.  
  - Type: numeric (continuous).  
  - Range: 18.7 to 96.20.  
  - Typical: often concentrated toward higher values depending on season; higher FFMC → more flammable fine fuels.

- DMC  
  - Description: Duff Moisture Code (DMC) from the FWI system; describes moisture in the organic layer (duff).  
  - Type: numeric (continuous).  
  - Range: 1.1 to 291.3.  
  - Typical: wide range; increases with accumulated dryness.

- DC  
  - Description: Drought Code (DC) from the FWI system; indicates long‑term drought and deep fuel dryness.  
  - Type: numeric (continuous).  
  - Range: 7.9 to 860.6.  
  - Typical: large scale values; useful for chronic dryness signals.

- ISI  
  - Description: Initial Spread Index (ISI) from the FWI system; combines wind and FFMC to estimate potential rate of spread.  
  - Type: numeric (continuous).  
  - Range: 0.0 to 56.10.  
  - Typical: sensitive to wind and FFMC; low values common, spikes during active fire weather.

- temp  
  - Description: temperature in degrees Celsius.  
  - Type: numeric (continuous).  
  - Range: 2.2 to 33.3.  
  - Typical: seasonal variation; use standardization for modeling.

- RH  
  - Description: relative humidity in percent.  
  - Type: numeric (continuous).  
  - Range: 15.0 to 100.0.  
  - Typical: inversely correlated with fire risk; consider clipping to  for sanity.

- wind  
  - Description: wind speed in km/h.  
  - Type: numeric (continuous).  
  - Range: 0.4 to 9.4.  
  - Typical: influences ISI and spread; may be skewed right.

- rain  
  - Description: outside rain in mm/m^2 (mm).  
  - Type: numeric (continuous).  
  - Range: 0.0 to 6.4.  
  - Typical: many zeros; rainfall events reduce fire risk.

- area  
  - Description: burned area of the forest (in hectares). This is the target variable in many tasks.  
  - Type: numeric (continuous).  
  - Range: 0.00 to 1090.84.  
  - Typical: heavily right-skewed; most observations = 0.0.  
  - Modeling note: highly skewed distribution; recommended target transforms include log(area + 1) or using a two-stage model (classification for zero vs >0, then regression on positives). Consider robust metrics (MAE, median absolute error) and evaluation on both raw and transformed scales.

Recommended summary statistics to include (compute these from your data and insert actual numbers)
- For numeric columns (FFMC, DMC, DC, ISI, temp, RH, wind, rain, area): Min, 25th percentile (Q1), Median, Mean, 75th percentile (Q3), Max, StdDev, % zeros (for rain and area), skewness.  
- For categorical columns (month, day, X, Y): unique values count, frequency of top categories, and whether values are balanced.

Example short table entry (replace bracketed values with dataset results)
- FFMC — type: float. range: 18.7–96.20. min: [min], Q1: [Q1], median: [median], mean: [mean], Q3: [Q3], max: [max], std: [std], skew: [skew].