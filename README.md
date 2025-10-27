# cs171-lol-draft-analysis
LoL Draft Analysis project for the CS 171 final project by Sai Wong and Ryan Rajaie

## Question & Research Topic

## Data Collection Plan

The first step to data collection would be to fetch existing data from the Riot Games API (https://developer.riotgames.com), which includes a variety of endpoints such as player information and match data. For our models, we plan to mostly gather match data rather than player information, so the main endpoints we utilize are mainly “match” and “league,” which go hand in hand. The only way to pull matches is from the “league” endpoint, which returns the top players (Master rank and above). With those players, we can pull each of their match histories to gather a large dataset of matches (filtering duplicates). Through this method, we would only have matches from the higher ranked players, so we currently focus on draft win prediction for this population of players. Each of the match data stores a large amount of information about the game (5K+ properties).

Sai: I initially had already pulled a lot of match data (around 200K matches) from the Europe West server, but filtered the matches to only include a specific type of champion. This means the amount of resulting matches that I have pulled are a lot less than 200K. The data is still in json format, so we need to clean this data by filtering the properties that we want for our model. This filtering can be done through pandas to obtain a single DataFrame that we can use to train our models.

## Model Plans

Our general plan for these models, as mentioned earlier, would be a supervised learning model suited for binary classification. From our data, our target column would be the label indicating if a certain team won or lost. We plan to make our features mostly based on the champions picked (10 total, 5 per team), which will be encoded in different ways depending on the outcome of our training. 

Sai: For this model, I would initially like to explore the impact of ensemble forest models, such as RandomForest and GradientBoostingClassifier. Because I believe that the task at hand can be modeled by individual decisions, such as if one player picks this champion, then goes down this path. If that player is in this specific role, then go down another path. Thus, this decision-based training seems suitable for our task and could give us reliable predictions. Moreover, these ensemble trees may handle sparse data better than a single tree, and if we were to one hot encode our data, then this could be beneficial. I can explore testing different encodings of the champions picked, possibly based on the metadata (general champion statistics) if results are not satisfactory from other encoding methods. 

## Timeline

Week 1 (10/26-11/1): Create data collection pipeline from Riot API.

Week 2 (11/2-11/8): Pre-process data (clean, filter, encode, split for train/test/val).

Week 3 (11/9-11/15): Iteratively construct models with desired features.

Week 4 (11/16-11/22): Refine and fine-tune models (explore hyperparameter tuning and comparing results).

Week 5 (11/23-11/29): Analyze results and create visualizations (provide metrics such as accuracy, recall, AUROC).

Week 6 (11/30-12/6): Prepare presentation and present project.

Week 7 (12/6-12/10): Make final adjustments and adjustments, submit.
