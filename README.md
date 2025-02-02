**Data Cleaning and Preparation**
1. **Handling Missing Values:**
   - Replaced empty cells with "Blank."
   - Counted total missing values using `=COUNTIF(A1:R9801, "Blank")`.
   - Found that all 11 missing values were in the "Postal Code" column and decided to either remove the column or fix those rows.

2. **Fixing Date Issues:**
   - Some cells in "Order Date" and "Ship Date" had text values.
   - Used `Data > Text to Column > Delimited > Next > Next > Date (DMY) > Finish` to fix the date format.

**Data Analysis**
3. **Finding Highest Sales:**
   - Used `=MAX(R2:R9801)` to get the highest sales value.
   - Found the related product using `=INDEX(Q2:Q9801, MATCH(MAX(R2:R9801), R2:R9801, 0))`.

4. **Top 10 Best-Selling Products:**
   - Created a Pivot Table to show the top 10 products by sales.

5. **Total Sales by Category:**
   - Used a Pivot Table to calculate total sales for each category.

6. **Region with Most Orders:**
   - Identified unique regions using `UNIQUE(M2:M9801)`.
   - Counted orders per region using `COUNTIF(M2:M9801, UNIQUE(M2:M9801y))`.
   - Found the region with the most orders using `=INDEX(M2:M9801, MATCH(MAX(COUNTIF(M2:M9801, UNIQUE(M2:M9801)))))`.

7. **Top 10 Customers by Sales:**
   - Summed up sales per customer and sorted them using:
     ```
     =SORT(CHOOSE({1,2}, UNIQUE(train!G2:G9801), SUMIF(train!G2:G9801, UNIQUE(train!G2:G9801), train!R2:R9801)),2,-1)
     ```
   - Extracted the top 10 customers using `FILTER` and `LARGE`:
     ```
     =CHOOSE({1,2},FILTER(A3:A795, B3:B795>=LARGE(B3:B795,10)), FILTER(B3:B795, B3:B795>=LARGE(B3:B795,10)))
     ```
   - Alternative method with `SEQUENCE`:
     ```
     =CHOOSE({1,2}, INDEX(A3:A795, MATCH(LARGE(B3:B795, SEQUENCE(10)), B3:B795, 0)), LARGE(B3:B795, SEQUENCE(10)))
     ```

8. **Counting Sales Per Customer:**
   - Used `=SORT(CHOOSE({1,2,3}, UNIQUE(train!G2:G9801), SUMIF(train!G2:G9801, UNIQUE(train!G2:G9801), train!R2:R9801), COUNTIF(train!G2:G9801, UNIQUE(train!G2:G9801))),2,-1)`.

9. **Correlation Between Sales Count and Total Sales:**
   - Used `=CORREL(B4:B794,C4:C794)` to check the relationship between the two.

10. **Grouping Customers by Sales Volume:**
    - Classified customers based on their sales count:
      ```
      =IFS(C2<=10, "Low", (C2>10)*(C2<=20), "Medium", (C2>20)*(C2<=35), "High")
      ```

11. **Scatter Plot for Sales Data:**
    - Created a scatter plot to visualize the customer sales data.

12. **Sales by Shipping Class:**
    - Used `=SORT(CHOOSE({1,2,3}, UNIQUE(train!E2:E9801), SUMIF(train!E2:E9801, UNIQUE(train!E2:E9801), train!R2:R9801), COUNTIF(train!E2:E9801, UNIQUE(train!E2:E9801))),2,-1)`.
    - Created a pie chart for better visualization.

13. **Top Products Analysis with Pareto Chart:**
    - Total sales per product calculated using:
      ```
      =SORT(CHOOSE({1,2}, UNIQUE(INDEX(train!A2:R9801, 0, MATCH("Product Name", train!A1:R1, 0))), SUMIF( INDEX(train!A2:R9801, 0, MATCH("Product Name", train!A1:R1, 0)), UNIQUE(INDEX(train!A2:R9801, 0, MATCH("Product Name", train!A1:R1, 0))), INDEX(train!A2:R9801, 0, MATCH("Sales", train!A1:R1, 0)) ) ), 2, 1)
      ```
    - Cumulative sum calculated using:
      ```
      =SUM($B$2:B2)
      ```
    - Used Pareto chart to show the top-selling products.




