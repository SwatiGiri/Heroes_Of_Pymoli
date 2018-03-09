#Analysis Report
1. 81% of players are male which also make the most of the percentage of the revenue.
2. The game is most popular among the age group of 15 years to 25 years  and after that age group there is drastic decline in player's interest.
3. The most popular items are below the average price of most of the items.
4. However the most popular items are not the most profitable items. The most profitable items are the item number 34 and 115 which are more pricy.




# Code

```python
import pandas as pd

from pprint import pprint

data = pd.read_json('purchase_data.json')
# View data
# print(data.head())
```


```python
# Number of players
unique_players = len(data["SN"].unique())
pd.DataFrame({"Total Players": [unique_players]})
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>



<h1>Purchasing Analysis (Total) </h1>


```python
temp_df = pd.DataFrame()
# * Number of Unique Items
unique_items = len(data['Item ID'].unique())
temp_df["Number of Unique Items"] = [unique_items]

# * Average Purchase Price
avg_price = round(data["Price"].mean(), 2)
temp_df["Average Purchase Price"] = avg_price

# * Total Number of Purchases
total_purchases = len(data)
temp_df["Total Purchases"] = total_purchases

# * Total Revenue
total_revenue = round(data["Price"].sum(), 2)
temp_df["Total Revenue"] = total_revenue
temp_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Purchase Price</th>
      <th>Total Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>2.93</td>
      <td>780</td>
      <td>2286.33</td>
    </tr>
  </tbody>
</table>
</div>



<h1> **Gender Demographics** </h1>


```python

# Removing duplicate players from the data
data_without_duplicate_players = data.drop_duplicates(subset=["SN"])

# Seperating the no duplicate data into gender groups
gender_groups = data_without_duplicate_players["Gender"].value_counts()

# Printing Percentage of palyers and total count according to their gender
x = pd.DataFrame({"Total Count":gender_groups,
                   "Percentage of Players": round(gender_groups/unique_players * 100, 2)})
x

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>81.15</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.40</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



<h1> **Purchasing Analysis (Gender)** </h1>


```python
# Number of purchases by each gender
grouped_data = data.groupby(["Gender"])
purchases = pd.DataFrame()
for gender, info in grouped_data:
    price_column = info["Price"]
    purchase = pd.DataFrame({
        "Total Purchases" : [len(info)],
        "Average Purchase Price" : [round(price_column.mean(), 2)],
        "Total Purchase Value" : [price_column.sum()]
    }, index=[gender])
    purchases = purchases.append(purchase)
#   TODO : Figure out how to calculate Normalized Totals
purchases
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Total Purchases</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>2.82</td>
      <td>382.91</td>
      <td>136</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2.95</td>
      <td>1867.68</td>
      <td>633</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>3.25</td>
      <td>35.74</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>



<h1>**Age Demographics**</h1>


