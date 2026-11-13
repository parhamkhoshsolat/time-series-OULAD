# Time-Series Forecasting on OULAD

Forecasting daily student activity on the Open University learning platform with SARIMA, ARIMAX, Prophet and a custom 1D CNN.

<p>
  <a href="https://www.parhamkhoshsolat.com/projects/oulad-timeseries"><img src="https://img.shields.io/badge/Write--up-portfolio-5dc6ff?style=flat-square&labelColor=0a1422" alt="Write-up: portfolio"></a>
  <img src="https://img.shields.io/badge/2024-team_of_3-5dc6ff?style=flat-square&labelColor=0a1422" alt="2024: team of 3">
</p>

## Overview

The 420 MB OULAD click-stream is aggregated to 808 daily totals and log-transformed. The statistical models use 7 lag features; the CNN reads a 30-day input window.

## What I did

I built the full pipeline: aggregation, feature engineering, the four models and a Streamlit app.

## Results

The CNN scored MAE 0.20 on log clicks on a chronological hold-out. The statistical models were not scored on the same hold-out, so this is not a like-for-like ranking.

## Dataset

[Open University Learning Analytics Dataset (OULAD)](https://www.kaggle.com/datasets/anlgrbz/student-demographics-online-education-dataoulad), CC BY 4.0. `studentVle.csv` is over 400 MB and is not in this repo: download it from Kaggle and place it in `data/`.

## Run it

```bash
git clone https://github.com/parhamkhoshsolat/time-series-OULAD.git
cd time-series-OULAD
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/Harware_and_Software_Mod_B_Final_Project.ipynb
# Streamlit app
streamlit run src/Hardware_and_sofware_Mod_B_Final_Project_Sreamlit_version.py
```

## Project layout

```
├── data/        # download from Kaggle
├── notebooks/Harware_and_Software_Mod_B_Final_Project.ipynb
├── src/Hardware_and_sofware_Mod_B_Final_Project_Sreamlit_version.py
├── models/tuner0.json
└── requirements.txt
```

## Team & course

Hardware and Software for Big Data (Module B), University of Naples Federico II, July 2024. Instructor: Prof. Flora Amato. Team: Parham Khosh Solat, Farshad Farahtaj, Zahra Jafarinejad.

## License

MIT. See [`LICENSE`](LICENSE).

---

Part of my portfolio: [parhamkhoshsolat.com](https://www.parhamkhoshsolat.com)
