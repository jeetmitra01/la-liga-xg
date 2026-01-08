# La Liga xG

### What is xG?

Expected goals(xG) measures the probability of a shot resulting in a goal.<br>Values range from 0 to 1 and are measured using historical data using factors like shot location, defensive pressure, shot angle, body part, etc.<br> xG can be useful in measuring a team's offensive performance, shot selection, and whether a team/player is able to finish their chances.

### Why La Liga?

I chose La Liga because it is a high quality league with a large amount of open-play shots per game. It is also home to my favorite sports team - FC Barcelona. 

### Data source (StatsBomb Open Data)

From the research I did StatsBomb data fit the needs I had for this project which started with relatively small goals. They do possess mre advanced data, from shot defensive pressure to pass height, things that could be useful in helping create a better model.

### Feature engineering

The two key features that needed to be calculated for this project were Distance(closer is generally better) and Angle(the more goal you can see the more likely you are to score). Using statsbomb's grid system which assigns an X and Y coordinate to each shot both distance to goal and angle of goal visible become very easy to calculate. Other features like shot type, shot body part and play pattern are provided by StatsBomb.

### Models tried

I started by using a linear regression model, this turned out eventually (atleast in terms of logloss and ROC-AUC score) to be the best for this version of the project. I did use XGBoost but before calibration I saw very poor scores on the important metrics as well as when comparing with the ideal curve of Observed Goal Rate vs Predicted XG. While Calibration did help the exra computational resources for little to no gain in predictive performance does not seem like a worthwhile tradeoff.

### Limitations

One of the limitations of this current implementation other than it not being very accurate for higher probabilities is that it does not provide any information regarding penalties. I removed penalties since they can heavily skew the probabilities for shots near the penalty spot, but a seperate model with penalty data only or one that is capable of isolating the shot type variable would be better.
