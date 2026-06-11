 Indian Railways Train Delay Prediction

I built this project to understand what actually causes train delays in India and whether those delays can be predicted from the data available before or during a journey.

The dataset has 100,000 train journey records with information like distance, weather, whether there was a signal failure or engine breakdown, how many stops the train makes, and how late the previous train on the same route was. The target we are trying to predict is how many minutes late the train arrives.

---

## What this project does

There are two things I tried to figure out:

**First**, can we predict the exact delay in minutes? This is a regression problem. I trained a Linear Regression model and a Random Forest on the same data and compared how close their predictions were to the real delays.

**Second**, can we at least classify whether a delay will be short or long? I defined short as 30 minutes or under and long as anything above 30 minutes. This gave a clean binary classification problem and I tested Logistic Regression, Random Forest, and Gradient Boosting on it.

---

## Files in this repo

- `Final.ipynb` — the main notebook with all the analysis, cleaning, models, and plots
- `stratquest_dataset.csv` — the dataset, 100,000 rows of Indian Railways journey data
- `README.md` — this file

---

## What I found

The single strongest predictor of arrival delay is how late the previous train on the same route was. Delays cascade — if the train before you was late, your train is almost certainly going to be late too. Departure delay is the second biggest factor, which makes sense since a train that leaves late almost always arrives late.

Signal failures and engine breakdowns push average delays up noticeably. Weather mattered less than I expected, though monsoon months (June through September) did show higher average delays across the board.

Random Forest performed significantly better than Linear Regression on this data, which tells me the relationship between features and delay is not a straight line. The data has interactions that a simple linear model cannot capture.

---

## How to run it

You need Python with pandas, numpy, matplotlib, seaborn, and scikit-learn installed. Clone the repo, put the CSV in the same folder as the notebook, and run all cells from top to bottom.

```bash
git clone https://github.com/mayanktiwari-cmd/Indian-railways-train-delay-prediction-classification-with-EDA
cd Indian-railways-train-delay-prediction-classification-with-EDA
jupyter notebook Final.ipynb
```

---

## Data cleaning notes

The dataset had a few issues I had to deal with. Temperature and humidity were stored as strings instead of numbers, so those needed converting. The WeatherCondition column had a mix of proper labels like Rain and Fog alongside what looked like random numeric codes — those got cleaned out and replaced with the most common valid label. About 8000 rows had missing weather measurements which I filled with column medians. After all that, the dataset was fully clean with no missing values going into any model.

---

Made by Mayank Tiwari
