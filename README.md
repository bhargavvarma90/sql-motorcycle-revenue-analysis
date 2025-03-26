A motorcycle parts retailer operating across three warehouses (retail & wholesale) wants to evaluate its wholesale net revenue performance. The company accepts credit cards, cash, and bank transfers, each incurring different processing fees. The board requested insights on:
	•	Net revenue by product line
	•	Revenue trends by month and warehouse
	•	Only wholesale orders included

⸻

🛠️ Methodology
	•	Filtered sales data to include only Wholesale clients
	•	Extracted the month from the transaction date
	•	Grouped data by product line, warehouse, and month
	•	Calculated net revenue = SUM(total) - SUM(payment_fee)

Code:


SELECT product_line,
    CASE WHEN EXTRACT('month' from date) = 6 THEN 'June'
         WHEN EXTRACT('month' from date) = 7 THEN 'July'
         WHEN EXTRACT('month' from date) = 8 THEN 'August'
    END as month,
    warehouse,
    SUM(total) - SUM(payment_fee) AS net_revenue
FROM sales
WHERE client_type = 'Wholesale'
GROUP BY product_line, warehouse, month
ORDER BY product_line, month, net_revenue DESC;
