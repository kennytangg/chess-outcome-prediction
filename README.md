# Data Science
Fundamental of Data Science final project (semester 3)

> **Note**: This is ongoing undergraduate research. 

## Dataset
For this research, I use the data from January 2024 to December 2024 
- Original plan was using lichess dataset: [Lichess](https://database.lichess.org/)

However the file size is too big, that I change it to a filtered version which is [Lichess Elite](https://database.nikonoel.fr/) . 

## Project Structure

```
├── data/                     
│   ├── chess_games_clean.csv
│   ├── chess_games_feature_60_sf.csv
│   ├── chess_games_feature.csv
│   ├── chess_games_raw.csv
│   └── lichess_elite_2024_full.pgn
├── images/                   # images used in report
│   ├── decision_tree.png
│   ├── logistic_regression.png
│   ├── neural_network.png
│   ├── random_forest.png
│   └── xgboost.png
├── models/                   
│   ├── pregame/              # pregame models
│   ├── early_moves/          # first k moves models
│   ├── early_moves_stockfish/# first k moves + small stockfish
│   └── full_game/            # full game models
├── notebooks/                 
│   ├── 01_convert/           # convert raw pgn to csv
│   ├── 02_preprocessing/     # data preprocessing
│   ├── 03_eda_features/      # feature engineering and EDA
│   ├── image.ipynb
│   ├── statistics.ipynb      
│   └── stockfish.ipynb
├── pyproject.toml            # Dependencies 
├── uv.lock                   
└── README.md
```

## Baseline
This is a chess prediction where a chess game can have three outcome:

1. **Random guessing: 33.3%** (win/loss/draw)
2. **First move win: 46.1%** (always predict white win)

## Results
  
**Model Performance by Game Depth**

> Only tested with one random_state = 42 and constraints are no player history, no search and all are 2300++ ELO games
 
| Move Depth | XGBoost | Neural Network (MLP) | Random Forest | Logistic Regression | Decision Tree |
|------------|---------|---------------------|---------------|---------------------|---------------|
| **Pre-game only** (no moves) | 58.31% | 58.28% | 58.12% | 58.12% | 57.32% |
| **First 10 moves** (20 half-moves) | 58.55% | 60.02% | 58.52% | 58.19% | 57.37% |
| **First 20 moves** (40 half-moves) | 60.01% | 60.02% | 59.89% | 59.17% | 57.51% |
| **First 30 moves** (60 half-moves) | 62.69% | 62.79% | 62.55% | 61.15% | 59.29% |
| **First 35 moves** (70 half-moves) | 63.19% | 63.25% | 63.08% | 61.74% | 59.66% |
| **First 40 moves** (80 half-moves) | 63.64% | 63.74% | 63.55% | 61.84% | 59.57% |
| **All moves** (full game) | 81.71% | **90.58%** | 81.95% | 73.72% | 83.28% |

**At 60 half-moves with Stockfish evaluation added as a feature:**
> This is using 150k sample and 0.2s movetime

| Model | No Engine | With Stockfish |
|-------|-------------|----------------|
| XGBoost | 62.69% | 62.87% |
| Neural Network | 62.79% | 62.33% |
| Random Forest | 62.55% | 62.33% |
| Logistic Regression | 61.15% | 61.47% |
| Decision Tree | 59.29% | 55.19% |

> This is using 50k sample and 20 depth

| Model | No Engine | With Stockfish |
|-------|-------------|----------------|
| XGBoost | 62.69% | 62.34% |
| Neural Network | 62.79% | 61.70% |
| Random Forest | 62.55% | 61.92% |
| Logistic Regression | 61.15% | 60.92% |
| Decision Tree | 59.29% | 52.29% |
