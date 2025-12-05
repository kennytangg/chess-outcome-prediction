# Data Science
Fundamental of Data Science final project (semester 3)

> **Note**: This is ongoing undergraduate research. 

## Dataset
For this research, I use the data from January 2024 to December 2024 
- Original plan was using lichess dataset: [Lichess](https://database.lichess.org/)

However the file size is too big, that I change it to a filtered version which is [Lichess Elite](https://database.nikonoel.fr/) . 

## Results
Model Performance by Game Depth

| Move Depth | XGBoost | Neural Network (MLP) | Random Forest | Logistic Regression | Decision Tree |
|------------|---------|---------------------|---------------|---------------------|---------------|
| **Pre-game only** (no moves) | 58.31% | 58.28% | 58.12% | 58.12% | 57.32% |
| **First 10 moves** (20 half-moves) | 58.55% | 60.02% | 58.52% | 58.19% | 57.37% |
| **First 20 moves** (40 half-moves) | 60.01% | 60.02% | 59.89% | 59.17% | 57.51% |
| **First 30 moves** (60 half-moves) | 62.69% | 62.79% | 62.55% | 61.15% | 59.29% |
| **First 35 moves** (70 half-moves) | 63.19% | 63.25% | 63.08% | 61.74% | 59.66% |
| **First 40 moves** (80 half-moves) | 63.64% | **63.74%** | 63.55% | 61.84% | 59.57% |

At 60 half-moves with Stockfish evaluation added as a feature:

| Model | Engine-Free | With Stockfish | Change |
|-------|-------------|----------------|--------|
| XGBoost | 62.69% | 62.88% | +0.19% |
| Neural Network | 62.79% | 62.09% | -0.70% |
| Random Forest | 62.55% | 62.25% | -0.30% |
| Logistic Regression | 61.15% | 61.44% | +0.29% |
| Decision Tree | 59.29% | 54.45% | -4.84% |
