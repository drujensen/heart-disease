# Predicting Heart Disease using SHAInet 

This workbook predicts the probability of heart disease.  We are using [SHAInet](https://github.com/NeuraLegion/shainet) modeling tool in Crystal.

This is for research purposes only and should not be used to diagnose or predict any actual persons health.

## Data

We will be using the [Heart Disease Dataset](https://www.kaggle.com/imnikhilanand/heart-attack-prediction) provided on kaggle.com by Nikhil Anand.

Heart Disease Data Set: 
Features: 
1. #3 (age) 
2. #4 (sex) (0 = female, 1 = male) 
3. #9 (cp) cp: chest pain type -- 1: typical angina -- 2: atypical angina -- 3: non-anginal pain -- 4: asymptomatic 
4. #10 (trestbps) trestbps: resting blood pressure (in mm Hg on admission to the hospital) 
5. #12 (chol) chol: serum cholesterol in mg/dl
6. #16 (fbs) fbs: (fasting blood sugar > 120 mg/dl) (1 = true; 0 = false)
7. #19 (restecg) restecg: resting electrocardiographic results
    -- Value 0: normal 
    -- Value 1: having ST-T wave abnormality (T wave inversions and/or ST elevation or depression of > 0.05 mV) 
    -- Value 2: showing probable or definite left ventricular hypertrophy by Estes' criteria
8. #32 (thalach) halach: maximum heart rate achieved
9. #38 (exang) exercise induced angina (1 = yes; 0 = no)
10. #40 (oldpeak) oldpeak = ST depression induced by exercise relative to rest
11. #41 (slope) slope: the slope of the peak exercise ST segment -- Value 1: upsloping -- Value 2: flat -- Value 3: downsloping
12. #44 (ca) ca: number of major vessels (0-3) colored by flourosopy
13. #51 (thal) thaldur: duration of exercise test in minutes
14. #58 (num) (the predicted attribute) num: diagnosis of heart disease (angiographic disease status) -- Value 0: < 50% diameter narrowing -- Value 1: > 50% diameter narrowing (in any major vessel: attributes 59 through 68 are vessels)

Creators:

 1. Hungarian Institute of Cardiology. Budapest: Andras Janosi, M.D.
 2. University Hospital, Zurich, Switzerland: William Steinbrunn, M.D.
 3. University Hospital, Basel, Switzerland: Matthias Pfisterer, M.D.
 4. V.A. Medical Center, Long Beach and Cleveland Clinic Foundation: Robert Detrano, M.D., Ph.D.

## Installation

This requires crystal 0.24.2 to be installed

## Usage

This project uses crystal's playground.  You can load and run the playground workbook using:
```bash
shards install
crystal play
open http://localhost:8080
```
Then select the Workbook -> Heart Disease from the menu.

You can also compile and run the application:
```bash
crystal run src/heart_disease.cr
```

## Contributing

1. Fork it ( https://github.com/drujensen/heart-disease/fork )
2. Create your feature branch (git checkout -b my-new-feature)
3. Commit your changes (git commit -am 'Add some feature')
4. Push to the branch (git push origin my-new-feature)
5. Create a new Pull Request

## Contributors

- [drujensen](https://github.com/drujensen) Dru Jensen - creator, maintainer