```python
# TODO:  Need to Redo - Incorrect
# Number of purchases by each gender
grouped_data = data.groupby(["Age"])
purchases = pd.DataFrame()
for age, info in grouped_data:
    price_column = info["Price"]
    purchase = pd.DataFrame({
        "Total Purchases" : [len(info)],
        "Average Purchase Price" : [round(price_column.mean(), 2)],
        "Total Purchase Value" : [price_column.sum()]
    }, index=[age])
    purchases = purchases.append(purchase)
#   TODO : Figure out how to calculate Normalized Totals
purchases
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Total Purchases</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>2.92</td>
      <td>55.47</td>
      <td>19</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.96</td>
      <td>5.87</td>
      <td>3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3.69</td>
      <td>22.12</td>
      <td>6</td>
    </tr>
    <tr>
      <th>10</th>
      <td>3.29</td>
      <td>13.16</td>
      <td>4</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2.97</td>
      <td>26.76</td>
      <td>9</td>
    </tr>
    <tr>
      <th>12</th>
      <td>3.84</td>
      <td>19.21</td>
      <td>5</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2.14</td>
      <td>23.52</td>
      <td>11</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2.38</td>
      <td>14.30</td>
      <td>6</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2.99</td>
      <td>140.36</td>
      <td>47</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2.64</td>
      <td>60.71</td>
      <td>23</td>
    </tr>
    <tr>
      <th>17</th>
      <td>3.01</td>
      <td>51.11</td>
      <td>17</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2.80</td>
      <td>67.14</td>
      <td>24</td>
    </tr>
    <tr>
      <th>19</th>
      <td>3.05</td>
      <td>67.10</td>
      <td>22</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2.88</td>
      <td>282.68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2.80</td>
      <td>120.37</td>
      <td>43</td>
    </tr>
    <tr>
      <th>22</th>
      <td>3.03</td>
      <td>206.05</td>
      <td>68</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2.74</td>
      <td>156.21</td>
      <td>57</td>
    </tr>
    <tr>
      <th>24</th>
      <td>3.05</td>
      <td>213.46</td>
      <td>70</td>
    </tr>
    <tr>
      <th>25</th>
      <td>3.08</td>
      <td>206.52</td>
      <td>67</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2.45</td>
      <td>31.83</td>
      <td>13</td>
    </tr>
    <tr>
      <th>27</th>
      <td>3.06</td>
      <td>58.21</td>
      <td>19</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2.56</td>
      <td>12.81</td>
      <td>5</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2.90</td>
      <td>60.96</td>
      <td>21</td>
    </tr>
    <tr>
      <th>30</th>
      <td>3.11</td>
      <td>56.01</td>
      <td>18</td>
    </tr>
    <tr>
      <th>31</th>
      <td>2.98</td>
      <td>47.62</td>
      <td>16</td>
    </tr>
    <tr>
      <th>32</th>
      <td>3.41</td>
      <td>37.50</td>
      <td>11</td>
    </tr>
    <tr>
      <th>33</th>
      <td>2.89</td>
      <td>31.80</td>
      <td>11</td>
    </tr>
    <tr>
      <th>34</th>
      <td>3.04</td>
      <td>24.32</td>
      <td>8</td>
    </tr>
    <tr>
      <th>35</th>
      <td>3.08</td>
      <td>37.02</td>
      <td>12</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2.88</td>
      <td>20.14</td>
      <td>7</td>
    </tr>
    <tr>
      <th>37</th>
      <td>2.35</td>
      <td>21.11</td>
      <td>9</td>
    </tr>
    <tr>
      <th>38</th>
      <td>2.87</td>
      <td>25.79</td>
      <td>9</td>
    </tr>
    <tr>
      <th>39</th>
      <td>3.07</td>
      <td>15.34</td>
      <td>5</td>
    </tr>
    <tr>
      <th>40</th>
      <td>3.22</td>
      <td>45.11</td>
      <td>14</td>
    </tr>
    <tr>
      <th>42</th>
      <td>2.11</td>
      <td>2.11</td>
      <td>1</td>
    </tr>
    <tr>
      <th>43</th>
      <td>3.81</td>
      <td>3.81</td>
      <td>1</td>
    </tr>
    <tr>
      <th>45</th>
      <td>2.72</td>
      <td>2.72</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



<h1>**Top Spenders**</h1>


```python
# Grouping the players and their purchases. 
grouped_players = data.groupby(["SN"])

players_info = pd.DataFrame()

# Going through every player and storing important values
for name, info in grouped_players:
    price_column = info["Price"]
    spender_info = pd.DataFrame({
        'Purchase Count': [len(price_column)],
        'Average Purchase Price' : [price_column.mean()],
        'Total Purchase Value' : [price_column.sum()]
    }, index=[name])
    # Need to store append value back into players_info because the person who wrote append was retarted
    players_info = players_info.append(spender_info, ignore_index=False)

