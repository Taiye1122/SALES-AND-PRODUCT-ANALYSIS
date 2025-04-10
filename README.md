
# 🛒 **Sales and Product Category Analysis**

### 🧠 **Objective**
The goal of this project is to **clean**, **organize**, and **analyze** sales and product-related data to uncover valuable business insights. These include **sales trends**, **revenue contributors**, and **product performance** across various categories and suppliers.

---

### 🗃️ **Datasets Used**
1. **`product_order`** – Contains product IDs, category affiliations, prices, and supplier details.
2. **`product_category`** – Maps product categories to their respective names and identifiers.
3. **`sales_order`** – Sales transaction data, including quantities, delivery dates, and monetary values.

---

### 🧹 **Data Cleaning & Preprocessing**
Key steps taken to prepare the data:

- **Column Renaming**: Corrected encoding issues (e.g., `ï»¿PRODUCTID` to `PRODUCTID`):
  ```sql
  alter table product_order
  change ï»¿PRODUCTID PRODUCTID text;
  ```

- **Removing Irrelevant Fields**: Dropped columns not useful for analysis:
  ```sql
  alter table product_order
  drop column CREATEDAT,
  drop column CHANGEDAT,
  drop column TYPECODE,
  drop column CREATEDBY;
  ```

- **Date Cleansing**: Removed placeholder dates like `'2999-12-12'`:
  ```sql
  Delete from sales_order
  where DELIVERYDATE = '2999-12-12';
  ```

- **Duplicate Checks**: Ensured unique category and product records:
  ```sql
  select count(*) as count_of_duplicates, PRODCATEGORYID
  from product_category
  group by PRODCATEGORYID
  having count(*) > 1;
  ```

- **Null/Blank Validation**:
  ```sql
  select *
  from product_order
  where '*' is null and '*' = ' ';
  ```

---

### 🔗 **Data Integration**
Combined data across the three tables using SQL joins:
```sql
select *
from product_order
left join product_category
  on product_order.PRODCATEGORYID = product_category.PRODCATEGORYID
right join sales_order
  on product_order.PRODUCTID = sales_order.PRODUCTID;
```

---

### 📈 **Key Analyses & Insights**

#### ✅ **Product Overview**
- **Product Count by Category**:
  ```sql
  select count(PRODUCTID) as Num_of_Products, Product_category_name
  from product_order 
  left join product_category
  on product_order.PRODCATEGORYID = product_category.PRODCATEGORYID
  group by Product_category_name;
  ```

- **Top 5 Most Expensive Categories**:
  ```sql
  select max(PRICE) as Price, Product_category_name
  from product_order 
  left join product_category
  on product_order.PRODCATEGORYID = product_category.PRODCATEGORYID
  group by Product_category_name
  order by Price desc
  limit 5;
  ```

#### 💰 **Sales Performance**
- **Gross Sales by Category**:
  ```sql
  select sum(GROSSAMOUNT) as Total_sales_amount, Product_category_name
  from product_order
  left join product_category
  on product_order.PRODCATEGORYID = product_category.PRODCATEGORYID
  right join sales_order
  on product_order.PRODUCTID = sales_order.PRODUCTID
  group by Product_category_name
  order by Total_sales_amount desc;
  ```

- **Top Revenue-Generating Products**:
  ```sql
  select sum(NETAMOUNT) as Most_revenue, PRODUCTID
  from sales_order
  group by PRODUCTID
  order by Most_revenue desc
  limit 1;
  ```

- **Revenue per Sales Order**:
  ```sql
  select sum(GROSSAMOUNT) as Total_Gross_Amount, SALESORDERID
  from sales_order
  group by SALESORDERID;
  ```

#### 📦 **Category & Supplier Breakdown**
- **Products in the 'Mountain Bike' Category**:
  ```sql
  select PRODUCTID
  from product_order 
  left join product_category
  on product_order.PRODCATEGORYID = product_category.PRODCATEGORYID
  where Product_category_name = 'Mountain Bike';
  ```

- **Category with Highest Quantity Sold**:
  ```sql
  select sum(QUANTITY) as Count, Product_category_name
  from product_order
  left join product_category
  on product_order.PRODCATEGORYID = product_category.PRODCATEGORYID
  right join sales_order
  on product_order.PRODUCTID = sales_order.PRODUCTID
  group by Product_category_name
  order by Count desc
  limit 1;
  ```

- **Top 5 Suppliers by Gross Sales**:
  ```sql
  select sum(GROSSAMOUNT) as Gross_Amount, SUPPLIER_PARTNERID
  from product_order
  left join product_category
  on product_order.PRODCATEGORYID = product_category.PRODCATEGORYID
  right join sales_order
  on product_order.PRODUCTID = sales_order.PRODUCTID
  group by SUPPLIER_PARTNERID
  order by Gross_Amount desc
  limit 5;
  ```

- **Revenue from 'Mountain Bike' and 'BMX' Categories**:
  ```sql
  select round(SUM(NETAMOUNT), 0) as Total_Revenue, Product_category_name
  from product_order
  left join product_category
  on product_order.PRODCATEGORYID = product_category.PRODCATEGORYID
  right join sales_order
  on product_order.PRODUCTID = sales_order.PRODUCTID
  group by Product_category_name
  having Product_category_name IN ('Mountain Bike', 'BMX');
  ```

---

### 📊 **Data Visualization**
All cleaned and joined data were imported into **Power BI** for visual representation.

**Sample Dashboard Screenshot:**

![Power BI Screenshot](https://github.com/user-attachments/assets/4c2b2558-c452-4063-8863-e926e72fac49)

---

### 🛠 **Tools Used**
- **SQL** – For data cleaning, joining, and analysis.
- **Power BI** – For interactive data visualization and reporting.

---

### ✅ **Recommendations**
- Invest more in **top-performing product categories** like *Mountain Bikes* to boost sales.
- **Monitor suppliers** closely—those with higher gross sales could be strategic partners.
- Consider **discounting or bundling** lower-selling categories to optimize inventory.
- Use **historical delivery trends** to predict and prepare for peak seasons.

## Thank you 😄
