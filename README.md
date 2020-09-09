# RentinBo

## 1. Introduction

In case .ipynb files are not rendered correctly just copy-paste their  raw link to:
https://nbviewer.jupyter.org/.

The RentinBo project I here present is intended to be a demostration of the workflow behind the application of a Machine Learnign algorithm.
The scope of this project is to train a classification algorithm, with real data from current housing situation in Bologna, to predict the possible range of euros that can be asked to rent a single or double room in Bologna.
In order to work with a true dataset I have personally collected ads for rooms during August 2020, surfing the website "Subito.it".
The only criterium to select ads has been to collect the same amount of informatios for single and double rooms, namely 100 and 100.
I selected few main features on the base of which lately I have trained the algorithm.

- Type
  - As mentioned before only single and double rooms have been considered.

- Gender
  - In many cases ads were explicitly oriented for one gender or the other, as well as both together.

- Position
  - Reporting the exact location of a room would have been inefficient without a precise system of coordinates and a metric, hence I opted for dividing the city according to the zones defined below (see references for the list).
  
  ![Zone di Bologna](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Mappa_zone.png)
  
- Bathroom/kitchen/living room/terrace
  - The number of spaces in the house influences the rent prices too.
  
Whit these considerations I have created the dataset and started working on it.

## 2. Structure

The project is subdivided in 3 main scripts edited in Jupyter Notebook.

### 1_Data_preparation.ipynb

In the first part I have inspected the dataset and this is how it presents, with all its features target values.

![Dataset](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Dataframe.png)

The very first idea was to use a regression model to predict the rent values but, since prices can depend on other factors that are not easy to categorise, I opted for working with classes instead of exact values.
The next step has been considering the datatypes contained in the dataframe, infact there were labels anche integral values.

![dtype](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Types.png)

After other few statistical considerations I took a step further towards the training algorithm.

### 2_RentinBo.ipynb

From the moment that the dataframe was made by labels and values I had to find a way to uniform the dataset to one type. 
I used then a dummy encoder for type, gender and position, which indeed expanded the dataframe a lot, and a label encoder for the rent classes of prices since they were ordered. If I had used the label encoder with non-numerical features I might have introduced some bias in case the algorithm had used a metric to evaluate distances among features; this is why I have taken as a good compromise the one hot encoding even though it introduced more data.

```python3 
le = preprocessing.LabelEncoder()
le.fit_transform(['175-200', '200-225', '225-250', '250-275', '275-300', '300-325', '325-350', '350-375',
                  '375-400', '400-425', '425-450', '450-475', '475-500', '500-525', '525-550', '550-575', 
                 '575-600', '600-625', '625-650', '650-675', '675-700'])
 ```

Meanwhile I have looked for possible internal correlations, and indeed there weren't any relevant ones.

![Correlation_a](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Correlation_matrix_a.png) ![Correlation_b](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Correlation_matrix_b.png)

Having said that I have trained a Random Forest Classifier capable to handle large datasets and, in principle, to gain high accuracies wthout much tuning thanks also to bootstrapping. 
## 3. References






