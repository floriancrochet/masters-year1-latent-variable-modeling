# Thermal Performance Modeling Using Latent Variables  
*A comparative analysis of PCR and PLS regression for building energy modeling.*

---

## 📘 Overview
This project applies **latent variable modeling** techniques — specifically **Principal Components Regression (PCR)** and **Partial Least Squares Regression (PLS)** — to predict the **total energy load** of university buildings.  
It was developed within the *Master 1 Econometrics and Statistics – Applied Econometrics track* at Oniris (academic year 2024–2025).

**Objectives**
- Build predictive models for energy consumption based on simulated building data  
- Compare PCR and PLS performance in the presence of multicollinearity  
- Identify the most influential variables on energy demand  
- Evaluate the effect of transforming the dependent variable to improve model fit  

---

## ⚙️ Features
- Exploratory analysis of 33 thermal, geometric, and usage variables  
- Transformation of target variable (square-root) to stabilize variance  
- PCR and PLS modeling with cross-validation and test evaluation  
- Automated selection of the optimal number of components using the *“one sigma”* criterion  
- Model comparison based on **R²**, **RMSE**, and **external validation**  
- Variable importance assessment via **VIP scores** for PLS  

---

## 🧰 Tech Stack
**Language:** R  
**Libraries:** `tidyverse`, `caret`, `car`, `pls`, `gridExtra`, `corrplot`  

---

## ⚙️ Installation
Clone the repository and ensure the R dependencies are installed:

```bash
git clone https://github.com/PierreQDK/rendu_varlat.git
cd rendu_varlat
Rscript -e "install.packages(c('tidyverse','caret','car','pls','gridExtra','corrplot'))"
```

---

## 📚 Usage Example

```r
# Run main script
source("code variables latentes.R")

# Fit PLS model with optimal components
plsr_model <- plsr(sqrt_EnergyLoad ~ ., data = Train2, validation = "CV", scale = TRUE)

# Plot performance metrics
validationplot(plsr_model, val.type = "RMSEP")
```

All data files (`UPENN.txt`, `GT.txt`) and scripts must be placed in the `data/` and `src/` directories respectively.

---

## 📂 Project Structure

```
rendu_varlat/
│
├── data/                # Simulation datasets (UPENN and GT)
├── src/                 # R source scripts (e.g., VIP.R)
├── code variables latentes.R
├── Variables latentes - rapport - Pierre et Florian.pdf
├── enoncé.pdf
└── README.md
```

---

## 📊 Results

### Model Comparison Summary

| Model | Target Variable | Optimal Components | R² (Train) | R² (CV) | R² (Test) | RMSE (CV) |
|--------|----------------|-------------------|-------------|----------|------------|------------|
| PCR | sqrt_EnergyLoad | 20 | 0.778 | 0.642 | -0.509 | 1.68 |
| PLS | sqrt_EnergyLoad | 3 | 0.801 | 0.670 | -0.496 | 1.61 |

- **PLS outperformed PCR** on training and validation sets, with fewer components and lower RMSE.  
- **Both models failed to generalize** on the test dataset (negative R²), reflecting sensitivity to new building structures.  
- **Key influential variables (VIP > 1):**  
  - Building geometry: `zone_area`, `bldg_height`, `op_S_area`, `gl_S_area`  
  - Thermal properties: `op_uValue`, `roof_op_uValue`, `gl_U_value`  
  - Internal gains: `totalocc`, `heat_flow_rate`, `cool_flow_rate`, `chair_per_occ`  

![Example RMSE plot](> À compléter)

---

## 🧠 References
- Tian, W., Choudhary, R., Augenbroe, G., & Lee, S. H. (2015). *Importance analysis and meta-model construction with correlated variables in evaluation of thermal performance of campus buildings.* Building and Environment, 92, 61–74.  
- Hyndman & Athanasopoulos, *Forecasting: Principles and Practice*  
- Hamilton, *Time Series Analysis*  
- Wooldridge, *Introductory Econometrics: A Modern Approach*

---

## 📜 License
This project is released under the **MIT License**.  
© 2025 Florian Crochet, Pierre Quintin de Kercadio  

---

## 👤 Author
**Florian Crochet** & **Pierre Quintin de Kercadio**  
*Master 1 Econometrics & Statistics – Applied Econometrics*  
📫 > À compléter  

---

## 💬 Acknowledgments
Supervised by **Véronique Cariou**  
(Department of Applied Econometrics, Oniris Nantes)  
Special thanks to the R open-source community for the statistical and visualization tools used in this project.
