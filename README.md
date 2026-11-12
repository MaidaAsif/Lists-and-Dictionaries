# Smart Grocery Store Management System

## Overview
A menu-driven Python application that helps a grocery store owner manage products, stock, and sales. It uses a **list of dictionaries** to store products and a separate **list of dictionaries** to record completed sales. The program keeps running until the user chooses to exit.

## Features

| Menu Option | Description |
|-------------|-------------|
| 1. Add New Product | Adds a product (ID, name, category, price, stock) and rejects duplicate IDs |
| 2. View All Products | Lists every product with its category, price, and stock |
| 3. Search Product | Finds a product by ID or by name (partial names work) |
| 4. Update Product Stock | Adds stock or sets a new quantity for a product |
| 5. Process Customer Sale | Checks the product and stock, calculates the total, deducts stock, and records the sale |
| 6. View Sales Records | Lists all completed sales |
| 7. Generate Store Report | Shows totals, low-stock products, and the highest and lowest priced products |
| 8. Exit | Closes the program |

## Data Structures

**Product (dictionary):**

```python
{"id": 101, "name": "Milk", "category": "Dairy", "price": 250.0, "stock": 20}
```

**Sales record (dictionary):**

```python
{"id": 101, "name": "Milk", "quantity": 3, "total": 750.0}
```

Products are stored in the `products` list and sales in the `sales` list.

## Custom Functions

| Function | Purpose |
|----------|---------|
| `get_number(prompt, minimum, number_type)` | Asks until a valid number is entered |
| `get_text(prompt)` | Asks until a non-empty text value is entered |
| `find_by_id(product_id)` | Returns the product with the given ID, or `None` |
| `show_product(product)` | Prints the details of one product |
| `add_product()` | Adds a new product and prevents duplicate IDs |
| `view_products()` | Displays all products |
| `search_product()` | Searches by ID or name |
| `update_stock()` | Adds stock or sets a new quantity |
| `process_sale()` | Validates and records a customer sale |
| `view_sales()` | Displays all sales records |
| `generate_report()` | Displays the store report |
| `main()` | Runs the menu loop |

## Python Concepts Used
- Lists and dictionaries, with keys and values to access data
- `.append()` to add products and sales
- `for` loops to process product and sales records
- `while` loop for the menu
- Conditional statements: `if`, `elif`, `else`
- List comprehensions, `max()`, `min()`, `sum()`, and `len()`
- A dictionary of functions to map menu choices to actions
- `try` / `except` for invalid input
- f-strings for formatted output

## How to Run

**Requirements:** Python 3.8 or later.

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
python smart_grocery_store.py
```

Use `python3` or `py` if `python` is not recognized.

The program starts with two sample products (Milk and Bread), so you can test every option immediately.

## Sample Execution

### Menu

```
====================================
SMART GROCERY STORE SYSTEM
====================================
1. Add New Product
2. View All Products
3. Search Product
4. Update Product Stock
5. Process Customer Sale
6. View Sales Records
7. Generate Store Report
8. Exit

Enter your choice:
```

### View all products (option 2)

```
--- ALL PRODUCTS ---
ID: 101 | Milk | Dairy | Rs. 250.00 | Stock: 20
ID: 102 | Bread | Bakery | Rs. 120.00 | Stock: 4
```

### Add a product (option 1)

```
Product ID: 103
Product name: rice
Category: grains
Price (Rs.): 180
Available stock: 50
Product added successfully.
```

Entering an existing ID, such as 101, gives:

```
A product with this ID already exists.
```

### Search a product (option 3)

```
Enter product name or ID: milk
ID: 101 | Milk | Dairy | Rs. 250.00 | Stock: 20
```

A name or ID that does not exist gives:

```
Product not found.
```

### Update stock (option 4)

```
Product ID: 102
1. Add stock  2. Set new quantity: 1
Quantity to add: 10
Updated stock of Bread: 14
```

### Process a sale (option 5)

```
Product ID: 101
Purchase quantity: 3

Purchase summary: 3 x Milk @ Rs. 250.00
Total: Rs. 750.00 | Remaining stock: 17
```

A quantity larger than the stock is rejected, for example 10 units of Bread when 4 are available:

```
Sale rejected: only 4 units available.
```

### View sales records (option 6)

```
--- SALES RECORDS ---
ID: 101 | Milk | Qty: 3 | Total: Rs. 750.00
```

### Store report (option 7)

After the sale above, starting from the original sample data:

```
===== STORE REPORT =====
Total products:      2
Total stock:         21
Sales transactions:  1
Total revenue:       Rs. 750.00
Low stock (< 5):     Bread
Highest priced:      Milk (Rs. 250.00)
Lowest priced:       Bread (Rs. 120.00)
```

## Input Validation
- Product ID, stock, and quantities must be whole numbers
- Price must be a number greater than zero
- Product ID must be unique
- Name and category cannot be empty
- Sales are rejected if the product does not exist or the stock is insufficient
- Invalid menu choices and invalid numbers prompt the user to try again

## Note
Data is stored in memory only. Products added and sales made during a session are lost when the program exits, and the program starts again with the two sample products.

## Project Structure

```
YOUR-REPOSITORY/
├── smart_grocery_store.py
└── README.md
```

## Author
Maida Asif
