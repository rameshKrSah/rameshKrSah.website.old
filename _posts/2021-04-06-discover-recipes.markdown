---
title: "Discover new recipes using Python 🍝."
date: 2021-04-07
comments: True
mathjax: True
tags: [python]
categories:
  - python
---

In this post, we are going to discover food recipes using Python. This is going to be a fun post and maybe a useful one 😁. So let's begin.

To do anything, we first need the data. Download the data from [here](https://www.kaggle.com/kanishk307/6000-indian-food-recipes-dataset) . Also, the Jupyter notebook for this project can be found [here](https://github.com/rameshKrSah/kaggle-journey/blob/main/JNBs/6000%20Indian%20Food%20.ipynb).

```python
import numpy as np
import pandas as pd
import os
```

```python
from zipfile import ZipFile
```

```python
os.listdir("../datasets/6000-Indian-Food-Dataset/")
```

    ['IndianFoodDatasetCSV.csv']

After downloading the data from Kaggle, we need to extract the zip file. Modify the path to the dataset for your case before running the next code block.

```python
# specifying the zip file name
file_name = "../datasets/6000-Indian-Food-Dataset/archive.zip"
  
# opening the zip file in READ mode
with ZipFile(file_name, 'r') as zip:
    # printing all the contents of the zip file
    zip.printdir()
  
    # extracting all the files
    print('Extracting all the files now...')
    zip.extractall("../datasets/6000-Indian-Food-Dataset/")
    print('Done!')
```

    File Name                                             Modified             Size
    IndianFoodDatasetCSV.csv                       2020-10-24 01:08:28     24151935
    IndianFoodDatasetXLS.xlsx                      2020-10-24 01:08:28      5535790
    Extracting all the files now...
    Done!
    
Now, you must have two files in your data folder. We will open the CSV file using pandas. 

```python
df = pd.read_csv("../datasets/6000-Indian-Food-Dataset/IndianFoodDatasetCSV.csv")
```

The data frame ```df``` contains all the rows and column of the CSV file in a proper format. Let's take a look at few rows.

```python
df.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Srno</th>
      <th>RecipeName</th>
      <th>TranslatedRecipeName</th>
      <th>Ingredients</th>
      <th>TranslatedIngredients</th>
      <th>PrepTimeInMins</th>
      <th>CookTimeInMins</th>
      <th>TotalTimeInMins</th>
      <th>Servings</th>
      <th>Cuisine</th>
      <th>Course</th>
      <th>Diet</th>
      <th>Instructions</th>
      <th>TranslatedInstructions</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Masala Karela Recipe</td>
      <td>Masala Karela Recipe</td>
      <td>6 Karela (Bitter Gourd/ Pavakkai) - deseeded,S...</td>
      <td>6 Karela (Bitter Gourd/ Pavakkai) - deseeded,S...</td>
      <td>15</td>
      <td>30</td>
      <td>45</td>
      <td>6</td>
      <td>Indian</td>
      <td>Side Dish</td>
      <td>Diabetic Friendly</td>
      <td>To begin making the Masala Karela Recipe,de-se...</td>
      <td>To begin making the Masala Karela Recipe,de-se...</td>
      <td>https://www.archanaskitchen.com/masala-karela-...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>टमाटर पुलियोगरे रेसिपी - Spicy Tomato Rice (Re...</td>
      <td>Spicy Tomato Rice (Recipe)</td>
      <td>2-1/2 कप चावल - पका ले,3 टमाटर,3 छोटा चमच्च बी...</td>
      <td>2-1 / 2 cups rice - cooked, 3 tomatoes, 3 teas...</td>
      <td>5</td>
      <td>10</td>
      <td>15</td>
      <td>3</td>
      <td>South Indian Recipes</td>
      <td>Main Course</td>
      <td>Vegetarian</td>
      <td>टमाटर पुलियोगरे बनाने के लिए सबसे पहले टमाटर क...</td>
      <td>To make tomato puliogere, first cut the tomato...</td>
      <td>http://www.archanaskitchen.com/spicy-tomato-ri...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Ragi Semiya Upma Recipe - Ragi Millet Vermicel...</td>
      <td>Ragi Semiya Upma Recipe - Ragi Millet Vermicel...</td>
      <td>1-1/2 cups Rice Vermicelli Noodles (Thin),1 On...</td>
      <td>1-1/2 cups Rice Vermicelli Noodles (Thin),1 On...</td>
      <td>20</td>
      <td>30</td>
      <td>50</td>
      <td>4</td>
      <td>South Indian Recipes</td>
      <td>South Indian Breakfast</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Ragi Vermicelli Recipe, fi...</td>
      <td>To begin making the Ragi Vermicelli Recipe, fi...</td>
      <td>http://www.archanaskitchen.com/ragi-vermicelli...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Gongura Chicken Curry Recipe - Andhra Style Go...</td>
      <td>Gongura Chicken Curry Recipe - Andhra Style Go...</td>
      <td>500 grams Chicken,2 Onion - chopped,1 Tomato -...</td>
      <td>500 grams Chicken,2 Onion - chopped,1 Tomato -...</td>
      <td>15</td>
      <td>30</td>
      <td>45</td>
      <td>4</td>
      <td>Andhra</td>
      <td>Lunch</td>
      <td>Non Vegeterian</td>
      <td>To begin making Gongura Chicken Curry Recipe f...</td>
      <td>To begin making Gongura Chicken Curry Recipe f...</td>
      <td>http://www.archanaskitchen.com/gongura-chicken...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>आंध्रा स्टाइल आलम पचड़ी रेसिपी - Adrak Chutney ...</td>
      <td>Andhra Style Alam Pachadi Recipe - Adrak Chutn...</td>
      <td>1 बड़ा चमच्च चना दाल,1 बड़ा चमच्च सफ़ेद उरद दाल,2...</td>
      <td>1 tablespoon chana dal, 1 tablespoon white ura...</td>
      <td>10</td>
      <td>20</td>
      <td>30</td>
      <td>4</td>
      <td>Andhra</td>
      <td>South Indian Breakfast</td>
      <td>Vegetarian</td>
      <td>आंध्रा स्टाइल आलम पचड़ी बनाने के लिए सबसे पहले ...</td>
      <td>To make Andhra Style Alam Pachadi, first heat ...</td>
      <td>https://www.archanaskitchen.com/andhra-style-a...</td>
    </tr>
  </tbody>
</table>
</div>

The ```Srno``` column is an unnecessary one and we will drop it. To drop a column from a pandas DataFrame use the ```drop()``` method and specify the columns you want dropped.

```python
# drop the serial no column
df = df.drop(columns=['Srno'])
```

```python
df.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>RecipeName</th>
      <th>TranslatedRecipeName</th>
      <th>Ingredients</th>
      <th>TranslatedIngredients</th>
      <th>PrepTimeInMins</th>
      <th>CookTimeInMins</th>
      <th>TotalTimeInMins</th>
      <th>Servings</th>
      <th>Cuisine</th>
      <th>Course</th>
      <th>Diet</th>
      <th>Instructions</th>
      <th>TranslatedInstructions</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Masala Karela Recipe</td>
      <td>Masala Karela Recipe</td>
      <td>6 Karela (Bitter Gourd/ Pavakkai) - deseeded,S...</td>
      <td>6 Karela (Bitter Gourd/ Pavakkai) - deseeded,S...</td>
      <td>15</td>
      <td>30</td>
      <td>45</td>
      <td>6</td>
      <td>Indian</td>
      <td>Side Dish</td>
      <td>Diabetic Friendly</td>
      <td>To begin making the Masala Karela Recipe,de-se...</td>
      <td>To begin making the Masala Karela Recipe,de-se...</td>
      <td>https://www.archanaskitchen.com/masala-karela-...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>टमाटर पुलियोगरे रेसिपी - Spicy Tomato Rice (Re...</td>
      <td>Spicy Tomato Rice (Recipe)</td>
      <td>2-1/2 कप चावल - पका ले,3 टमाटर,3 छोटा चमच्च बी...</td>
      <td>2-1 / 2 cups rice - cooked, 3 tomatoes, 3 teas...</td>
      <td>5</td>
      <td>10</td>
      <td>15</td>
      <td>3</td>
      <td>South Indian Recipes</td>
      <td>Main Course</td>
      <td>Vegetarian</td>
      <td>टमाटर पुलियोगरे बनाने के लिए सबसे पहले टमाटर क...</td>
      <td>To make tomato puliogere, first cut the tomato...</td>
      <td>http://www.archanaskitchen.com/spicy-tomato-ri...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ragi Semiya Upma Recipe - Ragi Millet Vermicel...</td>
      <td>Ragi Semiya Upma Recipe - Ragi Millet Vermicel...</td>
      <td>1-1/2 cups Rice Vermicelli Noodles (Thin),1 On...</td>
      <td>1-1/2 cups Rice Vermicelli Noodles (Thin),1 On...</td>
      <td>20</td>
      <td>30</td>
      <td>50</td>
      <td>4</td>
      <td>South Indian Recipes</td>
      <td>South Indian Breakfast</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Ragi Vermicelli Recipe, fi...</td>
      <td>To begin making the Ragi Vermicelli Recipe, fi...</td>
      <td>http://www.archanaskitchen.com/ragi-vermicelli...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Gongura Chicken Curry Recipe - Andhra Style Go...</td>
      <td>Gongura Chicken Curry Recipe - Andhra Style Go...</td>
      <td>500 grams Chicken,2 Onion - chopped,1 Tomato -...</td>
      <td>500 grams Chicken,2 Onion - chopped,1 Tomato -...</td>
      <td>15</td>
      <td>30</td>
      <td>45</td>
      <td>4</td>
      <td>Andhra</td>
      <td>Lunch</td>
      <td>Non Vegeterian</td>
      <td>To begin making Gongura Chicken Curry Recipe f...</td>
      <td>To begin making Gongura Chicken Curry Recipe f...</td>
      <td>http://www.archanaskitchen.com/gongura-chicken...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>आंध्रा स्टाइल आलम पचड़ी रेसिपी - Adrak Chutney ...</td>
      <td>Andhra Style Alam Pachadi Recipe - Adrak Chutn...</td>
      <td>1 बड़ा चमच्च चना दाल,1 बड़ा चमच्च सफ़ेद उरद दाल,2...</td>
      <td>1 tablespoon chana dal, 1 tablespoon white ura...</td>
      <td>10</td>
      <td>20</td>
      <td>30</td>
      <td>4</td>
      <td>Andhra</td>
      <td>South Indian Breakfast</td>
      <td>Vegetarian</td>
      <td>आंध्रा स्टाइल आलम पचड़ी बनाने के लिए सबसे पहले ...</td>
      <td>To make Andhra Style Alam Pachadi, first heat ...</td>
      <td>https://www.archanaskitchen.com/andhra-style-a...</td>
    </tr>
  </tbody>
</table>
</div>

Let's print out the dimensions of the data frame. 

```python
df.shape
```

    (6871, 14)

We have a total of ```6871``` recipes and there are ```14``` properties for each recipe. As you can see, the recipes are categories by diets, course, cuisine and many more. Let's get the statistics for some categories.

```python
df.Diet.value_counts()
```

    Vegetarian                      4712
    High Protein Vegetarian          705
    Non Vegeterian                   427
    Eggetarian                       344
    Diabetic Friendly                260
    High Protein Non Vegetarian      225
    No Onion No Garlic (Sattvic)      73
    Vegan                             61
    Gluten Free                       50
    Sugar Free Diet                   14
    Name: Diet, dtype: int64

```python
df.Course.value_counts()
```

    Lunch                           1765
    Side Dish                        992
    Snack                            876
    Dinner                           782
    Dessert                          659
    Appetizer                        639
    Main Course                      315
    World Breakfast                  260
    South Indian Breakfast           260
    North Indian Breakfast           123
    Indian Breakfast                 101
    Vegetarian                        47
    One Pot Dish                      33
    High Protein Vegetarian            7
    Brunch                             4
    Vegan                              3
    Non Vegeterian                     2
    No Onion No Garlic (Sattvic)       1
    Eggetarian                         1
    Sugar Free Diet                    1
    Name: Course, dtype: int64

```python
df.Cuisine.value_counts()
```

    Indian                  1157
    Continental             1021
    North Indian Recipes     938
    South Indian Recipes     682
    Italian Recipes          236
                            ... 
    Jewish                     1
    Dessert                    1
    Lunch                      1
    Brunch                     1
    Dinner                     1
    Name: Cuisine, Length: 82, dtype: int64

I am really interested in the high protein vegetarian diet categories. Let's filter out vegetarian high protein dishes with maximum preparation and cooking time of 30 minutes from Indian cuisine. We can do this by combining multiple columns condtions for the data frame. 

First filter out the recipes based on diet like this.

```python
high_protein_veg_recp = df[df['Diet'] == 'High Protein Vegetarian']
```

Next, we can filter out the recipes based on Cuisine.

```python
high_protein_veg_recp = high_protein_veg_recp[high_protein_veg_recp['Cuisine'] == 'Indian']
```

And, finally last filter for TotalTimeInMins

```python
high_protein_veg_recp = high_protein_veg_recp[high_protein_veg_recp['TotalTimeInMins'] < 31]
```

Now the data frame ```high_protein_veg_recp``` contains all the recipes that are vegetarian, high in protein, Indian cuisine, and total preparation time less than or equal to 30 minutes. Let's see some of them.

```python
high_protein_veg_recp.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>RecipeName</th>
      <th>TranslatedRecipeName</th>
      <th>Ingredients</th>
      <th>TranslatedIngredients</th>
      <th>PrepTimeInMins</th>
      <th>CookTimeInMins</th>
      <th>TotalTimeInMins</th>
      <th>Servings</th>
      <th>Cuisine</th>
      <th>Course</th>
      <th>Diet</th>
      <th>Instructions</th>
      <th>TranslatedInstructions</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1775</th>
      <td>Soya Chunks Pepper Curry Recipe</td>
      <td>Soya Chunks Pepper Curry Recipe</td>
      <td>2 cups Soy Chunks (Nuggets),1 Green Bell Peppe...</td>
      <td>2 cups Soy Chunks (Nuggets),1 Green Bell Peppe...</td>
      <td>10</td>
      <td>20</td>
      <td>30</td>
      <td>3</td>
      <td>Indian</td>
      <td>Lunch</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Soya Chunks Pepper Curry r...</td>
      <td>To begin making the Soya Chunks Pepper Curry r...</td>
      <td>https://www.archanaskitchen.com/soya-chunks-pe...</td>
    </tr>
    <tr>
      <th>1976</th>
      <td>High-Protein Peanut Chutney Recipe-Indian Styl...</td>
      <td>High-Protein Peanut Chutney Recipe-Indian Styl...</td>
      <td>1/2 teaspoon Ghee,3/4 cup Roasted Peanuts (Moo...</td>
      <td>1/2 teaspoon Ghee,3/4 cup Roasted Peanuts (Moo...</td>
      <td>15</td>
      <td>15</td>
      <td>30</td>
      <td>5</td>
      <td>Indian</td>
      <td>Side Dish</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Peanut Chutney Recipe, fir...</td>
      <td>To begin making the Peanut Chutney Recipe, fir...</td>
      <td>http://www.archanaskitchen.com/peanut-chutney-...</td>
    </tr>
    <tr>
      <th>2146</th>
      <td>Rajma and Corn Salad Recipe</td>
      <td>Rajma and Corn Salad Recipe</td>
      <td>1/2 cup Kashmiri Rajma - or regular rajma,1/2 ...</td>
      <td>1/2 cup Kashmiri Rajma - or regular rajma,1/2 ...</td>
      <td>15</td>
      <td>10</td>
      <td>25</td>
      <td>5</td>
      <td>Indian</td>
      <td>Side Dish</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Rajma and Corn Salad Recip...</td>
      <td>To begin making the Rajma and Corn Salad Recip...</td>
      <td>https://www.archanaskitchen.com/kidney-beans-c...</td>
    </tr>
    <tr>
      <th>2248</th>
      <td>सोया चंक्स सब्ज़ी रेसिपी - Soya Chunks Sabzi (R...</td>
      <td>Soya Chunks Sabzi (Recipe In Hindi)</td>
      <td>1 कप सोया चंक्स,4 कप पानी - गुनगुना,1 प्याज - ...</td>
      <td>1 cup soy chunks, 4 cups water - lukewarm, 1 o...</td>
      <td>10</td>
      <td>20</td>
      <td>30</td>
      <td>3</td>
      <td>Indian</td>
      <td>Lunch</td>
      <td>High Protein Vegetarian</td>
      <td>सोया चंक्स सब्ज़ी बनाने के लिए सबसे पहले सोया च...</td>
      <td>To make Soya Chunks vegetable, first of all, p...</td>
      <td>http://www.archanaskitchen.com/soya-chunks-sab...</td>
    </tr>
    <tr>
      <th>2373</th>
      <td>Matar Masala Tofu Recipe</td>
      <td>Matar Masala Tofu Recipe</td>
      <td>200 grams Tofu,3/4 cups Homemade tomato puree,...</td>
      <td>200 grams Tofu,3/4 cups Homemade tomato puree,...</td>
      <td>10</td>
      <td>10</td>
      <td>20</td>
      <td>2</td>
      <td>Indian</td>
      <td>Lunch</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Matar Masala Tofu Recipe, ...</td>
      <td>To begin making the Matar Masala Tofu Recipe, ...</td>
      <td>http://www.archanaskitchen.com/matar-masala-to...</td>
    </tr>
  </tbody>
</table>
</div>

We can also combine multiple conditions we set for the columns of the data frame like this. 

```python
high_protein_veg_recp = df[(df['Diet'] == 'High Protein Vegetarian') & (df['Cuisine'] == 'Indian') & (df['TotalTimeInMins'] < 31)].reset_index(drop=True)
```

```python
high_protein_veg_recp.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>RecipeName</th>
      <th>TranslatedRecipeName</th>
      <th>Ingredients</th>
      <th>TranslatedIngredients</th>
      <th>PrepTimeInMins</th>
      <th>CookTimeInMins</th>
      <th>TotalTimeInMins</th>
      <th>Servings</th>
      <th>Cuisine</th>
      <th>Course</th>
      <th>Diet</th>
      <th>Instructions</th>
      <th>TranslatedInstructions</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Soya Chunks Pepper Curry Recipe</td>
      <td>Soya Chunks Pepper Curry Recipe</td>
      <td>2 cups Soy Chunks (Nuggets),1 Green Bell Peppe...</td>
      <td>2 cups Soy Chunks (Nuggets),1 Green Bell Peppe...</td>
      <td>10</td>
      <td>20</td>
      <td>30</td>
      <td>3</td>
      <td>Indian</td>
      <td>Lunch</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Soya Chunks Pepper Curry r...</td>
      <td>To begin making the Soya Chunks Pepper Curry r...</td>
      <td>https://www.archanaskitchen.com/soya-chunks-pe...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>High-Protein Peanut Chutney Recipe-Indian Styl...</td>
      <td>High-Protein Peanut Chutney Recipe-Indian Styl...</td>
      <td>1/2 teaspoon Ghee,3/4 cup Roasted Peanuts (Moo...</td>
      <td>1/2 teaspoon Ghee,3/4 cup Roasted Peanuts (Moo...</td>
      <td>15</td>
      <td>15</td>
      <td>30</td>
      <td>5</td>
      <td>Indian</td>
      <td>Side Dish</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Peanut Chutney Recipe, fir...</td>
      <td>To begin making the Peanut Chutney Recipe, fir...</td>
      <td>http://www.archanaskitchen.com/peanut-chutney-...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Rajma and Corn Salad Recipe</td>
      <td>Rajma and Corn Salad Recipe</td>
      <td>1/2 cup Kashmiri Rajma - or regular rajma,1/2 ...</td>
      <td>1/2 cup Kashmiri Rajma - or regular rajma,1/2 ...</td>
      <td>15</td>
      <td>10</td>
      <td>25</td>
      <td>5</td>
      <td>Indian</td>
      <td>Side Dish</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Rajma and Corn Salad Recip...</td>
      <td>To begin making the Rajma and Corn Salad Recip...</td>
      <td>https://www.archanaskitchen.com/kidney-beans-c...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>सोया चंक्स सब्ज़ी रेसिपी - Soya Chunks Sabzi (R...</td>
      <td>Soya Chunks Sabzi (Recipe In Hindi)</td>
      <td>1 कप सोया चंक्स,4 कप पानी - गुनगुना,1 प्याज - ...</td>
      <td>1 cup soy chunks, 4 cups water - lukewarm, 1 o...</td>
      <td>10</td>
      <td>20</td>
      <td>30</td>
      <td>3</td>
      <td>Indian</td>
      <td>Lunch</td>
      <td>High Protein Vegetarian</td>
      <td>सोया चंक्स सब्ज़ी बनाने के लिए सबसे पहले सोया च...</td>
      <td>To make Soya Chunks vegetable, first of all, p...</td>
      <td>http://www.archanaskitchen.com/soya-chunks-sab...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Matar Masala Tofu Recipe</td>
      <td>Matar Masala Tofu Recipe</td>
      <td>200 grams Tofu,3/4 cups Homemade tomato puree,...</td>
      <td>200 grams Tofu,3/4 cups Homemade tomato puree,...</td>
      <td>10</td>
      <td>10</td>
      <td>20</td>
      <td>2</td>
      <td>Indian</td>
      <td>Lunch</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Matar Masala Tofu Recipe, ...</td>
      <td>To begin making the Matar Masala Tofu Recipe, ...</td>
      <td>http://www.archanaskitchen.com/matar-masala-to...</td>
    </tr>
  </tbody>
</table>
</div>

Notice, that I have also reset the index of the data frame by appending ```reset_index(drop=True)``` at the end of the conditions.

Finally, let's assume that you have Tofu in your fridge and you want to know what high protein dishes you can make using Tofu. We can do this by filtering the rows of the data frame based on ```tofu``` keyword. Let's print out the details for recipes that has Tofu in them. 

```python
# Create a Tofu data frame
tofu_df = pd.DataFrame()
```

```python
# find all the Tofu recipes and add them to the Tofu data frame
for p in high_protein_veg_recp['RecipeName']:
    if 'Tofu' in p:
        tofu_df = tofu_df.append(high_protein_veg_recp.loc[high_protein_veg_recp['RecipeName'] == p])
```

```python
# print out the tofu data frame
tofu_df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>RecipeName</th>
      <th>TranslatedRecipeName</th>
      <th>Ingredients</th>
      <th>TranslatedIngredients</th>
      <th>PrepTimeInMins</th>
      <th>CookTimeInMins</th>
      <th>TotalTimeInMins</th>
      <th>Servings</th>
      <th>Cuisine</th>
      <th>Course</th>
      <th>Diet</th>
      <th>Instructions</th>
      <th>TranslatedInstructions</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>Matar Masala Tofu Recipe</td>
      <td>Matar Masala Tofu Recipe</td>
      <td>200 grams Tofu,3/4 cups Homemade tomato puree,...</td>
      <td>200 grams Tofu,3/4 cups Homemade tomato puree,...</td>
      <td>10</td>
      <td>10</td>
      <td>20</td>
      <td>2</td>
      <td>Indian</td>
      <td>Lunch</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Matar Masala Tofu Recipe, ...</td>
      <td>To begin making the Matar Masala Tofu Recipe, ...</td>
      <td>http://www.archanaskitchen.com/matar-masala-to...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Mango Tofu Smoothie Recipe</td>
      <td>Mango Tofu Smoothie Recipe</td>
      <td>1 Ripe Bananas - spotty and frozen,1-1/2 cups ...</td>
      <td>1 Ripe Bananas - spotty and frozen,1-1/2 cups ...</td>
      <td>5</td>
      <td>5</td>
      <td>10</td>
      <td>2</td>
      <td>Indian</td>
      <td>World Breakfast</td>
      <td>High Protein Vegetarian</td>
      <td>To begin making the Mango Tofu smoothie, place...</td>
      <td>To begin making the Mango Tofu smoothie, place...</td>
      <td>http://www.archanaskitchen.com/mango-tofu-smoo...</td>
    </tr>
  </tbody>
</table>
</div>

Enjoy your Tofu recipes 😋
