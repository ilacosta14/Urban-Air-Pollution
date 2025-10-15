# Urban Air Pollution Challenge
__Can you predict air quality in cities around the world using satellite data?__

For this challenge we’ll be digging deeper into Air quality data in several African cities, finding ways to track air quality and how it is changing, even in places without ground-based sensors. The collected weather data and daily observations are from the _Sentinel 5P satellite_ tracking various pollutants in the atmosphere. 

Our goal is to use the information from such data to predict _PM2.5_ particulate matter concentration (a common measure of air quality that normally requires ground-based sensors to measure) every day for each city. The data covers the last three months, spanning hundreds of cities across the globe.

_This is a Zindi data challenge, for more details check: [Urban Air Pollution challenge](https://zindi.africa/competitions/zindiweekendz-learning-urban-air-pollution-challenge)_


The objective of this challenge is to predict __PM2.5__ particulate matter concentration in the air __every day__ for __each city__. 
- PM2.5 refers to atmospheric particulate matter that have a diameter of __less than 2.5 micrometers__ 
- Is one of the most harmful air pollutants. 
- PM2.5 is a common measure of air quality that normally requires ground-based sensors to measure.

The data comes from three main sources:

1. __Ground-based air quality sensors__. These measure the __target__ variable (PM2.5 particle concentration). In addition to the `target` column (which is the daily mean concentration) there are also columns for `minimum` and `maximum` readings on that day, the `variance` of the readings and the total number (`count`) of sensor readings used to compute the target value. _This data is only provided for the train set_ - you must predict the target variable for the test set.

2. __The Global Forecast System (GFS)__ for _weather data_. `Humidity`, `temperature` and `wind speed`, which can be used as inputs for your model.

3. __The Sentinel 5P satellite__. This satellite monitors various _pollutants_ in the atmosphere. For each pollutant, we queried the `offline Level 3` (L3) datasets available in Google Earth Engine (you can read more about the individual products here: https://developers.google.com/earth-engine/datasets/catalog/sentinel-5p). For a given pollutant, for example NO2, we provide all data from the Sentinel 5P dataset for that pollutant. This includes the key measurements like `NO2_column_number_density` (a measure of NO2 concentration) as well as metadata like the `satellite altitude`. We recommend that you __focus on the key measurements__, either the `column_number_density` or the `tropospheric_X_column_number_density` (which measures density closer to Earth’s surface).
Unfortunately, this data is not 100% complete. Some locations have no sensor readings for a particular day, and so those rows have been excluded. There are also gaps in the input data, particularly the satellite data for CH4.

This data is not 100% complete. Some locations have no sensor readings for a particular day, and so those rows have been excluded. There are also gaps in the input data, particularly the satellite data for CH4.

## Set up your Environment



### **`macOS`** type the following commands : 

- For installing the virtual environment you can either use the [Makefile](Makefile) and run `make setup` or install it manually with the following commands:

     ```BASH
    make setup
    ```
    After that active your environment by following commands:
    ```BASH
    source .venv/bin/activate
    ```
Or ....
- Install the virtual environment and the required packages by following commands:

    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/bin/activate
    pip install --upgrade pip
    pip install -r requirements.txt
    ```
    
### **`WindowsOS`** type the following commands :

- Install the virtual environment and the required packages by following commands.

   For `PowerShell` CLI :

    ```PowerShell
    pyenv local 3.11.3
    python -m venv .venv
    .venv\Scripts\Activate.ps1
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

    For `Git-bash` CLI :
  
    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/Scripts/activate
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

    **`Note:`**
    If you encounter an error when trying to run `pip install --upgrade pip`, try using the following command:
    ```Bash
    python.exe -m pip install --upgrade pip
    ```


   
## Usage

In order to train the model and store test data in the data folder and the model in models run:

**`Note`**: Make sure your environment is activated.

```bash
python example_files/train.py  
```

In order to test that predict works on a test set you created run:

```bash
python example_files/predict.py models/linear_regression_model.sav data/X_test.csv data/y_test.csv
```

## Limitations

Development libraries are part of the production environment, normally these would be separate as the production code should be as slim as possible.


