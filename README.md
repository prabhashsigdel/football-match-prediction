# football-match-prediction

Predicting football match scorelines with a Poisson model, then comparing it against other algorithms. Python, pandas, scipy.

## Status
This is the starting phase. The current model only uses final scores from two seasons, which is the simplest possible version. As the project goes on it'll use a lot more data: shots, corners, fouls and cards, then full event data with pitch coordinates (where every shot and pass happened) to build my own xG model. Each upgrade gets tested against the baseline to see if it actually improves the predictions.

## How it works
1. Load two Premier League seasons of results (2025/26 and 2026/27)
2. Work out each team's attack and defence strength, home and away, compared to the league average
3. Turn those into expected goals for each team
4. Use a Poisson distribution to get the chance of every scoreline (0-0 up to 6-6)
5. Add up the scorelines into home win / draw / away win

## First prediction: Man City vs Fulham
- Expected goals: Man City 2.23, Fulham 0.60
- Man City win 74%, draw 17%, Fulham win 8%
- Most likely score: 2-0 (14.7%)

## Known limitations
- Only uses goals, not shots or chances
- Both seasons are weighted equally
- Promoted teams have very few games, so their numbers are shaky
- Poisson assumes each team's goals are independent of the other's

## Roadmap

### 1. Backtest the baseline
- [ ] Train on the early part of the season, predict the rest
- [ ] Measure accuracy, log loss and Brier score
- [ ] Compare against bookmaker odds as a benchmark

### 2. Fix the obvious weaknesses
- [ ] Recency weighting, so recent matches count more
- [ ] Better handling of promoted teams

### 3. Add more match stats
- [ ] Shots, shots on target, corners, fouls, cards
- [ ] Check which ones actually improve predictions

### 4. Compare other models
- [ ] Dixon-Coles (fixes Poisson underrating low-scoring draws)
- [ ] Elo ratings
- [ ] Logistic regression and other ML models with scikit-learn

### 5. Event data
- [ ] StatsBomb open data with pitch coordinates
- [ ] Build my own xG model from shot positions

## Run it
```
pip install pandas scipy matplotlib notebook
jupyter notebook mancity_vs_fulham_poisson.ipynb
```

## Data
- Match data from [football-data.co.uk](https://www.football-data.co.uk)
