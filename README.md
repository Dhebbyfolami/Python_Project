# Python_Project
Python project  for DATA Analysis.
# Project Overview
This sample sales analysis shows various activities in a SuperStores company :top selling products, most(highest) sales, least sales, most(highest) profits, least profits, sales trends across the states, cities, and regions.
It shows the Year, Month, Segment, product category, sub-category, numbers of customers.
## Project Title
Sales Analysis of products in SuperStore.
### Aims and Objectives
-To Highlight sales trend over time(month, year).
- To know the top selling product in the superstore.
- To know the Region, state, city with the most and least sales.
  ### Data Source
  It is a sample sales data from a Superstore.
  ### Tools Used
  Microsoft Excel, Python
  ### Treated Questions
- What are the top selling products in the superstore?
    
- What is the sales trend over time (monthly, year)?

- Which category of products generates the highest revenue and profit?

- Which region generates the most  sales?

- What is the impact of discounts and promotions -on sales?

- What is the average profit margin for each produc-t category?

- Which sub-category of products has the hi-ghest demand?

- Which Year had the most a-nd least sales?

- Which month had the most- and least sales?

- Which state had the mo-st and least sales?

- Which states had the m-ost and least profit?

- Which 3 cities had th-e most and least sales?

- Which 3 cities h-ad most and least profit?

- Which region had the most and least sa-les, most and least profit?

- How many products are being- sold in which shipping mode?

- What is the order value for each- product category by ship mode?

 - Which product category -has the highest and least orders?

 - Which sub-categor-y has the highest and least orders?

- Which sub-category has the- highest and lowest profit and sales?

 - How ma-ny customers are there in each segment?

  - Which segment had the most and least profit and sales?.
    
### Data Analysis
Some of the CODE use
#### Visualization the data Use.
```
SuperStore = pd.read_excel('Sample - Superstore.xlsx')

SuperStore.head()
```
####  The top selling products in the superstore
```
Top_sellingProducts = SuperStore.groupby('Product Name')['Sales'].sum().sort_values(ascending=False)

print(Top_sellingProducts.head(10))

#For Quantity sold
Top_sellingProducts = SuperStore.groupby('Product Name')['Quantity'].sum().sort_values(ascending=False)

print(Top_sellingProducts.head(10))
```
#### Sales trends over time(month, year).
```
#setting 'Order Date' to datetime format
SuperStore['Order Date'] = pd.to_datetime(SuperStore['Order Date'])

#Extract Year and Month
SuperStore['Year-Month'] = SuperStore['Order Date'].dt.to_period('M')

#Groupby Year-Mont and sum sales
Sales_trend = SuperStore.groupby('Year-Month')['Sales'].sum()

plt.figure(figsize=(12,6))
Sales_trend.plot(kind='line', marker='o', linestyle='-', color='green')
plt.xlabel('Year-Month')
plt.ylabel('Total Sales')
plt.title('Sales Trend Over Time')
plt.grid(True)
plt.show()
```

#### Category of products generates the highest revenue and profit
```
Category_Sales = SuperStore.groupby('Category')[['Sales', 'Profit']].sum().sort_values(by='Sales', ascending=False)

print(f'Category of products that generate the highest revenue and profit is:\n\n  {Category_Sales}')
```

#### Region that generates the most  sales.
```
HighestRegion_Sales = SuperStore.groupby('Region')['Sales'].sum().sort_values(ascending=False)

print(f'Region which generates the most sales is:\n \n {HighestRegion_Sales}')
```

#### The impact of discounts and promotions on sales
```
SuperStore['Has  Discount'] = SuperStore['Discount']> 0
discount_impact = SuperStore.groupby('Has  Discount')['Sales'].mean()
print(f'Impact of discount and promotion on sales:\n \n {discount_impact}')

sns.scatterplot(data=SuperStore, x='Discount', y='Sales')
```

#### Average profit margin for each product category.
```
SuperStore['Profit Margin'] = (SuperStore['Profit']/ SuperStore['Sales'])*100
CategoryProfit_Margin = SuperStore.groupby('Category')['Profit Margin'].mean().sort_values(ascending=False)

print(f'Average Profit Margin for each Product Category is:\n \n {CategoryProfit_Margin}')
```

####  Sub-category of products has the hi-ghest demand.
```
SubCategory_Demand = SuperStore.groupby('Sub-Category')['Quantity'].sum().sort_values(ascending=False)

print(f'Highest Sub-Category of product is:\n\n {SubCategory_Demand}')
```

