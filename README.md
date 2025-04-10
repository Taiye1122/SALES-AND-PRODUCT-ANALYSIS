# SALES AND PRODUCT CATEGORY ANALYSIS


### 🧠 **Objective**
The primary goal of this project is to clean, organize, and analyze the sales data and product information to extract valuable insights such as sales trends, revenue drivers, and product performance by category and supplier.

---

### 🗃️ **Datasets Involved**
1. **`product_order`** – Contains information about product IDs, categories, prices, suppliers, and other attributes.
2. **`product_category`** – Provides the category names and IDs for each product category.
3. **`sales_order`** – Holds transactional sales data including quantities sold, pricing, and delivery dates.

---

### 🧹 **Data Cleaning and Preprocessing**
- **Column Renaming**: Fixed encoding issues (e.g., `ï»¿PRODUCTID` to `PRODUCTID`).
- **Column Removal**: Removed irrelevant columns like timestamps, currency, and unit details.
- **Date Formatting**: Reformatted and cleaned up delivery dates, removing default/fake dates like `'2999-12-12'`.
- **Duplicate Checks**: Ensured uniqueness of records by checking and counting duplicates across tables.
- **Null and Blank Filtering**: Checked for null or empty fields across important columns.

---

### 🔗 **Data Joins**
- Joined the `product_order` table with the `product_category` table via `PRODCATEGORYID`.
- Linked sales data (`sales_order`) to product details using `PRODUCTID`.

---

### 📈 **Key Analyses & Business Insights**

#### ✅ Product Overview
- **Total Number of Products by Category**: Grouped products to see distribution across categories.
- **Top 5 Most Expensive Product Categories**: Identified using `MAX(PRICE)`.

#### 💰 Sales Performance
- **Total Sales by Category (Gross)**: Aggregated `GROSSAMOUNT` per category to see which category sells the most.
- **Revenue Contribution by Product**: Highlighted top-performing products based on `NETAMOUNT`.
- **Sales Order Revenue**: Calculated the total gross revenue per sales order ID.

#### 📦 Category & Supplier Analysis
- **Products in 'Mountain Bike' Category**: Filtered to view all relevant products.
- **Highest Quantity Sold by Category**: Revealed the most popular category in terms of volume.
- **Top 5 Suppliers by Gross Sales**: Ranked based on total gross sales value.
- **Revenue from 'Mountain Bike' and 'BMX'**: Focused on niche product lines to gauge their financial performance.

#### Data Visualisation


### 📌 **Tools Used**
- SQL for data manipulation and analysis.
- Power BI For Data Visualization

---

### ✅ **Next Steps / Recommendations**
- **Visualization**: Import the clean and joined dataset into Power BI or Tableau for dashboards.
- **Time Series Analysis**: Explore delivery or order dates (after cleanup) for trends over time.
- **Customer Segmentation** *(if data is available)*: Analyze purchases by customer behavior.
- **Product Lifecycle Insight**: Cross-match with inventory or stock-in data (if accessible).

