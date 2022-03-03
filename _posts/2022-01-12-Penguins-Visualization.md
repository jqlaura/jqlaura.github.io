---
layout: post
title: Penguins Visualization
---
In this post, we will be doing a simple visualization using the *Penguins* dataset. In particular, we want to investigate the distribution of culmen lengths for every penguin species.

## Data Import

First, we would want to import the dataset from the url:


```python
import pandas as pd
import numpy as np
from matplotlib import pyplot as plt


url = "https://raw.githubusercontent.com/PhilChodrow/PIC16B/master/datasets/palmer_penguins.csv"
penguins = pd.read_csv(url)
```
## Data Preprocessing

For our visualization specifically, in order to take a close look at the culmen length for different penguin species, we will simplify the data as follows:


```python
# specify only the two columns we need for this visualization
cols = ["Species", "Culmen Length (mm)"]

# select a subset of columns
penguins = penguins[cols]

# shorten the species name
penguins["Species"] = penguins["Species"].str.split().str.get(0)
```

## Data Visualization

Now, we want to visualize the distribution of culmen length for different penguin species. We want to draw a histogram for our visualization:


```python
#Create fig and ax
fig, ax = plt.subplots(1)

#Define a function that helps us to plot the histogram 
def plot_hist(df, colname, alpha): 
    ax.hist(df[colname], alpha = alpha, label = df['Species'])

#apply the function for each species
penguins.groupby("Species").apply(plot_hist, 'Culmen Length (mm)', 0.5)

#Set title, labels and display legends
ax.set_title('Culmen Length Distribution of Different Penguin Species')
ax.set_xlabel('Culmen Length')
ax.set_ylabel('Counts')
ax.legend()
```

    
![Penguins_Visualization_5_0.png](/images/Penguins_Visualization_5_0.png)
    


Now we shall see that for the Adelie penguins, the average culmen length is the shortest. There is a lot of overlapping with respect to the culmen lengths of Chinstrap and Gentoo penguins. This is the end of our simple visualization!



