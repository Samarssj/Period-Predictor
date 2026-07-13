# 🌸 FlowCast

A single-file Streamlit app that predicts your next period start date using a machine learning model trained on real menstrual cycle data.

**[Live demo →](https://period-predictor-kxssmdhkv2qxjqymovkkro.streamlit.app)**

## What it does

- Log your period start dates, flow intensity, mood, and symptoms in a simple sidebar form
- Get a predicted next period start date + a likely date range
- Automatically switches from a simple average (early on) to a trained ML model once you've logged 3+ cycles
- View your cycle length trend over time in a chart
- Toggle between light and dark theme

## How the prediction works

- **New users (1–2 logged cycles):** falls back to a simple average of your logged cycle lengths — not enough data yet to trust a model
- **3+ logged cycles:** switches to a **Linear Regression** model trained on the [FedCycle dataset](https://www.kaggle.com/datasets/nikitabisht/fedcycledata) (159 women, ~1,665 real logged cycles), using features like your recent cycle lengths, luteal phase, menses length, and cycle history
- The model achieves an average error of **±1.8 days** on held-out test data

The dataset is embedded directly in the app file (as base64), so there's no separate data file or model file to manage — everything trains in-memory on first run and is cached for the session.

## Running locally

```bash
pip install streamlit pandas numpy scikit-learn
streamlit run period_predictor_app.py
```

That's it — no other files needed to run it locally.

## Deploying on Streamlit Community Cloud

1. Push `period_predictor_app.py` and `requirements.txt` to a GitHub repo
2. Go to [share.streamlit.io](https://share.streamlit.io) → sign in with GitHub
3. Click **New app** → select your repo → set the main file to `period_predictor_app.py` → Deploy

> Note: `requirements.txt` must be lowercase and sit alongside the app file — Streamlit Cloud looks for that exact filename to know what to install.

## Project structure

```
period_predictor_app.py   # everything: embedded dataset, model training, and the Streamlit UI
requirements.txt          # streamlit, pandas, numpy, scikit-learn
```

## Tech stack

- **Streamlit** — UI and app framework
- **scikit-learn** — Linear Regression / Random Forest model training
- **pandas / numpy** — data processing and feature engineering

## Disclaimer

This tool provides estimates for informational purposes only. It is not a substitute for medical advice, diagnosis, or contraception. Please consult a healthcare provider for medical guidance.
<img width="1440" height="900" alt="Screenshot 2026-07-13 at 16 38 23" src="https://github.com/user-attachments/assets/dfcec8be-bf34-48ed-a831-ab72a9620bbd" />

