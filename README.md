# GDP-Forecasting-app-Neural-Networks-Linear-Regression-
Desktop app that predicts future GDP per capita based on previous values for years 1960-2021. It creates and displays charts (GDP/years). It has been developed using neural networks and linear regression.

- [Overview](#overview)
    - Data processing
    - Prediction model
    - App Gui
- [Data analysis](#data-analysis)
- [License](#license)
- [Contact](#contact)



## Overview
The dataset (gdppercapita_us_inflation_adjusted.csv) was found as a CSV file on https://www.kaggle.com/datasets. It contained data on the GDP of 211 countries over the years 1960-2021. However, the dataset had many missing values, so it required preprocessing. Once I had a clean and ready-to-use dataframe, I created a deep learning neural network to predict future GDP per capita values.

### Data processing
To process the data, I usedthe Linear Regression model from the scikit-learn library. For each country in the dataframe, I created a separate Linear Regression model, trained using the available data from years without missing values. With this model, I could predict the missing GDP values for each year.

However, the models occasionally produced negative predictions. Since GDP cannot be negative, I implemented a correction step, setting any negative predicted values to 0. After this step the data was ready-to-use!

### Prediction model
The Neural Network model consists of three hidden layers with 32, 64, and 64 units, respectively, using the ReLU activation function. The output layer has a single unit with a linear activation function, as this is a regression problem. The model is then compiled with the mean squared error as the loss function and the Adam optimizer. Next, it is trained on the training data using a batch size of 32 for 120 epochs. To optimize the model, I normalized it by dividing every element of the data by the largest value in the data frame.

The NN model is created by predicting the GDP per capita value for the year 2021 and then evaluating it with the real value. The values of the loss and validation loss are equal to 1.8553e-05 and 1.8836e-05, respectively. These results are highly promising, indicating that the model has achieved very low error rates during training and validation. Below, you can find the final values of the loss and validation loss obtained during the model's compilation.

<p align="center">
  <img src="Loss.png" alt="Loss" width="400" height="250">
</p>

After the model is fully trained, it is used to predict the GDPs of every country in the future years. In my app, it predicts GDPs until the year 2040, but this can be easily changed. The model then creates and saves charts (GDP/years) for each country's predictions.

### App Gui
The app's GUI prompts the user to input the name of a country in uppercase.

<p align="center">
  <img src="GUI/GUI_1.png" alt="GUI Screenshot" width="600" height="350">
</p>

Once the country name is entered, the app displays a GDP (year) chart for that country if it is found in the dataset. The area highlighted in red indicates that the values for those years are not actual data points but predictions made by the model.

<p align="center">
  <img src="GUI/GUI_2.png" alt="GUI Screenshot" width="600" height="350">
</p>

In this way, the app allows users to interactively explore the GDP trends of different countries and compare the actual historical data with the model's predictions. This visual representation provides valuable insights into how well the model performs in forecasting GDP per capita for various countries over time.

## Data Analysis
Despite the low values of the loss and validation loss in the model, it cannot be considered a reliable indicator of GDP values for an extended period of time. The model efficiently predicts values for the year 2021 in the training phase because it had the opportunity to learn and adjust its parameters based on the available data. However, GDP depends on numerous unpredictable factors that this model does not take into account. Nevertheless, the GDP values for a few years ahead may be relatively close to those predicted by the model, as long as there are no significant economic changes in those years.

Model assumes a positive scenario for most cases, in which GDP per capita steadily increases. 

<p align="center">
  <img src="plots/India_gdp_plot.png" alt="India_gdp_plot" width="500" height="350">
</p>

<p align="center">
  <img src="plots/Poland_gdp_plot.png" alt="Poland_gdp_plot" width="500" height="350">
</p>

However, there are some cases for which it predicts a different trend. For example, in the case of Burundi, the model assumes a negative growth rate for the GDP per capita. The most interesting cases are China, where despite significant GDP per capita growth, the model predicts a downturn, and Syria, where the model foresees a sudden increase until 2032, followed by a sharp decline. More plots can be seen [here](plots).

<p align="center">
  <img src="plots/China_gdp_plot.png" alt="China_gdp_plot" width="500" height="350">
</p>

<p align="center">
  <img src="plots/Syria_gdp_plot.png" alt="Syria_gdp_plot" width="500" height="350">
</p>

## License
This project is licensed under the MIT License - [License](LICENSE.txt).

## Contact
Email: mikolajczachorowski260203@gmail.com