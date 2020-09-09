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

## 1_Data_preparation

In the first part I have inspected the dataset and this is how it presents, with all its features target values.

![Dataset](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Dataframe.png)

The very first idea was to use a regression model to predict the rent values but, since prices can depend on other factors that are not easy to categorise, I opted for working with classes instead of exact values.
The next step has been considering the datatypes contained in the dataframe, infact there were labels anche integral values.

![dtype](https://github.com/MarcoCollesei/RentinBo/blob/master/Mixed/Types.png)

## 3. References






