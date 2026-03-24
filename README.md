Process and code:
1. Setup
Download customers CSV and employees JSON files from adventureworks and put it into a folder called data.
Imports libraries (pandas, pymongo, sqlalchemy) and defines all connection credentials for MySQL and MongoDB Atlas, plus the path to customers CSV.

2. Helper Functions
get_sql_dataframe: runs a SQL query and returns a DataFrame
set_dataframe: writes a DataFrame to MySQL
get_mongo_client and get_mongo_dataframe: connects to and reads from MongoDB
set_mongo_collection: uploads a JSON file to a MongoDB collection

3. Extract, Transform, Load for each dimension
Each dimension follows the same Extract → Transform → Load → Validate pattern:
dim_products: MySQL
dim_vendors: MySQL
dim_employees: MongoDB Atlas
dim_customers: Local CSV

Fact Table (dim_fact_sales_orders):
Pulls raw sales from fact_sales_orders_vw
Replaces OrderDate, DueDate, ShipDate with surrogate date keys from dim_date
Merges in customer_key, employee_key, and product_key, drops unneeded columns, loads to dim_fact_sales_orders

4. SQL Query:
Joins dim_fact_sales_orders + dim_customers + dim_date to get top 10 customers by revenue per month.

5. Deployment:
Run the notebook top to bottom — skip Section 3 (drop/recreate DB) on reruns since it would wipe dim_date
Run Lab_02c_Create_Populate_Dim_Date.sql in MySQL Workbench first when you reach the dim_date section
