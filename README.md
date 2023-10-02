# 25 Days of DAX Fridays! Challenge – Ed1: NorthWind Company

I took part in the "25 Days of DAX Fridays! Challenge – Ed1: NorthWind Company" hosted by curbal.com. It involved solving a daily DAX puzzle, with a new challenge available every day from the 1st to the 25th of the month. It was a fantastic learning experience!

For this exercise, a modified version of the Northwind Dataset was made available. This dataset can be downloaded [via this link](https://curbal.com/wp-content/uploads/2021/12/Northwind-challenge_exercise-file.zip)

#  THE DATASET 

The Northwind database contains the sales data for a fictitious company called “Northwind Traders,” which imports and exports specialty foods from around the world. 
The Northwind database is an excellent tutorial schema for a small-business ERP, with customers, orders, inventory, purchasing, suppliers, shipping, employees, and single-entry accounting.

The Northwind dataset includes sample data for the following.

`Suppliers:` Suppliers and vendors of Northwind

`Customers:` Customers who buy products from Northwind

`Employees:` Employee details of Northwind traders

`Products:` Product information

`Shippers:` The details of the shippers who ship the products from the traders to the end-customers

`Orders and Order_Details:` Sales Order transactions taking place between the customers & the company

For the purpose of this exercise, the dataset has been modified and loaded into PowerBI Desktop.



*how the data model looks like*

![northwind Data Model](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/98023d50-1376-4c9c-a194-00d6354e839c)


#                       DAY 1


## Question: How many current Products cost less than $20?

Answer: `37`

My initial solution provided a count of 39 using the DAX code:

```DAX
DAY1 = 
    CALCULATE(
        COUNT(Products[ProductID]),
        FILTER(Products, Products[Unit Price] < 20))
```

However, the correct answer should have been 37, and the correct DAX code used to achieve this is as follows:

```DAX
DAY1 = 
    CALCULATE(
        COUNT(Products[ProductID]),
        FILTER(Products, Products[Unit Price] < 20),
        FILTER(Products, Products[Discontinued] = FALSE()))
```

The corrected formula includes an additional filter condition to account for products that are not discontinued. This gives the count of current products. 

![DAY 1](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/f5dd6528-1f13-42ee-b510-3b1d728e6b99)



#                       DAY 2

## Question: Which product is the most expensive?

Answer: `cote de Baye`

I experimented and made several attempts to create a DAX formula to address this specific question, but unfortunately, my efforts did not yield a successful result. Here is the formula  used to solve this particular problem.

```DAX
DAY2 = 

        CALCULATE(SELECTEDVALUE(Products[ProductName]),
        TOPN(1,Products,Products[UnitPrice],DESC))
```


![DAY2](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/31287b7b-818e-481d-b697-26a3cdce6c16)


### Explanation of Code 

1. `CALCULATE`: This is a DAX function used to modify the filter context for a calculation. It's used here to perform calculations based on certain conditions.

2. `SELECTEDVALUE(Products[ProductName])`: This part of the code returns the selected value of the "ProductName" column from the "Products" table. `SELECTEDVALUE` is often used to retrieve a single value from a column in the current filter context. It's like asking, "What is the selected product name?"

3. `TOPN(1, Products, Products[UnitPrice], DESC)`: This part of the code is a bit more complex. It uses the `TOPN` function to retrieve the top (or highest) value from a table. Here's how it works:

   - `1`: This specifies that you want to retrieve only one row (the top 1).
   - `Products`: This is the table from which you want to retrieve the row.
   - `Products[UnitPrice]`: This indicates that you want to use the "UnitPrice" column as the criterion for ranking.
   - `DESC`: This specifies that you want to rank the values in descending order, meaning you want the highest value.

After dedicating time to comprehending the aforementioned DAX formula, I devised an alternative approach that yielded the same outcome.

```DAX
DAY2 ALT =
    CALCULATE(
    SELECTEDVALUE(Products[ProductName]),
    FILTER(Products,Products[UnitPrice]=MAX(Products[UnitPrice])))
```

![DAY2 ALT](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/c90cac7d-4a0a-400f-ab32-70ffc98324b3)


#                       DAY 3


## Question: What is the average unit price for our products?

Answer: `28.87`

DAX code used to get the answer

```
DAY3 = AVERAGE(Products[UnitPrice])
```

![DAY3](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/932982e1-868c-459c-b6f1-fed5529b2a62)


#                       DAY 4


## Question: How many Products are above the average unit price?

Answer: `25`

DAX codes used to get the answer

```DAX
DAY4 = 
        VAR _AVG = AVERAGE(Products[UnitPrice])
        RETURN 
        CALCULATE(
        COUNT(Products[ProductID]),
        FILTER(Products,Products[Unit Price]>_AVG))
```

![DAY4](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/5440bc26-a52d-4480-b538-6919774b3cb7)


```
DAY4 ALT = 
        CALCULATE(
            COUNT(Products[ProductID]),
            FILTER(Products,Products[Unit Price]>AVERAGE(Products[UnitPrice])
            ))
```

![DAY4 ALT](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/94e3be96-121f-4092-8a4b-0d778ec40364)


#                       DAY 5

## Question: How many Products cost between $15 and $25?

Answer: `25`

DAX codes used to get the answer

```
DAY 5 = CALCULATE(
        COUNT(Products[ProductName]),
        FILTER(Products,(Products[Unit Price]) >= 15 && (Products[Unit Price]<= 25)))
```

![DAY5](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/fa715e33-691f-43b7-a51d-ab5696936d9a)


#                       DAY 6


## Question: What is the average number of products (not quantity) per order?

Answer: `2.60`
```
DAY6 = 
 AVERAGEX(
     SUMMARIZE(Orders,Orders[OrderID],"productCount",COUNT(Orders[ProductID])),
     [productCount])
```

![DAY6](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/18151834-6e55-4a41-b4ee-73ce91a78784)


#                       DAY 7

## Question: What is the order value in $ of open orders? (not Shipped yet)

Answer: `$27.44K`

```
DAY7 = CALCULATE(
       SUM(Orders[_Sales]),
       FILTER(Orders,Orders[ShippedDate] = BLANK()))
```

![DAY7](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/96b593d6-3407-47e2-9ab9-2305ae7681d2)


#                       DAY 8


## Question: How many orders are "single items" (only one product ordered)?

Answer: `137`

```
DAY8 = CALCULATE(
        COUNT(Orders[OrderID]),
        FILTER(SUMMARIZE(Orders,Orders[OrderID],"productCount",COUNT(Orders[ProductID])),
        [productCount] = 1))
```

![DAY8](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/75883610-7473-4d86-85b3-13bb5dbb6aee)


#                       DAY 9

## Question: Average sales per transaction (orderId) for "Romero y Tomillo"

Answer: `293.46`

```
DAY9 = CALCULATE(
        AVERAGEX(VALUES(Orders[OrderID]),[Total sales]),
        FILTER(Customers,Customers[CompanyName] = "Romero y tomillo"))
```

![DAY9](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/43b6063f-a1d1-4dc4-9955-b187f62dd38a)


```
DAY9ALT = CALCULATE(
        DIVIDE(SUM(Orders[_Sales]),DISTINCTCOUNT(Orders[OrderID]),0),
        FILTER(Orders,Orders[CustomerID] = "ROMEY"))
```

![DAY9ALT](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/740c5490-ecf2-4b5d-a4e2-78beb71b7236)


#                       DAY 10

## Question: How many days have passed since "North/South" last purchased?

Answer: `656`

```
DAY10 = CALCULATE(
        DATEDIFF(MAX(Orders[OrderDate]),TODAY(),DAY),
        FILTER(Customers,Customers[CompanyName] = "North/South"))
```

![DAY10](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/8e309d68-b49c-49a5-868f-56e8ac1c9d92)



#                       DAY 11

## Question: How many customers have ordered only once?

Answer: `1`

```
DAY11 = CALCULATE(
        DISTINCTCOUNT(Orders[CustomerID]),
        FILTER(SUMMARIZE(Orders,Orders[CustomerID],"OrdersCount",DISTINCTCOUNT(Orders[OrderID])),
        [OrdersCount] = 1))

```

![DAY11](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/01968b51-1425-492c-b719-aa0de53d421e)


#                       DAY 12

## Question: How many new customers (first purchase in the year 2021)?

Answer: `293.46`

```

DAY12 = CALCULATE(
        DISTINCTCOUNT(Orders[CustomerID]),
        FILTER(SUMMARIZE(Orders,Orders[CustomerID],"firstDate",FIRSTDATE(Orders[OrderDate])),
        YEAR([firstDate]) = 2021))
```

![DAY12](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/938f31a3-cff3-4217-81d0-f298e5bbb99b)


#                       DAY 13

## Question: how many lost customers (no purchases in currenty year)?

Answer: `2`

```
DAY13 = CALCULATE(
        DISTINCTCOUNT(Orders[CustomerID]),
        FILTER(SUMMARIZE(Orders,Orders[CustomerID],"lastDate",LASTDATE(Orders[OrderDate])),
        YEAR([lastDate]) <> 2021))
```
![DAY13](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/5b363395-4f05-4fa5-8288-f3786a78d06e)


#                       DAY 14

## Question:how many customers have never purchased Queso Cabrales?

Answer: `59`

![DAY14](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/1e962e9b-7a24-4c94-a52c-43c1ef40098c)




#                       DAY 15

## Question: How many customers have purchased only Queso Cabrales?

Answer: `5`

![DAY15](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/57fffd72-8c7c-42f7-8b9b-187a166eee48)


#                       DAY 16

## Question: How many products are out of stock?

Answer: `5`

![DAY16](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/cc69c308-09b7-4435-802c-c49303d56798)


![DAY16ALT](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/6d60b9ff-4156-4b77-8746-c12508163e95)


#                       DAY 17

## Question: How many products need to be restocked (based on restock level)?

Answer: `18`

![DAY17](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/6848f1ad-807a-4b7d-9ae6-ef542e34ab1b)



![DAY17ALT](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/7604f4f7-6acd-4114-9b0a-a9171d6cc98f)


#                       DAY 18

## Question: How many products on order do we need to restock?

Answer: `14`

![DAY18](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/bd4fe4b2-dddc-40ed-895f-ab0270513efd)




![DAY18ALT](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/a0a009a8-f55d-441b-a8ca-f7ee8725e97b)

#                       DAY 19

## Question: What is the stocked value of the discontinued products?

Answer: `$4.45k`

```
DAY19 = 
CALCULATE(SUMX(Products,[Stocked units]*Products[Unit Price]), Products[Discontinued] = TRUE())

```

![DAY19](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/c67b9c92-8248-4319-a77e-5ce1ff703346)

#                       DAY 20

## Question: Which vendor has the highest stocked value?

Answer: `Aux joyeux ecclesiatiques`

```
DAY20 = 
CALCULATE(
SELECTEDVALUE(Suppliers[CompanyName]),
TOPN(1,SUMMARIZE(Products,Suppliers[CompanyName],"StockValue",SUMX(Products,Products[Stocked units]*Products[Unit Price])),[StockValue],DESC))

```

![DAY20](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/b08d707d-3e56-4313-b545-87ff5a93837f)

#                       DAY 21

## Question: How many employees (%) are female?

Answer: `55.6%`

```
DAY21 = 
    VAR employeeCount = COUNTA(Employees[EmployeeID])
    VAR femaleCount = CALCULATE( COUNTA(Employees[EmployeeID]),
                                Employees[Gender] = "female")
    RETURN DIVIDE(femaleCount,employeeCount,0)
```

![DAY21](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/de7e0afd-8bd3-4633-982f-479471bcd08a)


#                       DAY 22

## Question: How many employees are 60 years or over?

Answer: `2`

```
DAY22 = 
    CALCULATE( COUNT(Employees[EmployeeID]),
               FILTER(Employees,DATEDIFF(Employees[BirthDate],TODAY(),YEAR) >=60))

```



#                       DAY 23

## Question:Which employee had the highest sales in 2021?

Answer: `Nancy Davolio`

```
DAY23 = 
    CALCULATE( SELECTEDVALUE(Employees[Full Name]),
    TOPN(1,FILTER(SUMMARIZE(Orders,Employees[Full Name],'Calendar'[Year],"sales",SUM(Orders[_Sales])),'Calendar'[Year]=2021),   [sales],DESC))

```

![DAY23](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/de2bd93f-63dd-400b-a5b2-e181fdbd7166)


```
DAY23ALT = 
CALCULATE(SELECTEDVALUE(Employees[Full Name]),
TOPN(1,Employees,CALCULATE([Total sales],'Calendar'[Year] = 2021),DESC))

```

![DAY23ALT](https://github.com/dannieRope/25-days-of-DAX-challenge/assets/132214828/2b3157f3-c98a-4ff9-89a7-4592849cb604)

#                       DAY 24

## Question: How many employees sold over $100k in 2021?

Answer: `4`

```
DAY24 = 
    CALCULATE( 
              COUNTA(Employees[Full Name]),
              FILTER(
                     SUMMARIZE(Orders,Employees[Full Name],'Calendar'[Year],"sales",SUM(Orders[_Sales])),'Calendar'[Year]=2021 && [sales] > 100000))
```


#                       DAY 25

## Question: How many employees got hired in 1994?

Answer: `2`