#### Year with most and least sales.
```
SuperStore['Year'] =SuperStore['Order Date'].dt.year
YearlySales = SuperStore.groupby('Year')['Sales'].sum()

Most_Sales_year = YearlySales.idxmax()
Least_Sales_year= YearlySales.idxmin()

print(f'Year with the most sales:\n Year: {Most_Sales_year}\n Sales:{YearlySales.max()}\n')
print(f'Year with the least sales:\n Year: {Least_Sales_year}\n Sales:{YearlySales.min()}')
```

#### Month with the most and least sales.
```
SuperStore['Month'] =SuperStore['Order Date'].dt.month
MonthlySales = SuperStore.groupby('Month')['Sales'].sum()

Most_Sales_month = MonthlySales.idxmax()
Least_Sales_month = MonthlySales.idxmin()

print(f'Month with the most sales:\n Month: {Most_Sales_month}\n Sales:{MonthlySales.max()}\n')
print(f'Month with the least sales:\n Month: {Least_Sales_month}\n Sales:{MonthlySales.min()}')
```

#### State with the most and least sales.
```
StateSales = SuperStore.groupby('State')['Sales'].sum().sort_values(ascending=False)

Most_Sales_state = StateSales.idxmax()
Least_Sales_state = StateSales.idxmin()

print(f'State with the most sales:\n State: {Most_Sales_state}\n Sales:{StateSales.max()}\n')
print(f'State with the least sales:\n State: {Least_Sales_state}\n Sales:{StateSales.min()}')
```

#### Graphical representation of Yearly , Monthly, state sales.
```
# Yearly Sales
plt.figure(figsize=(10, 5))
sns.barplot(x=YearlySales.index, y=YearlySales.values, palette="Blues")
plt.title("Sales Per Year")
plt.xlabel("Year")
plt.ylabel("Total Sales")
plt.show()

# Monthly Sales
plt.figure(figsize=(10, 5))
sns.barplot(x=MonthlySales.index, y=MonthlySales.values, palette="Greens")
plt.title("Sales Per Month")
plt.xlabel("Month")
plt.ylabel("Total Sales")
plt.show()

# State Sales
plt.figure(figsize=(15,12))
StateSales.sort_values().plot(kind="barh", color="purple")
plt.title("Sales by State")
plt.xlabel("Total Sales")
plt.ylabel("State")
plt.show()
```

#### States with the most and least profit.
```
StateProfit = SuperStore.groupby('State')['Profit'].sum().sort_values(ascending=False)

Most_Profit_state = StateProfit.idxmax()
Least_Profit_state = StateProfit.idxmin()

print(f'State with the most profit:\n State: {Most_Profit_state}\n Sales:{StateProfit.max()}\n')
print(f'State with the least profit:\n State: {Least_Profit_state}\n Sales:{StateProfit.min()}')
```

 #### 3 cities with the most and least sales.
 ```
Most3Cities_Sales = CitySales.head(3)
Least3cities_Sales = CitySales.tail(3)

print(f'Top 3 cities with the most sales are:\n \n {Most3Cities_Sales}\n\n')
print(f'Bottom 3 cities with the least sales are:\n \n {Least3cities_Sales}')
```

#### 3 cities with the most and least profit.
```
CityProfit = SuperStore.groupby('City')['Profit'].sum().sort_values(ascending=False)

Most3Cities_Profit = CityProfit.head(3)
Least3cities_Profit = CityProfit.tail(3)

print(f'Top 3 cities with the most profit are:\n \n {Most3Cities_Profit}\n\n')
print(f'Bottom 3 cities with the least profit are:\n \n {Least3cities_Profit}')
```

#### Region with the most and least sales, most and least profit.
```
RegionSales = SuperStore.groupby('Region')['Sales'].sum().sort_values(ascending=False)

Most_Sales_Region = RegionSales.idxmax()
Least_Sales_Region = RegionSales.idxmin()

print(f'Region with the most sales:\n Region: {Most_Sales_Region}\n Sales:{RegionSales.max()}\n')
print(f'Region with the least sales:\n Region: {Least_Sales_Region}\n Sales:{RegionSales.min()}')

RegionProfit = SuperStore.groupby('Region')['Profit'].sum().sort_values(ascending=False)

Most_Profit_Region = RegionProfit.idxmax()
Least_Profit_Region = RegionProfit.idxmin()

print(f'Region with the most profit:\n Region: {Most_Profit_Region}\n Sales:{RegionProfit.max()}\n')
print(f'Region with the least profit:\n Region: {Least_Profit_Region}\n Sales:{RegionProfit.min()}')
```

#### Graphical representation of sales by region and profit by region.
```
plt.figure(figsize=(10, 5))
sns.barplot(x=RegionSales.index, y=RegionSales.values, palette="Reds")
plt.title("Sales by Region")
plt.xlabel("Region")
plt.ylabel("Total Sales")
plt.show()

plt.figure(figsize=(10, 5))
sns.barplot(x=RegionProfit.index, y=RegionProfit.values, palette="Purples")
plt.title("Profit by Region")
plt.xlabel("Region")
plt.ylabel("Total Profit")
plt.show()
```


