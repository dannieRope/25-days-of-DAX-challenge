I took part in the "25 Days of DAX Fridays! Challenge – Ed1: NorthWind Company" hosted by curbal.com. It involved solving a daily DAX puzzle, with a new challenge available every day from the 1st to the 25th of the month. It was a fantastic learning experience!

For this exercise, a modified version of the Northwind Dataset was made available. This dataset can be downloaded [via this link](https://curbal.com/wp-content/uploads/2021/12/Northwind-challenge_exercise-file.zip)


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



#                       DAY 7


## Question: What is the order value in $ of open orders? (not Shipped yet)



#                       DAY 8


## Question: How many orders are "single items" (only one product ordered)?


#                       DAY 9


## Question: Average sales per transaction (orderId) for "Romero y Tomillo"
