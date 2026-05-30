CREATE TABLE `kimia_farma.analisa_transaksi` AS SELECT 
ft.transaction_id, 
ft.date, 
ft.branch_id, 
kc.branch_name, 
kc.kota, 
kc.provinsi, 
kc.rating AS rating_cabang, 
ft.customer_name, 
ft.product_id, 
p.product_name, 
p.price AS actual_price, 

-- Persentase gross laba berdasarkan harga 
ft.discount_percentage,
CASE WHEN p.price <= 50000 THEN 0.10 WHEN p.price <= 100000 THEN 0.15 
WHEN p.price <= 300000 THEN 0.20 
WHEN p.price <= 500000 THEN 0.25 ELSE 0.30 END AS persentase_gross_laba,

 -- Kalkulasi nett sales & nett profit
p.price*(1-ft.discount_percentage) as nett_sales,
p.price*(1-ft.discount_percentage)*case
WHEN p.price <= 50000 THEN 0.10
WHEN p.price <=100000 THEN 0.15
WHEN p.price <= 300000 THEN 0.20
WHEN p.price <= 500000 THEN 0.25
else 0.30
end as nett_profit,
ft.rating AS rating_transaksi
from `kimia_farma.kf_final_transaction`ft
LEFT JOIN `kimia_farma.kf_kantor_cabang` kc ON ft.branch_id=kc.branch_id
LEFT JOIN `kimia_farma.kf_product` p ON ft.product_id = p.product_id;
