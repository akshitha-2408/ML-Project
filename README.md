***EcoPlate: Smart Food Intelligence for Sustainable Kitchens***
----What is the project about----
EcoPlate is a machine-learning-based system that helps restaurants predict how many plates of food customers may need. It then recommends how much food to prepare, estimates the expected leftover food, and identifies suitable NGOs that may collect the surplus.
The main aim is to reduce unnecessary food waste and support food redistribution.
Why is this project needed?
Restaurants cannot always predict the exact number of customers each day. Demand changes because of reservations, walk-in customers, weekdays, weather, holidays, festivals, and menu preferences. Preparing too much food may create waste, while preparing too little may leave customers without food.
EcoPlate uses historical data to make better preparation decisions.
*******workflow*******
1. Restaurant and NGO Datasets
Historical sales, menu items, reservations, weather, holidays, NGO capacity and availability

2. Data Cleaning and Feature Engineering
Clean records, prepare features, encode categories and scale numerical values

3. Attention + Gated Temporal Neural Network
Learns patterns from previous 7 observations to predict food demand

4. Demand Prediction
Predicts the required number of plates

5. Preparation and Surplus Calculation
Adds a 10-plate preparation margin and estimates the expected surplus

6. NGO Filtering and Ranking
Checks food type, availability, capacity and pickup information

7. Final Recommendation
Displays predicted demand, preparation quantity, expected surplus and a suitable NGO


3. Dataset used
Dataset	Details
Restaurant dataset	11,493 records, 10 restaurants and 6 menu items
NGO dataset	15 organizations
Prediction target	Quantity_Sold
Historical input	Previous 7 observations for each restaurant-menu sequence
NGO matching	Food type, availability, capacity and pickup information
The two datasets are not directly merged row by row. Instead, the predicted surplus from the restaurant process is used to select an eligible NGO.
4. Code explanation: cell by cell
Your notebook contains 37 code cells and one empty cell. The code cells are grouped into five main stages.
Stage 1 — Data preparation (Cells 1–8)
Cell 1

Import libraries
Imports Pandas, NumPy, Matplotlib, TensorFlow and Scikit-learn. These libraries are used for data processing, plotting, neural-network training and model evaluation.



Cell 2

Load datasets
Reads EcoPlate_Cleaned.csv and NGO_Cleaned.csv, then displays their sizes and column names.



Cell 3

Clean the data
Converts dates and numerical values, handles missing values, removes duplicate records and sorts the restaurant data chronologically.



Cell 4

Feature engineering
Creates additional time features, such as day number, year, weekend indicator, month number and week number. Quantity_Sold is the target to predict.



Cell 5

Dataset statistics
Shows the number of restaurants, menu items, weather categories, festivals and the distribution of food sales.



Cell 6

Split the dataset
Divides the data chronologically into training, validation and testing sets, so future dates are not used to train the model.



Cell 7

Categorical encoding
Converts categories such as restaurant names, menu items and weather into numerical IDs that the neural network can process.



Cell 8

Numerical feature scaling
Uses StandardScaler to put numerical inputs on comparable scales, helping model training.



Stage 2 — Proposed neural network (Cells 9–15)
- Cell 9 — Temporal sequence creation: Groups historical observations into 7-step sequences for predicting demand.
- Cell 10 — Prepare neural-network inputs: Separates categorical and numerical features into the required input arrays.
- Cell 11 — Build the proposed model: Creates the EcoPlate neural network using categorical embeddings, a numerical projection layer, Multi-Head Attention and GRU-based temporal layers.
- Cell 12 — Train the model: Learns patterns from the training dataset and checks performance on the validation dataset. Early stopping helps prevent unnecessary training.
- Cell 13 — Training and validation graph: Displays the loss curves to show how training progresses.
- Cell 14 — Test the model: Generates demand predictions on the test dataset and calculates MAE, RMSE and R².
- Cell 15 — Actual versus predicted graph: Compares the model's predictions with actual food sales.
What are Attention and GRU?
Multi-Head Attention: Helps the model learn which historical observations are important for predicting demand.
GRU (Gated Recurrent Unit): Learns sequential patterns and changes across the historical observations.
Embeddings: Convert categorical information into learnable numerical representations.
Together, these components form your proposed Attention + Gated Temporal model.
Stage 3 — Compare models (Cells 16–24)
- Cell 16: Prepares the historical sequences for a baseline model.
- Cell 17: Trains and evaluates a Random Forest regression model.
- Cell 18: Builds and trains a GRU baseline neural network.
- Cell 19: Evaluates GRU predictions using test data.
- Cell 20: Creates a simple baseline using previous-day sales.
- Cell 21: Compares all models using MAE, RMSE and R².
- Cell 22: Draws a graph comparing the models' MAE values.
- Cell 23: Identifies the model with the lowest MAE.
- Cell 24: Saves the comparison results to EcoPlate_Model_Comparison.csv.
Your reported model comparison
Model	MAE	RMSE	R²
Previous-Day Baseline	27.076	34.102	-0.006
Random Forest	17.724	22.065	0.579
GRU	18.693	23.668	0.516
EcoPlate Attention + Gated Temporal	17.534	21.339	0.606
The proposed model has the lowest MAE and RMSE and the highest R² among these four evaluated models.
- MAE: Average absolute difference between actual and predicted demand.
- RMSE: Prediction error metric that penalizes larger errors more heavily.
- R²: Indicates how much of the variation in the test demand is explained by the model.
Stage 4 — Restaurant selection and prediction (Cells 25–32)
- Cell 25: Displays restaurants and lets the user select one by number.
- Cell 26: Displays menu items for the selected restaurant and lets the user select one.
- Cell 27: Automatically retrieves the latest available data for that restaurant and menu item.
- Cell 28: Plots the historical sales trend.
- Cell 29: Prepares the latest 7-observation sequence for prediction.
- Cell 30: Uses the trained model to predict the expected demand in plates.
- Cell 31: Determines the food type, such as Veg or Non-Veg.
- Cell 32: Adds the preparation margin and calculates expected surplus.
The notebook's preparation policy adds 10 plates to the predicted demand:
\[
\text{Preparation}=\text{Predicted Demand}+10
\]

\[
\text{Expected Surplus}=\text{Preparation}-\text{Predicted Demand}
\]

This is a decision rule, not a separate prediction of actual leftover food. The resulting surplus is expected surplus, assuming demand matches the prediction.
Stage 5 — NGO recommendation and final output (Cells 33–37)
- Cell 33: Prepares the NGO dataset for matching.
- Cell 34: Filters and ranks NGOs based on food-type compatibility, availability and capacity.
- Cell 35: Displays the final EcoPlate recommendation.
- Cell 36: Shows a table of ranked NGO candidates.
- Cell 37: Summarizes the model performance and final recommendation.
- Cell 38: Empty cell; it does not perform any operation.
The current notebook does not calculate actual restaurant-to-NGO distance because restaurant coordinates are not available in the restaurant dataset.
5. Example of the final result
Your notebook produced this example:
EcoPlate prediction example
Restaurant

Aroma Kitchen

Menu item

Butter Chicken


Predicted demand

135 plates

Recommended preparation

145 plates

Expected surplus

10 plates


Recommended NGO: Feeding Hands Foundation
Area: Gachibowli · Capacity: 250 meals
Distance: Unavailable



The system predicts 135 plates, applies the 10-plate safety margin to recommend preparing 145 plates, and estimates 10 plates of surplus. It then uses the surplus and NGO information to identify a suitable organization.
