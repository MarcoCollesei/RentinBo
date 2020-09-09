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
 array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
       17, 18, 19, 20])

Meanwhile I have looked for possible internal correlations, and indeed there weren't any relevant ones.

![Correlation_a](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Correlation_matrix_a.png) ![Correlation_b](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Correlation_matrix_b.png)

Having said that I have trained a Random Forest Classifier capable to handle large datasets and, in principle, to gain high accuracies wthout much tuning thanks also to bootstrapping.
After splitting the data into train and test sets I've launched the algorithm and ended up with a very low accuracy.

```python3
clf_accuracy = clf.score(X_test, Y_test)
print("Accuracy: %.3f%%" % (clf_accuracy*100.0))
```
Accuracy: 42.308%

To have a more clear idea of what had not performed as expected I have plotted the confusion matrix, which explained better than words that many targets were misclassified.

![Confusion](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Confusion_matrix.png)

I have decided to search for optimal hyperparameters with RandomizedSearchCV and GridSearchCV but none was able to make the Random Forest model perform better.
I have chosen then to compare as many as possible classification algorithms, without touching their default parameters too much, to see if there was a prommising one. It turned out Naive Bayes classifiers were more suited for my dataframe.

![Accuracies](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Accuracies.png)

Still I was not satisfied and I decided to use a scaler on data.

```python3
from sklearn.preprocessing import StandardScaler, scale
```
Results were still mediocre so I managed to work out a different solution, collecting new data.

### 3_Playground.ipynb

Instead of spending time browsing for new data to add to the old ones I have created an interactive function with widgets.
**(I strongly suggest to appreciate the interactivity to copy locally the repository and open it in Jupyter Notebook)**

With this function one can:
* Select the features that might be obtained from real ads on renting sites
* Ask the algorithm which rent price would be appropriate, based on the old dataset
* Decide wether the prediction correspons to the real price found in the real ad
* If the prediction is wrong choose the right prices for that specific room
* Store the new features and the new target into arrays that later can be add to the old dataset: in order to train the algorithm on more true data

The following is just an example of what can be achieved with interactive features (note that the rent price is given back in real time, varying with selected features).

![Playground](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Playground_c.png)

## 3. References






