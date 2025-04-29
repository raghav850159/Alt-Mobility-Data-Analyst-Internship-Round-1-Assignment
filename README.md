# Alt-Mobility-Data-Analyst-Internship-Round-1-Assignment

1)Number of Orders per Month:
SELECT 
    EXTRACT(YEAR FROM order_date) AS order_year,
    EXTRACT(MONTH FROM order_date) AS order_month,
    COUNT(order_id) AS total_orders
FROM 
    customer_orders
GROUP BY 
    EXTRACT(YEAR FROM order_date),
    EXTRACT(MONTH FROM order_date)
ORDER BY 
    order_year, order_month;

2)Total Sales Revenue per Month:
SELECT 
    EXTRACT(YEAR FROM order_date) AS sales_year,
    EXTRACT(MONTH FROM order_date) AS sales_month,
    SUM(order_amount) AS total_sales
FROM 
    customer_orders
GROUP BY 
    EXTRACT(YEAR FROM order_date),
    EXTRACT(MONTH FROM order_date)
ORDER BY 
    sales_year, sales_month;
    
3)Order Status Breakdown:
SELECT 
    order_status,
    COUNT(order_id) AS status_count
FROM 
    customer_orders
GROUP BY 
    order_status;
    
4)Average Order Value:
SELECT 
    AVG(order_amount) AS avg_order_value
FROM 
    customer_orders;

5)Fulfillment Rate:
SELECT 
    COUNT(CASE WHEN order_status = 'Delivered' THEN 1 END) AS delivered_orders,
    COUNT(order_id) AS total_orders,
    (COUNT(CASE WHEN order_status = 'Delivered' THEN 1 END) * 100.0) / COUNT(order_id) AS fulfillment_rate
FROM 
    customer_orders;
    
6)New vs Returning Customers:
SELECT 
    CASE 
        WHEN COUNT(order_id) = 1 THEN 'New Customer'
        ELSE 'Returning Customer'
    END AS customer_type,
    COUNT(*) AS customer_count
FROM 
    customer_orders
GROUP BY 
    customer_name
ORDER BY 
    customer_type;

7)Average Orders per Customer:
SELECT 
    AVG(order_count) AS avg_orders_per_customer
FROM (
    SELECT 
        customer_name,
        COUNT(order_id) AS order_count
    FROM 
        customer_orders
    GROUP BY 
        customer_name
) AS subquery;

8) Customer Lifetime Value (LTV):
SELECT 
    customer_name,
    SUM(order_amount) AS lifetime_value
FROM 
    customer_orders
GROUP BY 
    customer_name
ORDER BY 
    lifetime_value DESC;
   
10) Payment Status Analysis :
    SELECT 
    (SUM(CASE WHEN payment_status = 'Success' THEN 1 ELSE 0 END) * 100.0) / COUNT(payment_id) AS payment_success_rate
FROM 
    payments;

11) Top Failure Reasons:
SELECT 
    failure_reason,
    COUNT(payment_id) AS failure_count
FROM 
    payments
WHERE 
    payment_status = 'Failed'
GROUP BY 
    failure_reason
ORDER BY 
    failure_count DESC;

12)Payment Success Rate by Payment Method:
SELECT 
    payment_method,
    (SUM(CASE WHEN payment_status = 'Success' THEN 1 ELSE 0 END) * 100.0) / COUNT(payment_id) AS success_rate
FROM 
    payments
GROUP BY 
    payment_method;




