# cbse-class12-cs-project
its CS project - inventory management based on python sql connectivity 

# push-corporations-db

A Python-MySQL application for regional branch management and executive reporting.

## 🛠️ Required Software
* **Python 3.x**
* **MySQL Server**
* **`mysql-connector-python`**

## ⚙️ Database Configuration
Create a database named `Push_Corporations` and add your local credentials in the script:
```python
mydb = mysql.connector.connect(
    host='localhost', 
    user='YOUR_MYSQL_USER', 
    passwd='YOUR_MYSQL_PASSWORD', 
    database='Push_Corporations'
)
```

## 🔑 System Users & Credentials
(Note: More branches can be added by expanding the if/elif conditions in the code).

| Branch / Role | User ID | Password |
| :--- | :--- | :--- |
| **Raipur Branch** | `Push Corporate Raipur` | `Raipur_Manager` |
| **Chhattisgarh Branch** | `Push Corporate Chattisgarh` | `Chattisgarh_Manager` |
| **Delhi Branch** | `Push Corporate Delhi` | `Delhi_Manager` |
| **Senior Executive** | `Push Corporate SM` | `Manager_Senior` |



## 📊 Application Menu Flow
**1. Login Screen**
The user is prompted to enter a Login ID and Password.  

**2. Branch Manager Portal**

**Table Selection:** The manager chooses one of four tables to work on: 1. Fashion Products, 2. General Products, 3. Supply Table, or 4. Customer Table (or presses 'E' to exit).  

**Operations Menu:** After selecting a table, the manager chooses an action: Insert (I), Update (U), Delete (D), Show (S), or Back (B).  

Insert (I): Adds new records. It performs composite key validation for Fashion and General products to block duplicate rows. For Customer entries, it verifies that the corresponding Order Number already exists in the Supply Table.  

Update (U): Allows modification of specific data fields. Managers can update the Quantity or Profit for inventory products, adjust Shipment or Delivery dates in the Supply table, or change a customer's Address.  

Delete (D): Removes records from the selected inventory or supply tables after verifying they exist. Note: Customer records cannot be deleted directly; they are cleared automatically when their linked supply order is deleted. 
 
Show (S): Displays data logs. The manager can either print the entire table (W) or apply custom filtering criteria (P) on specific fields like company name, order date, or profit ranges.  

**3. Senior Executive Portal**
The executive bypasses individual tables and chooses from a centralized management menu:  

**1. Business Overview:** Generates a running 3-month operational review across all three branches. It aggregates total order counts, cumulative profits, and delivery delay percentages for each region. 
 
**2. Delayed Orders:** Prompts for a threshold number of days and utilizes SQL DATEDIFF to list all specific orders across Raipur, Chhattisgarh, and Delhi that exceeded their expected delivery timelines.  

**3. Save and Export:** Dynamically compiles corporate datasets into standalone .csv spreadsheet files. The executive can export the standard trailing 3-month performance history or define a custom YYYY-MM-DD start and end date range.  

4. Exit: Disconnects from the administrative portal.  


## 📋 Database Tables & Layout

### 1. Fashion Products Table (`fashion_pro_[suffix]`)
Tracks clothing stock entries with composite uniqueness checks on the brand identifier, category type, and size to avoid duplication flaws.
* **Fields:** `company`, `category`, `size`, `quantity`, `profit_per_item`
* **Allowed Actions:** Insert, Update (Quantity/Profit), Delete, Search (Full table or conditional)

### 2. General Products Table (`general_pro_[suffix]`)
Manages standard inventory logs containing discrete expiration dates with composite key safety.
* **Fields:** `company`, `category`, `expiry_date`, `quantity`, `profit_per_item`
* **Allowed Actions:** Insert, Update (Quantity/Profit), Delete, Search (Full table or conditional)

### 3. Supply Table (`supply_tb_[suffix]`)
Tracks distribution logistics pipelines and transactional milestones.
* **Fields:** `order_no`, `profit`, `date_order`, `expected_delivery`, `shipment`, `delivery`
* **Allowed Actions:** Create order logs, Update timelines (Shipment/Delivery dates), Delete tracking indices

### 4. Customer Table (`customer_tb_[suffix]`)
Stores profiles linked to individual client tracking. Orders cannot exist unless matching order IDs reside in the supply system.
* **Fields:** `order_no`, `name`, `contact`, `address`
* **Allowed Actions:** Add profiles, Edit addresses, View operational listings

