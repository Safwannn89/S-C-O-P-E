

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone https://github.com/<username>/scope-dashboard.git
    ```
4I can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone https://github.com/<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudI can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load withinI can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** DisplaysI can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog ofI can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog of the dataset with dynamically updating distribution histograms.
3.  **Model Performance:** Detailed analytics including accuracy comparisons, a high-contrast confusion matrix, and feature importance rankings.
4.I can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog of the dataset with dynamically updating distribution histograms.
3.  **Model Performance:** Detailed analytics including accuracy comparisons, a high-contrast confusion matrix, and feature importance rankings.
4.  **Live Prediction Lab:**
    *   **Search by Planet Name:** Instantly classify known exoplanets with a confidence score.
    *   I can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog of the dataset with dynamically updating distribution histograms.
3.  **Model Performance:** Detailed analytics including accuracy comparisons, a high-contrast confusion matrix, and feature importance rankings.
4.  **Live Prediction Lab:**
    *   **Search by Planet Name:** Instantly classify known exoplanets with a confidence score.
    *   **Custom Parameters:** Input hypothetical stellar and orbital parameters to simulate an environment and receive real-time habitability classifications.

---

## Future Scope

Planned extensions for theI can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog of the dataset with dynamically updating distribution histograms.
3.  **Model Performance:** Detailed analytics including accuracy comparisons, a high-contrast confusion matrix, and feature importance rankings.
4.  **Live Prediction Lab:**
    *   **Search by Planet Name:** Instantly classify known exoplanets with a confidence score.
    *   **Custom Parameters:** Input hypothetical stellar and orbital parameters to simulate an environment and receive real-time habitability classifications.

---

## Future Scope

Planned extensions for the SCOPE architecture include:
*   **JWST Atmospheric Data Integration:** Moving from geometric proxies to direct chemical evidence (e.g., detecting $H_2O$,I can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog of the dataset with dynamically updating distribution histograms.
3.  **Model Performance:** Detailed analytics including accuracy comparisons, a high-contrast confusion matrix, and feature importance rankings.
4.  **Live Prediction Lab:**
    *   **Search by Planet Name:** Instantly classify known exoplanets with a confidence score.
    *   **Custom Parameters:** Input hypothetical stellar and orbital parameters to simulate an environment and receive real-time habitability classifications.

---

## Future Scope

Planned extensions for the SCOPE architecture include:
*   **JWST Atmospheric Data Integration:** Moving from geometric proxies to direct chemical evidence (e.g., detecting $H_2O$, $CO_2$).
*   **Multi-Condition Habitability Label:** Expanding beyond a radius-only label to include limits on insolation and equilibrium temperatureI can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog of the dataset with dynamically updating distribution histograms.
3.  **Model Performance:** Detailed analytics including accuracy comparisons, a high-contrast confusion matrix, and feature importance rankings.
4.  **Live Prediction Lab:**
    *   **Search by Planet Name:** Instantly classify known exoplanets with a confidence score.
    *   **Custom Parameters:** Input hypothetical stellar and orbital parameters to simulate an environment and receive real-time habitability classifications.

---

## Future Scope

Planned extensions for the SCOPE architecture include:
*   **JWST Atmospheric Data Integration:** Moving from geometric proxies to direct chemical evidence (e.g., detecting $H_2O$, $CO_2$).
*   **Multi-Condition Habitability Label:** Expanding beyond a radius-only label to include limits on insolation and equilibrium temperature to reduce false positives (like lava worlds).
*   **Earth Similarity Index (ESI) Scoring:** Creating a composite 0-1 metric for candidate ranking.I can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog of the dataset with dynamically updating distribution histograms.
3.  **Model Performance:** Detailed analytics including accuracy comparisons, a high-contrast confusion matrix, and feature importance rankings.
4.  **Live Prediction Lab:**
    *   **Search by Planet Name:** Instantly classify known exoplanets with a confidence score.
    *   **Custom Parameters:** Input hypothetical stellar and orbital parameters to simulate an environment and receive real-time habitability classifications.

---

## Future Scope

Planned extensions for the SCOPE architecture include:
*   **JWST Atmospheric Data Integration:** Moving from geometric proxies to direct chemical evidence (e.g., detecting $H_2O$, $CO_2$).
*   **Multi-Condition Habitability Label:** Expanding beyond a radius-only label to include limits on insolation and equilibrium temperature to reduce false positives (like lava worlds).
*   **Earth Similarity Index (ESI) Scoring:** Creating a composite 0-1 metric for candidate ranking.
*   **Deep Learning Integration:** Applying Neural Networks directly to raw photometric time-series light curves.

---

## Team

*   **Arpan Kumar**I can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog of the dataset with dynamically updating distribution histograms.
3.  **Model Performance:** Detailed analytics including accuracy comparisons, a high-contrast confusion matrix, and feature importance rankings.
4.  **Live Prediction Lab:**
    *   **Search by Planet Name:** Instantly classify known exoplanets with a confidence score.
    *   **Custom Parameters:** Input hypothetical stellar and orbital parameters to simulate an environment and receive real-time habitability classifications.

---

## Future Scope

Planned extensions for the SCOPE architecture include:
*   **JWST Atmospheric Data Integration:** Moving from geometric proxies to direct chemical evidence (e.g., detecting $H_2O$, $CO_2$).
*   **Multi-Condition Habitability Label:** Expanding beyond a radius-only label to include limits on insolation and equilibrium temperature to reduce false positives (like lava worlds).
*   **Earth Similarity Index (ESI) Scoring:** Creating a composite 0-1 metric for candidate ranking.
*   **Deep Learning Integration:** Applying Neural Networks directly to raw photometric time-series light curves.

---

## Team

*   **Arpan Kumar**
*   **Affaz Hussain**
*   **Safwan Khan**
*   **Naman Paisal**

**Batch:** 2022–20I can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog of the dataset with dynamically updating distribution histograms.
3.  **Model Performance:** Detailed analytics including accuracy comparisons, a high-contrast confusion matrix, and feature importance rankings.
4.  **Live Prediction Lab:**
    *   **Search by Planet Name:** Instantly classify known exoplanets with a confidence score.
    *   **Custom Parameters:** Input hypothetical stellar and orbital parameters to simulate an environment and receive real-time habitability classifications.

---

## Future Scope

Planned extensions for the SCOPE architecture include:
*   **JWST Atmospheric Data Integration:** Moving from geometric proxies to direct chemical evidence (e.g., detecting $H_2O$, $CO_2$).
*   **Multi-Condition Habitability Label:** Expanding beyond a radius-only label to include limits on insolation and equilibrium temperature to reduce false positives (like lava worlds).
*   **Earth Similarity Index (ESI) Scoring:** Creating a composite 0-1 metric for candidate ranking.
*   **Deep Learning Integration:** Applying Neural Networks directly to raw photometric time-series light curves.

---

## Team

*   **Arpan Kumar**
*   **Affaz Hussain**
*   **Safwan Khan**
*   **Naman Paisal**

**Batch:** 2022–2026 | B.Tech CSE (Data Science)
**Institution:** Moradabad Institute of Technology, Moradabad (U.P.)
**Supervisor:** Mr. VarunI can definitely help you structure a detailed README file for your SCOPE project! While I can't generate a PDF file directly, I can write the content in standard Markdown format. You can then easily convert this Markdown into a PDF using various online tools or editors like VS Code or Typora.

Here is a comprehensive README structure based on the information in your report:

***

# SCOPE: System for Celestial Observation and Planetary Exploration

## Overview

**SCOPE** (System for Celestial Observation and Planetary Exploration) is a comprehensive end-to-end data science pipeline and interactive web dashboard. It is engineered to automatically classify the habitability of exoplanets using live observational telemetry from the NASA Exoplanet Archive.

This project addresses the critical data analysis bottleneck created by the exponential growth of confirmed exoplanets (now exceeding 6,000 entries). By moving beyond conventional static filtering, SCOPE captures the complex, non-linear interdependencies between stellar energy output, planetary orbital mechanics, and surface thermal conditions to provide a scientifically robust habitability assessment.

## Table of Contents
1. [Core Features](#core-features)
2. [Scientific Foundation](#scientific-foundation)
3. [Architecture](#architecture)
4. [Dataset & Features](#dataset--features)
5. [Machine Learning Models](#machine-learning-models)
6. [Technology Stack](#technology-stack)
7. [Installation & Setup](#installation--setup)
8. [Dashboard Modules](#dashboard-modules)
9. [Future Scope](#future-scope)
10. [Team](#team)

---

## Core Features

*   **Live Data Ingestion:** Establishes a direct, synchronous connection with the NASA TAP/sync API, automatically fetching up-to-date stellar and planetary parameters upon session initialization.
*   **Physics-Based Feature Engineering:** Transforms raw measurements into 11 scientifically meaningful predictors (e.g., Equilibrium Temperature, Insolation Flux) derived from peer-reviewed astrophysics literature.
*   **Data Leakage Mitigation:** Strictly excludes planetary radius (the basis of the label definition) from the training dataset, ensuring the model learns genuine physical correlations rather than memorizing a threshold.
*   **Dual-Model Architecture:** Trains Random Forest and Gradient Boosting classifiers in parallel, automatically deploying the superior model (Gradient Boosting achieved 81.6% accuracy).
*   **Interactive Streamlit Dashboard:** Provides a four-module user interface for exploring the dataset, analyzing model performance, and conducting real-time habitability predictions for both known exoplanets and hypothetical custom parameters.

---

## Scientific Foundation

SCOPE’s feature engineering and labeling logic are grounded in established astrophysics literature:

*   **Habitable Zone Boundaries:** Scaled dynamically based on stellar luminosity, following **Kopparapu et al. (2013)**.
*   **Habitability Labeling (The Fulton Gap):** The primary habitability label boundary is defined as $0.8 \le R \le 1.9\,R_\oplus$, identifying rocky super-Earths while excluding volatile-rich mini-Neptunes, based on **Fulton et al. (2017)**.
*   **Thermodynamic Predictors:** Equilibrium Temperature ($T_{eq}$) and Insolation Flux are calculated as key predictors, following the framework of **Kane et al. (2016)**.
*   **Orbital Eccentricity:** Included as a feature due to its significant impact on climate stability, per **Shields et al. (2016)**.

---

## Architecture

The SCOPE pipeline follows a linear, four-layer data flow:

1.  **Data Acquisition:** Raw JSON data fetched via the NASA Exoplanet Archive TAP API.
2.  **Preprocessing:** Application of median imputation for missing values and necessary type conversions.
3.  **Physics Engine:** Engineering of 11 advanced features, strictly excluding `pl_rade` (planetary radius) to prevent data leakage.
4.  **Machine Learning:** Parallel training of Random Forest and Gradient Boosting classifiers.
5.  **Interactive UI:** Deployment via a Streamlit web dashboard.

---

## Dataset & Features

**Source:** NASA Exoplanet Archive (`pscomppars` table).
**Total Records Analyzed:** ~6,273

### 11-Feature Training Set
1.  `pl_masse` (Raw): Planet mass in Earth masses
2.  `pl_orbper` (Raw): Orbital period
3.  `pl_orbsmax` (Raw): Semi-major axis in AU
4.  `pl_orbeccen` (Raw): Orbital eccentricity
5.  `sy_snum` (Raw): Number of stellar components
6.  `sy_pnum` (Raw): Number of planets in system
7.  `st_logg` (Raw): Stellar surface gravity
8.  `T_eq` (Engineered): Equilibrium Temperature (K)
9.  `insolation` (Engineered): Insolation flux
10. `in_hz` (Engineered): Binary flag for presence in Habitable Zone
11. `st_type` (Engineered): Categorical stellar spectral classification

*(Note: `pl_rade` is strictly excluded from training to prevent data leakage)*

---

## Machine Learning Models

The dataset presented a moderately imbalanced binary classification problem (approx. 24.8% habitable, 75.2% non-habitable).

*   **Baseline (4 Features, No Engineering):** Random Forest achieved 71.6% accuracy.
*   **Random Forest (11 Physics Features):** 300 trees, max depth 15. Achieved **76.7% accuracy**.
*   **Gradient Boosting (11 Physics Features):** 200 trees, max depth 5, learning rate 0.05. Achieved **81.6% accuracy**. (Selected for deployment).

**Feature Importance Insight:** Orbital distance (`pl_orbsmax`) and planetary mass (`pl_masse`) are the dominant predictive features, aligning with astrophysical theory.

---

## Technology Stack

*   **Language:** Python 3.10+
*   **Data Manipulation:** Pandas, NumPy
*   **API Integration:** Requests
*   **Machine Learning:** Scikit-Learn
*   **Visualization:** Matplotlib, Seaborn
*   **Dashboard UI:** Streamlit
*   **Deployment:** Google Colaboratory, Cloudflare Tunnel

---

## Installation & Setup

SCOPE is designed to be easily deployed via Google Colaboratory.

1.  Open a new Google Colab notebook and select a CPU runtime.
2.  Install required dependencies:
    ```bash
    !pip install streamlit pyngrok cloudflared
    ```
3.  Clone the repository or upload `scope_dashboard.py` to the working directory:
    ```bash
    !git clone [https://github.com/](https://github.com/)<username>/scope-dashboard.git
    ```
4.  Launch the Streamlit server and initiate the Cloudflare Tunnel:
    ```bash
    !streamlit run scope_dashboard.py &
    !cloudflared tunnel --url http://localhost:8501
    ```
5.  Open the `.trycloudflare.com` URL provided in the output. The dashboard will load within 60-90 seconds as the live data is fetched and models are trained.

---

## Dashboard Modules

1.  **Mission Overview:** Displays high-level KPIs, discovery timelines, detection methods, and an interactive Insolation-Radius scatter plot highlighting the Fulton Gap.
2.  **Data Explorer:** A filterable catalog of the dataset with dynamically updating distribution histograms.
3.  **Model Performance:** Detailed analytics including accuracy comparisons, a high-contrast confusion matrix, and feature importance rankings.
4.  **Live Prediction Lab:**
    *   **Search by Planet Name:** Instantly classify known exoplanets with a confidence score.
    *   **Custom Parameters:** Input hypothetical stellar and orbital parameters to simulate an environment and receive real-time habitability classifications.

---

## Future Scope

Planned extensions for the SCOPE architecture include:
*   **JWST Atmospheric Data Integration:** Moving from geometric proxies to direct chemical evidence (e.g., detecting $H_2O$, $CO_2$).
*   **Multi-Condition Habitability Label:** Expanding beyond a radius-only label to include limits on insolation and equilibrium temperature to reduce false positives (like lava worlds).
*   **Earth Similarity Index (ESI) Scoring:** Creating a composite 0-1 metric for candidate ranking.
*   **Deep Learning Integration:** Applying Neural Networks directly to raw photometric time-series light curves.

---

## Team

*   **Arpan Kumar**
*   **Affaz Hussain**
*   **Safwan Khan**
*   **Naman Paisal**

**Batch:** 2022–2026 | B.Tech CSE (Data Science)
**Institution:** Moradabad Institute of Technology, Moradabad (U.P.)
**Supervisor:** Mr. Varun Agarwal, Assistant Professor
