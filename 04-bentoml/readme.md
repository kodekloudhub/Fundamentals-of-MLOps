# House Price Prediction with BentoML

This project demonstrates how to build, train, and deploy a house price prediction model using Python, BentoML, and various machine learning libraries. Follow the steps below to set up the environment, train the model, serve it using BentoML, and make predictions via API requests.

## Table of Contents

- [House Price Prediction with BentoML](#house-price-prediction-with-bentoml)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Setup](#setup)
  - [Training the Model](#training-the-model)
    - [Version 1](#version-1)
  - [Serving the Model](#serving-the-model)
    - [Version 1](#version-1-1)
    - [Version 2](#version-2)
    - [Version 3](#version-3)
  - [Versioning](#versioning)
  - [Cleanup](#cleanup)

## Prerequisites

Ensure you have the following installed on your local machine:

- **Python 3.7+**
- **pip**
- **Git** (optional, for version control)

## Setup

1. **Create a Virtual Environment**

   ```bash
   python3 -m venv bentoml-env
   ```

2. **Activate the Virtual Environment**

   ```bash
   source bentoml-env/bin/activate
   ```

3. **Install Required Packages**

   ```bash
   pip3 install bentoml==1.3.5 scikit-learn pandas
   ```

4. **Navigate to the Project Directory**

   ```bash
   cd 04-bentoml
   ```

## Training the Model

### Version 1

1. **Train the Initial Model**

   ```bash
   python3 model_train_v1.py
   ```

2. **List Available BentoML Models**

   ```bash
   bentoml models list
   ```

## Serving the Model

### Version 1

1. **Serve the Model with BentoML**

   ```bash
   bentoml serve model_service_v1.py --reload
   ```

2. **Make a Prediction Request**

   Open a new terminal window/tab, activate the virtual environment, navigate to the project directory, and run:

   ```bash
   curl -X POST "http://127.0.0.1:3000/predict_house_price" \
        -H "Content-Type: application/json" \
        -d '{"square_footage": 2500, "num_rooms": 5}'
   ```

### Version 2

1. **Train the Enhanced Model**

   ```bash
   python3 model_train_v2.py
   ```

2. **Serve the Enhanced Model**

   ```bash
   bentoml serve model_service_v2.py --reload
   ```

3. **Make a Detailed Prediction Request**

   ```bash
   curl -X POST "http://127.0.0.1:3000/predict_house_price" \
        -H "Content-Type: application/json" \
        -d '{
             "square_footage": 2500,
             "num_rooms": 5,
             "num_bathrooms": 3,
             "house_age": 10,
             "distance_to_city_center": 8,
             "has_garage": 1,
             "has_garden": 1,
             "crime_rate": 0.2,
             "avg_school_rating": 8,
             "country": "Germany"
         }'
   ```

### Version 3

1. **Serve Additional Model Versions**

   ```bash
   bentoml serve model_service_v3.py --reload
   ```

2. **Make Prediction Requests to Specific Model Versions**

   - **Version 1 Endpoint**

     ```bash
     curl -X POST "http://127.0.0.1:3000/predict_house_price_v1" \
          -H "Content-Type: application/json" \
          -d '{"square_footage": 2500, "num_rooms": 5}'
     ```

   - **Version 2 Endpoint**

     ```bash
     curl -X POST "http://127.0.0.1:3000/predict_house_price_v2" \
          -H "Content-Type: application/json" \
          -d '{
               "square_footage": 2500,
               "num_rooms": 5,
               "num_bathrooms": 3,
               "house_age": 10,
               "distance_to_city_center": 8,
               "has_garage": 1,
               "has_garden": 1,
               "crime_rate": 0.2,
               "avg_school_rating": 8,
               "country": "Germany"
           }'
     ```

## Versioning

Each version of the model and its corresponding service script allows for iterative improvements and testing. Ensure that you train and serve the appropriate version based on your requirements.

## Cleanup

To deactivate the virtual environment and clean up your terminal:

1. **Deactivate the Virtual Environment**

   ```bash
   deactivate
   ```

2. **Clear the Terminal (Optional)**

   ```bash
   clear
   ```

---