I took part in the "25 Days of DAX Fridays! Challenge – Ed1: NorthWind Company" hosted by curbal.com. It involved solving a daily DAX puzzle, with a new challenge available every day from the 1st to the 25th of the month. It was a fantastic learning experience!

For this exercise, a modified version of the Northwind Dataset was made available. This dataset can be downloaded [via this link](https://curbal.com/wp-content/uploads/2021/12/Northwind-challenge_exercise-file.zip)


#                       DAY 1


## Question: How many current Products cost less than $20?

My initial solution provided a count of 39 using the following DAX formula:

```DAX
DAY1 = 
    CALCULATE(
        COUNT(Products[ProductID]),
        FILTER(Products, Products[Unit Price] < 20))
```

However, the correct answer should have been 37, and the correct DAX formula to achieve this is as follows:

```DAX
DAY1 = 
    CALCULATE(
        COUNT(Products[ProductID]),
        FILTER(Products, Products[Unit Price] < 20),
        FILTER(Products, Products[Discontinued] = FALSE()))
```

The corrected formula includes an additional filter condition to account for products that are not discontinued.


#                       DAY 2

## Question: Which product is the most expensive?

I experimented and made several attempts to create a DAX formula to address this specific question, but unfortunately, my efforts did not yield a successful result. Here is the formula  used to solve this particular problem.

```DAX
DAY2 = 

        CALCULATE(SELECTEDVALUE(Products[ProductName]),
        TOPN(1,Products,Products[UnitPrice],DESC))
```

### Explanation of Code 

1. `CALCULATE`: This is a DAX function used to modify the filter context for a calculation. It's used here to perform calculations based on certain conditions.

2. `SELECTEDVALUE(Products[ProductName])`: This part of the code returns the selected value of the "ProductName" column from the "Products" table. `SELECTEDVALUE` is often used to retrieve a single value from a column in the current filter context. It's like asking, "What is the selected product name?"

3. `TOPN(1, Products, Products[UnitPrice], DESC)`: This part of the code is a bit more complex. It uses the `TOPN` function to retrieve the top (or highest) value from a table. Here's how it works:

   - `1`: This specifies that you want to retrieve only one row (the top 1).
   - `Products`: This is the table from which you want to retrieve the row.
   - `Products[UnitPrice]`: This indicates that you want to use the "UnitPrice" column as the criterion for ranking.
   - `DESC`: This specifies that you want to rank the values in descending order, meaning you want the highest value.


