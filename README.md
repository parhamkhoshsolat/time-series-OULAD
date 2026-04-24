# Time Series Forecasting on OULAD

![Python](https://img.shields.io/badge/python-3.8%2B-yellow)
![PyTorch](https://img.shields.io/badge/pytorch-2.0%2B-red)

Forecasting student interactions with the Open University's Virtual Learning Environment using four modeling approaches: SARIMA, ARIMAX, Prophet, and CNN. The CNN achieved the best MAE and MAPE across all evaluation windows.

## Team

- Parham Khosh Solat
- Farshad Farahtaj
- Zahra Jafarinejad

## Approach

The OULAD dataset tracks weekly student clicks on VLE materials across multiple courses and presentations. The goal was to predict future interaction volume from historical patterns.

Each model handles time series differently. SARIMA and ARIMAX capture seasonality and external variables well; Prophet handles trend changes; the CNN learns temporal patterns directly from raw sequences. Lag features were engineered for ARIMAX and CNN — this measurably improved both.

All models were evaluated on MAE and MAPE to allow direct comparison.

## Dataset

[Open University Learning Analytics Dataset (OULAD)](https://www.kaggle.com/datasets/anlgrbz/student-demographics-online-education-dataoulad) — CC BY 4.0

`studentVle.csv` exceeds 400MB and is excluded from this repo. Download from Kaggle and place in `/data`.

## Project Structure

```
├── data/                  # Download from Kaggle
├── notebooks/
│   └── Harware_and_Software_Mod_B_Final_Project.ipynb
├── src/
│   └── Hardware_and_sofware_Mod_B_Final_Project_Sreamlit_version.py
├── models/
│   └── tuner0.json
├── docs/
│   └── Harware_and_Software_Mod_B_Final_Project.pdf
├── requirements.txt
└── README.md
```

## Setup

```bash
git clone https://github.com/Alirezakhoshsolat/time-series-OULAD.git
cd time-series-OULAD
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/Harware_and_Software_Mod_B_Final_Project.ipynb
```

To run the Streamlit app:

```bash
streamlit run src/Hardware_and_sofware_Mod_B_Final_Project_Sreamlit_version.py
```

## Course

Hardware and Software for Big Data (Module B) — University of Naples Federico II
Instructor: Prof. Flora Amato · July 2024

## License

MIT
