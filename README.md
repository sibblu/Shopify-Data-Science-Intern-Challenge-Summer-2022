<i>Find detailed solution & analysis in jupyternotebook (analysis.ipynb) </i>
<b>Question 1: Given some sample data, write a program to answer the following: <a href = 'https://docs.google.com/spreadsheets/d/16i38oonuX1y1g7C_UAmiK9GkY7cS-64DfiDMNiR41LM/edit#gid=0'>click here to access the required data set</a></b>

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 
<ol type='a'>
    <li><b>Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.</b>
        <ul>
        <li><i>The naive calculation of AOV ($3145.13) is wrong because it simply takes the mean of <b>"order_amount",i.e., sum of order_amount/number_of_orders (5000)</b>. Which doesn't gives a true picture because of presence of high volume (no. of items in order) orders, which skews the AOV. <b>Therefore, quantity of items in an order(total_items) and amount_per_item (new attribute, = order_amount/total_items) should be taken into account,</b> outliers should be removed with careful analysis.
        </i>
        </li>
        </ul>
    </li>
    <li><b>What metric would you report for this dataset? </b>
        <ul>
        <li><i>After analysing and removing outliers, we get following: </i>
            <li>Order values Mean: $302.5, Median: $284.0, Mode:$153</li>
            <li>amount_per_item values, Mean: $151.79, Median: $153.0, Mode: $153.0.</li>
            <li>total_items values, Mean:1.9947336439133077, Median:2.0, Mode:2</li>
            <li>When total_items per order = 2 (mode) [1816 such orders], order_amount Mean: $303.5, Median:306.0, Mode:306</li>
        </li>
        <li><b>Given above observations, it can be concluded that mean (average) order value $302.5 gives better picture of AOV. Even in case of most frequent orders with "total_item" = 2, the mean order value $303.5 is close to the general mean value ( $302.5).</b>
        </li>
        </ul>
    </li>
    <li>What is its value?
        <ul><li><b>$302.5</b></li>
        </ul>
    </li>


</ol>

<p><b>Question 2: For this question you’ll need to use SQL. <a href ="https://www.w3schools.com/SQL/TRYSQL.ASP?FILENAME=TRYSQL_SELECT_ALL"> Follow this link to access the data set required for the challenge. </a></b> Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.</p>


<p>a. How many orders were shipped by Speedy Express in total?</p>
<b>54</b>
<p>
<i>
SELECT COUNT(*) FROM Orders,Shippers 
WHERE Orders.ShipperID = Shippers.ShipperID AND ShipperName = "Speedy Express";
</i>
</p>
<p>b. What is the last name of the employee with the most orders?</p>
<b>Peacock</b>
<p>
<i>
SELECT LastName FROM Employees, Orders WHERE Employees.EmployeeID = Orders.EmployeeID
GROUP BY Orders.EmployeeID
ORDER BY Count(Employees.EmployeeID) DESC
LIMIT 1;
</i>
</p>
<p>c. What product was ordered the most by customers in Germany?</p>
<b>Boston Crab Meat</b>
<p>
<i>
SELECT prod.ProductName, SUM(det.Quantity) as quan
FROM Products prod JOIN OrderDetails det
ON prod.ProductID = det.ProductID
JOIN Orders Ord
ON det.OrderID = Ord.OrderID
JOIN Customers cus
ON cus.customerID = Ord.customerID
WHERE cus.Country = 'Germany'
GROUP BY prod.productName
ORDER BY quan DESC
LIMIT 1;
</i>
</p>
