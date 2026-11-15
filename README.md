![Smart Grocery Store banner](assets/banner.svg)

# Smart Grocery Store Management System

A menu-driven Python application for managing a grocery store's products, stock, and sales, built with lists and dictionaries.

**Live demo:** https://maidaasif.github.io/Lists-and-Dictionaries/

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Type](https://img.shields.io/badge/Interface-Command%20Line-lightgrey)
![Status](https://img.shields.io/badge/Status-Complete-success)

## Table of Contents
1. [Overview](#overview)
2. [Features](#features)
3. [Live Demo](#live-demo)
4. [Getting Started](#getting-started)
5. [Usage](#usage)
6. [Data Model](#data-model)
7. [Code Structure](#code-structure)
8. [Input Validation](#input-validation)
9. [Testing](#testing)
10. [Design Decisions](#design-decisions)
11. [Limitations and Future Improvements](#limitations-and-future-improvements)
12. [Project Structure](#project-structure)
13. [Author](#author)

## Overview
A local grocery store owner needs a simple way to track products, prices, available stock, and daily sales. This application provides that through a command-line menu that keeps running until the user exits.

It stores products and sales as **lists of dictionaries**, validates every input, and prevents invalid operations such as duplicate product IDs or selling more stock than is available.

## Features

| Menu Option | Description |
|-------------|-------------|
| 1. Add New Product | Records a product (ID, name, category, price, stock) and rejects duplicate IDs |
| 2. View All Products | Lists every product with its category, price, and stock |
| 3. Search Product | Finds products by ID or by full or partial name, ignoring case |
| 4. Update Product Stock | Adds stock to a product or sets a new quantity |
| 5. Process Customer Sale | Verifies the product and stock, calculates the total, deducts stock, and records the sale |
| 6. View Sales Records | Lists all completed sales |
| 7. Generate Store Report | Summarises totals, revenue, low-stock products, and the highest and lowest priced items |
| 8. Exit | Ends the program |

## Live Demo
`index.html` is an interactive browser preview that mirrors the menu and rules of the Python program, so it can be tried without installing Python. It includes a console, live inventory and sales tables, and summary cards.

- **Online:** https://maidaasif.github.io/Lists-and-Dictionaries/
- **Offline:** download the repository and open `index.html` in any browser.

The preview is a JavaScript re-creation built for demonstration. The Python file is the actual application.

## Getting Started

### Requirements
- Python 3.8 or later (no external libraries needed)
- Git (optional, for cloning)

### Installation and Run

```bash
git clone https://github.com/MaidaAsif/Lists-and-Dictionaries.git
cd Lists-and-Dictionaries
python "Smart  Grocery Store Management System.py"
```

Use `python3` (macOS/Linux) or `py` (Windows) if `python` is not recognised. The file name contains spaces, so keep the quotes around it.

The program starts with two sample products (Milk and Bread), so every feature can be tested immediately.

## Usage

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

### Example session

```
Enter your choice: 2

--- ALL PRODUCTS ---
ID: 101 | Milk | Dairy | Rs. 250.00 | Stock: 20
ID: 102 | Bread | Bakery | Rs. 120.00 | Stock: 4

Enter your choice: 5
Product ID: 101
Purchase quantity: 3

Purchase summary: 3 x Milk @ Rs. 250.00
Total: Rs. 750.00 | Remaining stock: 17

Enter your choice: 7

===== STORE REPORT =====
Total products:      2
Total stock:         21
Sales transactions:  1
Total revenue:       Rs. 750.00
Low stock (< 5):     Bread
Highest priced:      Milk (Rs. 250.00)
Lowest priced:       Bread (Rs. 120.00)
```

### Rejected operations

```
A product with this ID already exists.
Sale rejected: only 4 units available.
Product not found.
```

## Data Model

**Product** (stored in the `products` list):

```python
{"id": 101, "name": "Milk", "category": "Dairy", "price": 250.0, "stock": 20}
```

**Sales record** (stored in the `sales` list):

```python
{"id": 101, "name": "Milk", "quantity": 3, "total": 750.0}
```

## Code Structure

![How the program works](assets/menu-flow.svg)

| Function | Responsibility |
|----------|----------------|
| `get_number(prompt, minimum, number_type)` | Reads a number, repeating until it is valid and at least the minimum |
| `get_text(prompt)` | Reads text, repeating until it is not empty |
| `find_by_id(product_id)` | Returns the matching product, or `None` |
| `show_product(product)` | Prints one product's details |
| `add_product()` | Creates a product and blocks duplicate IDs |
| `view_products()` | Displays all products |
| `search_product()` | Searches by ID or name |
| `update_stock()` | Adds stock or sets a new quantity |
| `process_sale()` | Validates, completes, and records a sale |
| `view_sales()` | Displays all sales |
| `generate_report()` | Produces the store report |
| `main()` | Runs the menu loop and dispatches to the functions above |

### Python concepts demonstrated
- Lists and dictionaries, accessed through keys and values
- `.append()`, `len()`, `sum()`, `max()`, `min()`
- `for` loops over product and sales records, and a `while` loop for the menu
- Conditional statements (`if`, `elif`, `else`)
- List comprehensions and `lambda` key functions
- A dictionary that maps menu choices to functions
- `try` / `except` for invalid input
- f-strings for formatted output

## Input Validation

| Field | Rule |
|-------|------|
| Product ID | Whole number of at least 1, unique |
| Name, category | Cannot be empty or only spaces; cleaned with `.strip()` and `.title()` |
| Price | Number greater than 0 |
| Stock, new quantity | Whole number of at least 0 |
| Quantity to add, purchase quantity | Whole number of at least 1 |
| Menu choice | Number from 1 to 8 |

Invalid input never crashes the program. It shows a message and asks again.

## Testing
Each case below was run against the program.

| # | Scenario | Expected result |
|---|----------|-----------------|
| 1 | Menu choice `9`, `abc`, or empty | "Invalid choice" message, menu shows again |
| 2 | Add ID `101` (already exists) | "A product with this ID already exists." |
| 3 | Add ID `0`, `-5`, `abc`, or `1.5` | "Invalid input", asks again |
| 4 | Name or category of only spaces | "This field cannot be empty." |
| 5 | Price `0`, `-10`, or `abc` | Rejected, asks again |
| 6 | Stock `0` when adding a product | Accepted |
| 7 | Name `  green TEA ` | Saved as `Green Tea` |
| 8 | Search `mil` or `MILK` | Finds Milk |
| 9 | Search empty, `999`, or `xyz` | "Product not found." |
| 10 | Update stock for ID `999` | "Product not found." |
| 11 | Add stock `0` or `-4` | Rejected (minimum is 1) |
| 12 | Set new quantity `0` | Accepted |
| 13 | Sale quantity `0`, `-2`, or `abc` | Rejected, asks again |
| 14 | Sell 5 Bread when stock is 4 | "Sale rejected: only 4 units available." Nothing changes |
| 15 | Sell exactly 4 Bread when stock is 4 | Accepted: Rs. 480.00, remaining stock 0 |
| 16 | Sell any Bread when stock is 0 | "Sale rejected: only 0 units available." |
| 17 | View sales before any sale | "No sales recorded yet." |
| 18 | Report with no sales | Transactions `0`, revenue `Rs. 0.00` |
| 19 | Product with stock exactly `5` | Not listed as low stock |
| 20 | Product with stock `4` or less | Listed as low stock |
| 21 | Two products share the lowest price | The first one added is shown |
| 22 | Rejected sale | Not counted in transactions or revenue |

## Design Decisions
- **List of dictionaries.** Each product's details stay together, so one product's price cannot be mixed up with another's name.
- **Checks before changes.** A sale is validated completely before stock is deducted or a record is created, so a rejected sale leaves no trace.
- **Low stock means below 5.** A product with exactly 5 units is not flagged, following the requirement "below 5 units".
- **One reusable input function.** `get_number()` handles all numeric validation, which avoids repeated code.
- **Dictionary-based menu.** Mapping choices to functions keeps `main()` short and makes adding an option a one-line change.

## Limitations and Future Improvements
- Data is held in memory only, so products and sales are lost when the program exits. Saving to a CSV or JSON file is the natural next step.
- Products cannot be edited or deleted after being added.
- Sales do not record a date or time.
- A sale covers one product at a time, with no multi-item cart.

## Project Structure

```
Lists-and-Dictionaries/
├── assets/
│   ├── banner.svg                              # README banner
│   ├── logo.svg                                # Logo and page icon
│   └── menu-flow.svg                           # Program flow diagram
├── Smart  Grocery Store Management System.py   # Python application
├── index.html                                  # Browser preview
└── README.md
```

## Author
**Maida Asif**
GitHub: [@MaidaAsif](https://github.com/MaidaAsif)
