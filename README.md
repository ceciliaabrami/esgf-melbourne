# TP 4 de ABRAMI Cecilia, CHERIF Leila and SITBON Yael


## Objective

We had to build a model able to predict the **daily** temperature in Melbourne over the **next year**.

##Difficulties
We had to rewrite parts of the esgflib as the split_train_test_data when given 1987 would return the first 1987 data points and not the data points up to the year 1987. It was also not possible to extract test data given a year, so we wrote create_test_data that returns as X the last ***history_days** data points of the last year and as Y the first **horizon_days** data points of the year.
There is also a missing data point on the 31st Dec 1988 that forced us to adapt.


##Model
After trying some basic models based on convolutions and bidirectional GRU, we decided to use the LSTNet model that is particularly well fitted to the problem as we encounter seasonality in the data. 
We also tried to work with a transformer model found on GitHub but could not obtain better results.
We decided to build 9 different models for the 9 predictions as it allows us to obtain better results with models built explicitly for the task.

## Evaluation

We evaluated and trained the models using the Mean Squared Error because our model should be an accurate prediction but we can never predict the small daily variation, only the underlying trends and using the mse will punish harshly the model for large errors but not too much for unpredictable daily variations. 

### Results

<table>
    <thead>
        <tr>
            <th>Evaluation year</th>
            <th>Next 3 months</th>
            <th>Next 6 months</th>
            <th>Next 12 months</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1987</td>
            <td>5.7</td>
            <td>6.7</td>
            <td>9.9</td>
        </tr>
        <tr>
            <td>1988</td>
            <td>9.4</td>
            <td>10.6</td>
            <td>13.3</td>
        </tr>
        <tr>
            <td>1989</td>
            <td>13.9</td>
            <td><13.3/td>
            <td>15.4</td>
        </tr>
    </tbody>
</table>