#### Amount of  products  being sold and it shipping mode.
```
products_by_ship_mode = SuperStore.groupby("Ship Mode")["Product Name"].nunique()
print(products_by_ship_mode)
```

#### Order value for each product category by ship mode.
```
order_value = SuperStore.groupby(["Category", "Ship Mode"])["Sales"].sum().unstack()
print(order_value)
```

#### Product category with the highest and least orders.
```
category_orders = SuperStore.groupby("Category")["Order ID"].nunique().sort_values(ascending=False)

most_orders_category = category_orders.idxmax()
least_orders_category = category_orders.idxmin()

print(f"Category with most orders: {most_orders_category}\n  Orders: {category_orders.max()}\n\n")
print(f"Category with least orders: {least_orders_category} \n Orders: {category_orders.min()}")
```

#### Sub-category with the highest and least orders.
```
sub_category_orders = SuperStore.groupby("Sub-Category")["Order ID"].nunique().sort_values(ascending=False)

most_orders_sub_category = sub_category_orders.idxmax()
least_orders_sub_category = sub_category_orders.idxmin()

print(f"Sub-Category with most orders: {most_orders_sub_category} \n Orders: {sub_category_orders.max()}\n\n")
print(f"Sub-Category with least orders: {least_orders_sub_category}\n  Orders: {sub_category_orders.min()}")
```

#### Sub-category with the- highest and lowest profit and sales. 
```
Sub_categorySales = SuperStore.groupby('Sub-Category')['Sales'].sum().sort_values(ascending=False)

Most_Sales_Subcategory = Sub_categorySales.idxmax()
Least_Sales_Subcategory = Sub_categorySales.idxmin()

print(f'Sub-Category with the most sales:\n Sub-Category: {Most_Sales_Subcategory}\n Sales:{Sub_categorySales.max()}\n')
print(f'Sub-category with the least sales:\n Sub-CAtegory: {Least_Sales_Subcategory}\n Sales:{Sub_categorySales.min()}')

Sub_categoryProfit = SuperStore.groupby('Sub-Category')['Profit'].sum().sort_values(ascending=False)

Most_Profit_Subcategory = Sub_categoryProfit.idxmax()
Least_Profit_Subcategory = Sub_categoryProfit.idxmin()

print(f'Sub-Category with the most Profit:\n Sub-Category: {Most_Profit_Subcategory}\n Profit:{Sub_categoryProfit.max()}\n')
print(f'Sub-category with the least Profit:\n Sub-Category: {Least_Profit_Subcategory}\n Profit:{Sub_categoryProfit.min()}')
```

#### Numbers of  customers  in each segment.
```
customers_per_segment = SuperStore.groupby("Segment")["Customer ID"].nunique()
print(customers_per_segment)
```

####  Segment with the most and least profit and sales.
```
Segment_Profit = SuperStore.groupby('Segment')['Profit'].sum().sort_values(ascending=False)

Most_Profit_Segment = Segment_Profit.idxmax()
Least_Profit_Segment = Segment_Profit.idxmin()

print(f'Segment with the most Profit:\n Segment: {Most_Profit_Segment}\n Profit:{Segment_Profit.max()}\n')
print(f'Segment with the least Profit:\n Segment: {Least_Profit_Segment}\n Profit:{Segment_Profit.min()}')

Segment_Sales = SuperStore.groupby('Segment')['Sales'].sum().sort_values(ascending=False)

Most_Sales_Segment = Segment_Sales.idxmax()
Least_Sales_Segment = Segment_Sales.idxmin()

print(f'Segment with the most Sales:\n Segment: {Most_Sales_Segment}\n Profit:{Segment_Sales.max()}\n')
print(f'Segment with the least Sales:\n Segment: {Least_Sales_Segment}\n Profit:{Segment_Sales.min()}')
```

#### Graphical representation of Sales and Profit by segment.
```
# Sales by Segment
plt.figure(figsize=(8, 4))
sns.barplot(x=Segment_Sales.index, y=Segment_Sales.values, palette="Blues")
plt.title("Sales by Segment")
plt.xlabel("Segment")
plt.ylabel("Total Sales")
plt.show()

# Profit by Segment
plt.figure(figsize=(8, 4))
sns.barplot(x=Segment_Profit.index, y=Segment_Profit.values, palette="Greens")
plt.title("Profit by Segment")
plt.xlabel("Segment")
plt.ylabel("Total Profit")
plt.show()
```

