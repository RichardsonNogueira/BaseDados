1. Listar todos Clientes que não tenham realizado uma compra

SELECT c.customer_id, c.first_name, c.last_name
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;

2. Listar os Produtos que não tenham sido comprados

SELECT p.product_id, p.product_name
FROM products p
LEFT JOIN order_items oi ON p.product_id = oi.product_id
WHERE oi.product_id IS NULL;

4. Listar os Produtos sem Estoque

SELECT p.product_id, p.product_name
FROM products p
LEFT JOIN stocks s ON p.product_id = s.product_id
WHERE s.quantity IS NULL OR s.quantity = 0;

6. Agrupar a quantidade de vendas de uma determinada Marca por Loja

SELECT b.brand_name,
       st.store_name,
       SUM(oi.quantity) AS total_vendido
FROM order_items oi
JOIN orders o ON oi.order_id = o.order_id
JOIN stores st ON o.store_id = st.store_id
JOIN products p ON oi.product_id = p.product_id
JOIN brands b ON p.brand_id = b.brand_id
GROUP BY b.brand_name, st.store_name
ORDER BY b.brand_name, st.store_name;
   
8. Listar os Funcionários que não estejam relacionados a um Pedido

SELECT s.staff_id, s.first_name, s.last_name
FROM staffs s
LEFT JOIN orders o ON s.staff_id = o.staff_id
WHERE o.order_id IS NULL;
