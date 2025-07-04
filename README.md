Postgres describe table:
------------------------
SELECT column_name, column_default, data_type 
FROM INFORMATION_SCHEMA.COLUMNS 
WHERE table_name = 'super_table';

Create sequence:
----------------
-- Подгатавливаем столбец к трансформации в serial  
CREATE SEQUENCE products_id_seq OWNED BY products.id;  

-- Устанавливаем автоинкремент для столбца по последовательности  
ALTER TABLE products ALTER COLUMN id SET DEFAULT nextval('products_id_seq');  

-- Настраиваем начальное значение последовательности  
SELECT setval('products_id_seq', COALESCE(MAX(id), 0) + 1) FROM products;  

----------------------------------
Set sequence:
-------------
alter table products
  alter id set not null,
  alter id set default nextval('products_id_seq');
