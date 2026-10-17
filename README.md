# Smart Truck Trip Prediction

This is a Python machine learning project I built to predict fuel consumption and transport price for truck trips between Iranian cities, using trip data from an Excel file.

## About the Project
I wanted to see if a machine learning model could estimate how much fuel a truck needs and how much a trip costs, based on the origin city, destination city and cargo weight. I trained two separate Random Forest models: one for fuel and one for price.

## Dataset
I used my own Excel file (`transport_data.xlsx`) with 22 trips between Iranian cities, like Mashhad → Dezful or Tehran → Mashhad.

- Columns: origin_city, destination_city, distance_km, weight_ton, fuel_liter, price_toman
- Input features: distance_km, weight_ton
- Targets: fuel_liter, price_toman

The dataset is small, so I see this project as a learning exercise and proof of concept, not a production model.

## What I Did
1. Loaded the data from Excel using Pandas and OpenPyXL
2. Cleaned the city names to avoid lookup errors
3. Split the data into 80% training and 20% test sets
4. Trained two RandomForestRegressor models (`n_estimators=50`)
5. Evaluated them with MAE, RMSE and R²
6. Wrote two prediction functions:
   - predict_truck_trip(distance_km, weight_ton): predicts fuel and price
   - predict_trip_from_excel(origin, destination, weight_ton): finds the distance from the Excel file using city names, then predicts

## Results
| Model | MAE | RMSE | R² |
|-------|-----|------|----|
| Fuel (liters) | 90.18 | ~174 | 0.567 |
| Price (Toman) | 1,043,120 | 1,210,393 | 0.994 |

The price model performed very well. The fuel model was weaker, and I think the main reason is the small amount of data.

## Example
```python
result = predict_trip_from_excel("Mashhad", "Dezful", 15)
print(result)
# {'origin': 'Mashhad', 'destination': 'Dezful', 'distance_km': 1451.5,
#  'fuel_liter': 538.4, 'price_toman': 42692400}
