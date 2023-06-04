# NETFLIX-MOVIE-RECOMMENDATION
To filter and predict only those movies that a corresponding user is most likely to want to watch. The ML algorithms for these recommendation systems use the data about this user from the system’s database.
# NETFLIX-MOVIE-RECOMMENDATION
To filter and predict only those movies that a corresponding user is most likely to want to watch. The ML algorithms for these recommendation systems use the data about this user from the system’s database.
#ECLAT
#IMPORTING LIBRARIES
pip install apyori
#IMPORTING DATASET
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
dataset = pd.read_csv('Netflix Recommendation.csv', header = None)
transactions = []
for i in range(0, 7466):
   transactions.append([str(dataset.values[i, j])for j in range(0, 20)])
   #ECLAT TRAINING ON DATASET
   from apyori import apriori
rules = apriori(transactions = transactions, min_support = 0.003, min_confidence = 0.2, min_lift = 3, min_length =5)
#VISUALIZING
#RAW RESULTS
results = list(rules)
results
#PROPER DISPLAY
def inspect(results):
  movie1 = [tuple(result[2][0][0])[0]for result in results]
  movie2 = [tuple(result[2][0][1])[0]for result in results]
  supports = [result[1]for result in results]
  return list(zip(movie1, movie2, supports))
resultsinDataFrame = pd.DataFrame(inspect(results), columns = ['movie1', 'movie2', 'support'])
resultsinDataFrame
resultsinDataFrame.nlargest(n = 10, columns = 'support')
