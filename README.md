# Actuarial Claim Frequency Modeling

## 📌 Project Overview
This repository contains an automated R function designed for actuarial and risk management applications. The `best_fit_frequency()` function evaluates and selects the optimal theoretical distribution for aggregated insurance claim frequencies.

It compares Poisson, Negative Binomial, and Binomial distributions by applying Maximum Likelihood Estimation (MLE) and selects the best-performing model based on the Akaike Information Criterion (AIC).

## ⚙️ Key Features
* **Automated Model Selection:** Evaluates multiple distributions and automatically ranks them by AIC.
* **Robust Error Handling:** Implements `tryCatch` to gracefully handle mathematical failures (e.g., Binomial distribution failure due to severe data overdispersion).
* **Data Unpacking:** Natively accepts aggregated actuarial data (number of claims $k$ and number of policies $n_k$) and expands it to raw observations for accurate MLE fitting.
* **Integrated Visualization:** Automatically generates a comparative density plot of the observed empirical data against the theoretical fitted distributions.

## 🛠️ Prerequisites & Dependencies
The script relies on the `fitdistrplus` package for distribution fitting and density computation.
To run the code, install the required library:
```R
install.packages("fitdistrplus")
# 1. Load the required library
library(fitdistrplus)

# 2. Source the function file
source("frequency_fitting.R")

# 3. Create dummy aggregated actuarial data
# k  = number of claims
# nk = number of policies experiencing k claims
claims_data <- data.frame(
  k = c(0, 1, 2, 3, 4),
  nk = c(850, 120, 25, 4, 1)
)

# 4. Run the model
results <- best_fit_frequency(claims_data)

# 5. View the summary table
print(results$Best_Fit_Result)
print(results$Summary)
