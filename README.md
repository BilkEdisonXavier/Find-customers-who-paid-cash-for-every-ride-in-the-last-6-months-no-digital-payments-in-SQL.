#Identify Cash-Only Customers in the Last 6 Months:

📌 Objective

This SQL program identifies customers who have exclusively used cash as their payment method for all rides taken in the last 6 months.
🗃️ Table Structure: ride_payments

The program uses a single table named ride_payments with the following schema:

| Column Name | Data Type | Description | 
| payment_id | INT | Unique identifier for each payment | 
| customer_id | INT | Unique identifier for each customer | 
| customer_name | VARCHAR(50) | Name of the customer | 
| payment_mode | VARCHAR(20) | Mode of payment (e.g., Cash, Credit) | 
| ride_date | DATE | Date of the ride | 


📥 Sample Data

INSERT INTO ride_payments VALUES
(1, 701, 'Gowtham', 'Cash', '2025-01-10'),
(2, 701, 'Gowtham', 'Cash', '2025-03-05'),
(3, 702, 'Anu', 'Credit Card', '2025-02-15'),
(4, 702, 'Anu', 'Cash', '2025-04-20');


🧠 Logic

- Filter rides that occurred within the last 6 months using DATE_SUB(CURDATE(), INTERVAL 6 MONTH).
- Group rides by customer_id and customer_name.
- Use a HAVING clause to ensure no rides in that period were paid using a mode other than cash.
  
🧮 SQL Query

SELECT customer_id, customer_name
FROM ride_payments
WHERE ride_date >= DATE_SUB(CURDATE(), INTERVAL 6 MONTH)
GROUP BY customer_id, customer_name
HAVING SUM(payment_mode != 'Cash') = 0;


✅ Output

This query returns a list of customers who:
- Took at least one ride in the last 6 months.
- Paid exclusively in cash for all those rides.
📌 Notes
- The SUM(payment_mode != 'Cash') expression counts how many rides were not paid in cash. If the sum is 0, it means all rides were paid in cash.
- This logic assumes that customers with no rides in the last 6 months are excluded from the result.


