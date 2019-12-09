# Product Recommender 
### Background
According to Statista, over 4.33 billion people access the internet globally. Many service providers and retailers have moved online and the popularity of ecommerce platforms continue to rise . Unlike physical stores, online retailers are not restricted to limited shelf space. Retailers are able to sell a wide variety of products online because the costs of logistics is lower. However, the huge amount of goods available makes it difficult for customers to navigate through their product of interest. To influence the user’s buying decision and increase the company’s revenue, we will create a product recommender system to provide a suggested list of items based on users history.

### Overview of Data
For this project, we will be using the [Online Retail](http://archive.ics.uci.edu/ml/datasets/Online+Retail) dataset from the UCI Machine Learning repository. It contains transactional information of an online retail company based in the UK during a year period. The company sells unique all-occasion gifts.

## Exploratory Data Analysis 
In this section, we will examine customer purchase history, unit price, countries of customers, and product trends. 

Some questions to consider:<br>
•	How many orders were made by customers? <br>
•	Who are the top customers with the most numbers of orders?<br>
•	How many orders per month?<br>
•	How many orders per day?<br>
•	How many orders per hour?<br>
•	How many orders for each country?<br>
•	Which products are best sellers?<br>
•	Which product did customers spend the most on?<br>


## Preprocessing 
- [x]  Form User-Item Matrix
- [x]  Create Train and Test set 

## Model
We will be using the __Alternating Least Squares__ model as discussed in [Collaborative Filtering for Implicit Feedback Datasets](http://yifanhu.net/PUB/cf.pdf) by Hu, Koren, and Volinsky.

## Evaluation 
Classification accuracy metrics, like __ROC AUC__, to assess the recommendation algorithm ability to classify relevant and irrelevant items.

## Hypermeters Tuning 
Cross-validation grid search will be used to find the optimal values for the following parameters:
•	num_factors: The number of latent factors, or degree of dimensionality in our model.
•	regularization: Scale of regularization for both user and item factors.
•	alpha: Our confidence scaling term.
•	iterations: Number of iterations to run Alternating Least Squares optimization

__Optimal Parameters__<br>

| Hyperparameters  | Values   |
| :------------- | :----------|
| num_factors             |   32   |
| :------------- | :----------|
| regularization |  0.1    |
| :------------- | :----------|
alpha |  15    |
| :------------- | :----------|
| iterations: |   50   |


__ROC AUC Score__ <br>

| Test score  | Baseline score  |
| :------------- | :----------|
| 0.871             |   0.813  |

__Observation__: We have a decent model that is able to recommend relevant items better than random guessing. Based on the baseline score, our model also does better than just recommending popular items. 


### Recommendation Example  

![](images/example.png?raw=true)<br>

__Observation__: Customer 12346 purchased a felt farm animal product. The system recommended other felt and farm animals products. The first 3 items seem more relevant than the lower half of the list.

### Conclusion
In this project, we have created a recommender system that takes in implicit feedback and produces a list of items similar to what the customer has purchased. We take an alternating least square approach that performs matrix factorization and minimize the cost function by solving one feature vector at a time. This enables it to run in parallel and makes it less computational expensive than singular value decomposition. Then, we were able to evaluate our recommender system by how well it was able to classify relevant items that were purchased with an ROC AUC score. 
 
Although we were able to design a decent recommender, there are a couple of shortcomings that we were unable to address. Deploying an implicit model and fitting a single user-item matrix in one machine would be too memory intensive. A more practical method would be to implement it through Spark. In addition, our model is not equipped to resolve the cold start problem since we do not have previous user history. A hybrid approach would be able to incorporate feature properties and produce recommend similar items without user data. 
 
In future work, we could strive to improve customer experience on the website by performing customer segmentation. By doing so, we would be able to uncover insightful behavior patterns that can allow us to create a set of personalized systems for each tier of customers. For example, if the customer runs an art and crafts shop, he might be interested in viewing newly released art supplies. This way, the system is able to learn about user preference and allow exposure of new products.