top_5_spenders = players_info.sort_values(by="Total Purchase Value", ascending=False).head()
top_5_spenders.style.format({'Total Purchase Value': '${:.2f}', 'Average Purchase Price': '${:.2f}'})
```




<style  type="text/css" >
</style>  
<table id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Purchase Count</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1level0_row0" class="row_heading level0 row0" >Undirrala66</th> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row0_col0" class="data row0 col0" >$3.41</td> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row0_col1" class="data row0 col1" >5</td> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row0_col2" class="data row0 col2" >$17.06</td> 
    </tr>    <tr> 
        <th id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1level0_row1" class="row_heading level0 row1" >Saedue76</th> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row1_col0" class="data row1 col0" >$3.39</td> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row1_col1" class="data row1 col1" >4</td> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row1_col2" class="data row1 col2" >$13.56</td> 
    </tr>    <tr> 
        <th id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1level0_row2" class="row_heading level0 row2" >Mindimnya67</th> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row2_col0" class="data row2 col0" >$3.18</td> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row2_col1" class="data row2 col1" >4</td> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row2_col2" class="data row2 col2" >$12.74</td> 
    </tr>    <tr> 
        <th id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1level0_row3" class="row_heading level0 row3" >Haellysu29</th> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row3_col0" class="data row3 col0" >$4.24</td> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row3_col1" class="data row3 col1" >3</td> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row3_col2" class="data row3 col2" >$12.73</td> 
    </tr>    <tr> 
        <th id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1level0_row4" class="row_heading level0 row4" >Eoda93</th> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row4_col0" class="data row4 col0" >$3.86</td> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row4_col1" class="data row4 col1" >3</td> 
        <td id="T_7ec67dc6_236c_11e8_8f3a_c292594352d1row4_col2" class="data row4 col2" >$11.58</td> 
    </tr></tbody> 
</table> 



<h1> Most Popular Items </h1>


```python
grouped_items = data.groupby(["Item ID"])
items = pd.DataFrame()


# # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #
#  Using mean to get just 1 value instead of all the values #
# # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #
for item_id, info in grouped_items:
    item = pd.DataFrame({
        "Item ID": [item_id],
        "Purchase Count" : [len(info)],
        "Item Price": [info["Price"].mean()],
        "Total Purchase Value": [info["Price"].sum()]
    }, index=[[data.loc[item_id]["Item Name"]]])
    items = items.append(item, ignore_index=False)

top_5_items = items.sort_values(by="Purchase Count", ascending=False).head()
top_5_items
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Stormfury Mace</th>
      <td>39</td>
      <td>2.35</td>
      <td>11</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>Thorn, Satchel of Dark Souls</th>
      <td>84</td>
      <td>2.23</td>
      <td>11</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>Shadow Strike, Glory of Ending Hope</th>
      <td>31</td>
      <td>2.07</td>
      <td>9</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>Retribution Axe</th>
      <td>175</td>
      <td>1.24</td>
      <td>9</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>Piety, Guardian of Riddles</th>
      <td>13</td>
      <td>1.49</td>
      <td>9</td>
      <td>13.41</td>
    </tr>
  </tbody>
</table>
</div>



<h1> Most Profitable Items </h1>


```python
top_5_profitable_items = items.sort_values(by="Total Purchase Value", ascending=False).head()
top_5_profitable_items
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alpha, Reach of Ending Hope</th>
      <td>34</td>
      <td>4.14</td>
      <td>9</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>Thorn, Conqueror of the Corrupted</th>
      <td>115</td>
      <td>4.25</td>
      <td>7</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>Rage, Legacy of the Lone Victor</th>
      <td>32</td>
      <td>4.95</td>
      <td>6</td>
      <td>29.70</td>
    </tr>
    <tr>
      <th>Mercy, Katana of Dismay</th>
      <td>103</td>
      <td>4.87</td>
      <td>6</td>
      <td>29.22</td>
    </tr>
    <tr>
      <th>Spectral Diamond Doomblade</th>
      <td>107</td>
      <td>3.61</td>
      <td>8</td>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>


