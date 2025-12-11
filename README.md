# cs171-lol-draft-analysis

League of Legends draft win prediction project for the CS 171 final by **Sai Wong** and **Ryan Rajaie**.

This project trains machine learning models to predict match outcomes using only champion draft information from high-elo ranked games.

---

## Research Question

How accurately can we predict the outcome of a League of Legends match using only the 5v5 champion draft?

League of Legends is a 5v5 competitive game where each player selects a unique champion with specific strengths, weaknesses, and strategic roles. Because counterpicks and team composition strongly influence outcomes, we frame this as a **binary classification problem**:
**Will Blue team win or lose based only on champion draft?**

---

## Data Collection

Data is collected using the official Riot Games API: [Riot Developer Portal](https://developer.riotgames.com)

We primarily use:

- **League endpoint** to fetch high-elo players (Master+)
- **Match endpoint** to fetch ranked match histories

Only high-ranked matches are used. Each match contains thousands of raw properties, which are filtered down to draft and outcome features.

---

### Encoding Approaches by Author

**Sai**

- Encodes champions using **both champion identity and champion metadata** (base stats and general performance indicators).
- This allows models to learn from **inherent champion strength, scaling, and statistical profiles** in addition to draft composition.

**Ryan**

- Uses a **hybrid encoding approach**:
  - ~1700 one-hot features for **champion × role × team side** (e.g., Blue Ahri Mid, Red Leona Support).
  - ~340 additional binary features for **team-level champion presence** (e.g., `blue_has_ziggs`, `red_has_kaisa`).
- Produces a sparse matrix with exactly **10 role-specific activations per match**, plus team-level indicators.

---

## Models

We apply **supervised binary classification** where:

- Target: Match outcome (Blue win = 1, Red win = 0)
- Features: Champion draft encodings

---

### Model Approaches

**Sai**

- Random Forest
- Gradient Boosting Classifier
- Experiments with champion metadata-based encodings

**Ryan**

- Logistic Regression on sparse one-hot champion-role-side matrix with team-level indicators
- Treats each champion-role-side as a distinct learned coefficient

---

## Evaluation Metrics

We analyze:

- Accuracy
- Precision / Recall
- AUROC
- Confusion Matrix

---

## Timeline

- **Week 1:** Data collection pipeline
- **Week 2:** Cleaning, filtering, encoding-
- **Week 3:** Model construction
- **Week 4:** Hyperparameter tuning
- **Week 5:** Metrics + visualization
- **Week 6:** Presentation
- **Week 7:** Final submission

---

## Setup Instructions

#### Riot API Access

You must generate a Riot API key: https://developer.riotgames.com
Keys expire every 24 hours.

---

## Dependencies (Both of us)

pandas
numpy
scikit-learn
torch
riotwatcher
cassiopeia
matplotlib
requests
python-dotenv
typing
pathlib
datetime
time
itertools
os
json
pickle
seaborn
gzip
io

Install with:
`pip install -r requirements.txt`

---

## Future Work Future work may include: (Ryan)

- Champion synergy/matchups modeling
- Adding features for patches, elo, player data (champ winrate/mastery, rank, etc.)
- Pick-order draft simulation

## Future Work and Notes (Sai)

- Project roles are indicated by directories labeled with our names (the files we worked on)
- Data collection (as explained in the notebook) may not be reproducible because the package that calls the API is very unstable, but I provide the data already so you can run the model training notebook
- I would want to get more points of data rather than having ~15K points because there are a large number of combinations of characters that can be played per match, and I want this variation within my data to get higher accuracies.
- Encoder architecture could replace my API-based, static embedding lookup that I have right now.
