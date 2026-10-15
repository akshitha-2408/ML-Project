 EcoPlate: Smart Food Intelligence for Sustainable Kitchens

 Project Overview

EcoPlate is a machine-learning-based project that predicts restaurant food demand, recommends food preparation quantities, estimates expected surplus, and identifies suitable NGOs for surplus-food redistribution. It uses historical restaurant data and an Attention + Gated Temporal neural network to support better kitchen planning and reduce unnecessary food waste.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Objectives

- Predict restaurant food demand using historical sales and contextual features.
- Recommend suitable food preparation quantities.
- Estimate expected surplus after demand prediction.
- Compare the proposed neural network with traditional and recurrent machine-learning models.
- Filter and rank NGOs based on food type, availability, capacity, and pickup information.
 ------------------------------------------------------------------------------------------------------------------------------------------------------------------

Models Used

--> Module 1: Previous-Day Sales Baseline

This baseline uses previous-day sales as the demand prediction. It provides a simple reference for evaluating more advanced models.

--> Module 2: Random Forest Regression

This module uses a Random Forest model to learn relationships between historical restaurant features and food demand.

--> Module 3: GRU Neural Network

This module uses Gated Recurrent Unit (GRU) layers to learn sequential patterns from historical food-demand data.

---> Module 4: EcoPlate Attention + Gated Temporal Model

This is the proposed neural-network model. It combines categorical embeddings, numerical feature projection, Multi-Head Attention, and GRU-based temporal learning to predict food demand.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Dataset

The project uses two datasets:

### Restaurant Dataset

- Total records after cleaning: 11,493
- Restaurants: 10
- Menu items: 6
- Features include restaurant name, menu item, date, reservations, walk-in customers, previous-day sales, average sales, weather, holidays, festivals, quantity prepared, and quantity sold.

### NGO Dataset

- Total organizations: 15
- Features include NGO name, location, meal capacity, accepted food type, availability, pickup window, and contact information.

The restaurant and NGO datasets are connected through the decision-making pipeline rather than being directly merged row by row.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Technologies Used

- Python
- Anaconda Jupyter Notebook
- Pandas and NumPy
- TensorFlow / Keras
- Scikit-learn
- Matplotlib
- Machine Learning and Deep Learning
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Evaluation Metrics

The demand-prediction models are evaluated using:

- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- Coefficient of Determination (R²)
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Results

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Previous-Day Baseline | 27.076 | 34.102 | -0.006 |
| Random Forest | 17.724 | 22.065 | 0.579 |
| GRU | 18.693 | 23.668 | 0.516 |
| **EcoPlate Attention + Gated Temporal** | **17.534** | **21.339** | **0.606** |

The proposed EcoPlate model achieved the lowest MAE and RMSE and the highest R² among the evaluated models.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Example Prediction

For a selected restaurant and menu item:

- Restaurant: Aroma Kitchen
- Menu item: Butter Chicken
- Predicted demand: 135 plates
- Recommended preparation: 145 plates
- Expected surplus: 10 plates
- Recommended NGO: Feeding Hands Foundation
- NGO area: Gachibowli
- NGO capacity: 250 meals

The preparation quantity uses a fixed 10-plate safety margin. The surplus is an estimate based on predicted demand, not a measurement of actual leftover food.

## NGO Recommendation

The NGO recommendation module filters and ranks organizations using:

- Food-type compatibility
- NGO availability
- Meal capacity
- Pickup-window information

**Limitation:** The restaurant dataset does not contain restaurant coordinates, so actual restaurant-to-NGO geographical distance is not calculated in the current implementation.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Project Structure

- EcoPlate.ipynb – Data preparation, model training, evaluation, demand prediction, and NGO recommendation.
- EcoPlate_Cleaned.csv – Cleaned restaurant dataset.
- NGO_Cleaned.csv – Cleaned NGO dataset.
*Note: Update these filenames if your actual uploaded files have different names.*
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Conclusion

EcoPlate combines restaurant demand prediction, preparation planning, surplus estimation, and NGO recommendation in a connected workflow. The proposed Attention + Gated Temporal model outperformed the evaluated baselines on the reported test metrics, providing a foundation for more informed food preparation and surplus redistribution.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Future Enhancements

- Evaluate separate 7-day, 14-day, and 30-day forecasting windows.
- Add restaurant coordinates for distance-aware NGO recommendations.
- Integrate real-time NGO availability and pickup confirmation.
- Add uncertainty estimates to support safer preparation decisions.
- Develop a web application for restaurant staff and NGO coordinators.
- Evaluate the system's real-world impact on food waste and redistribution.
