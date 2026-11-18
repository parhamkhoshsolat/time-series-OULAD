# Time-Series Forecasting on OULAD

Forecasting daily student activity on the Open University learning platform with SARIMA, ARIMAX, Prophet and a custom 1D CNN.

<p>
  <a href="https://www.parhamkhoshsolat.com/projects/oulad-timeseries"><img src="https://img.shields.io/badge/Write--up-portfolio-5dc6ff?style=flat-square&labelColor=0a1422" alt="Write-up: portfolio"></a>
  <img src="https://img.shields.io/badge/2024-team_of_3-5dc6ff?style=flat-square&labelColor=0a1422" alt="2024: team of 3">
</p>

## Overview

The OULAD click-stream (`studentVle.csv`, over 400 MB) is summed to daily total clicks, about 2.3 years of days (January 2013 to April 2015), and log-transformed. Each course presentation is placed on the calendar by assuming B courses start on 1 February and J courses on 1 October; OULAD itself gives only relative days. The step that builds the daily file (`time_series_vle_interactions.csv`) from `studentVle.csv` is not in this repo.

- **SARIMA and ARIMAX**: both are statsmodels SARIMAX models on the differenced log series, with lagged copies at 1, 2, 3, 7, 14, 21 and 28 days as inputs. They use 808 days (12 February 2013 to 30 April 2015), the rows left after differencing and lagging.
- **Prophet**: a grid search over 24 settings plus a monthly term. Prophet uses no lag features.
- **1D CNN**: reads a 30-day window of past log clicks; trained on the first 80% of days and tested on the last 20% in time order.

## What I did

I built the pipeline: feature engineering, the four models and a Streamlit app.

## Results

The CNN scored a mean absolute error of 0.20 on log daily clicks (MAPE 1.9% of the log value) on the chronological hold-out, the last 20% of days (about 160 days).

This is the only real hold-out score in the project:

- SARIMA and ARIMAX were fitted on all 808 days. Their printed MAE (0.122 and 0.121) compares a forecast of the 240 days after the data ends with the last 240 observed days, which are different dates, so those numbers do not measure forecast quality.
- Prophet was scored on its own training data (best in-sample MAE 0.203).
- The models are therefore not ranked against each other, and the comparison chart in the Streamlit app should not be read as a ranking.

### Limits

- **No naive baseline.** No simple benchmark such as "same as yesterday" or "same weekday last week" was run on the same hold-out, so MAE 0.20 cannot be called good or bad on its own. The daily data file is not committed, so the baseline could not be added here.
- **Light leakage in the CNN pre-processing.** The z-scores used to flag unusual days and the median used to replace them are computed over the whole series, test period included. The test set is also passed as `validation_data`, but training runs a fixed 50 epochs with no early stopping, so it does not choose the model.
- **The CNN plot in the notebook is shifted.** Predictions are drawn 30 days earlier than the dates they belong to (the 30-day window is not accounted for), and actual values for the test period are not drawn. The Streamlit app now plots both at the right dates.
- **Assumed calendar dates.** Peaks at 1 February and 1 October may come from the date mapping above rather than from student behaviour. Errors are on the log scale.
- `models/tuner0.json` is empty; the CNN was not tuned.

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

The notebook reads the OULAD CSV files (`studentVle.csv`, `studentInfo.csv`, `courses.csv` and the others) from a folder on my own machine (`D:\study\...\archive\`). To re-run it, put the files in `data/` and change those paths to `data/`. Its cells were run out of order during the project, so the saved run numbers are not in sequence.

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
