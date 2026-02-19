# Overview

As a software engineer, I'm working to strengthen my understanding of relational databases and how to integrate them with application code. One of the most important skills in backend and full-stack development is knowing how to design a proper database schema, write efficient SQL queries, and connect that data layer to a program users can actually interact with. This project was my hands-on way of building that foundation.

I built **Simple Inventory** — a command-line application written in Python that uses SQLite to manage product stock for a small business. The app lets you add and remove products, update stock quantities and prices, view the full inventory, and generate a value report showing how much your total stock is worth. To use it, simply run `python inventory.py` in your terminal and navigate the menu by entering the number for the option you want.

My purpose in writing this software was to move beyond just reading about SQL and actually apply it — designing a two-table schema with a real foreign key relationship, writing JOIN queries to combine data across tables, and using aggregate functions like SUM and COUNT to produce meaningful reports. Building something practical made those concepts stick in a way that reading alone never would.

[Software Demo Video](https://youtu.be/-KO8U6Itl8A)

# Relational Database

This project uses **SQLite**, a lightweight, file-based relational database that is built into Python's standard library. All data is stored in a single file called `inventory.db` which is created automatically when the program runs for the first time. Because SQLite is file-based, no database server setup is required, making it ideal for a self-contained desktop application like this one.

The database contains two tables:

**categories**
| Column | Type | Constraints |
|--------|------|-------------|
| id | INTEGER | PRIMARY KEY, AUTOINCREMENT |
| name | TEXT | NOT NULL, UNIQUE |

**products**
| Column | Type | Constraints |
|--------|------|-------------|
| id | INTEGER | PRIMARY KEY, AUTOINCREMENT |
| name | TEXT | NOT NULL, UNIQUE |
| category_id | INTEGER | NOT NULL, FOREIGN KEY → categories(id) |
| price | REAL | NOT NULL, CHECK >= 0 |
| quantity | INTEGER | NOT NULL, DEFAULT 0, CHECK >= 0 |

The `category_id` column in `products` is a foreign key that references the `categories` table. This enforces referential integrity — a product cannot be assigned to a category that doesn't exist, and a category cannot be deleted while products are still assigned to it. Foreign key enforcement is activated at runtime using `PRAGMA foreign_keys = ON`.

# Development Environment

- **Editor:** Visual Studio Code
- **Terminal:** Built-in VS Code terminal
- **Version Control:** Git + GitHub
- **Database Viewer:** DB Browser for SQLite (used during development to inspect the .db file)

The application is written in **Python 3.10+**. The only library used is `sqlite3`, which is part of Python's standard library — no external packages need to be installed.

# Useful Websites

- [SQLite Official Documentation](https://www.sqlite.org/docs.html)
- [Python sqlite3 Module Docs](https://docs.python.org/3/library/sqlite3.html)
- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)
- [DB Browser for SQLite](https://sqlitebrowser.org/)
- [Real Python – Introduction to Python SQL Libraries](https://realpython.com/python-sql-libraries/)

# Future Work

- Add a search feature so users can look up a product by name without scrolling through the full inventory list
- Add the ability to edit a product's name or reassign it to a different category
- Export the value report to a CSV file so it can be opened in a spreadsheet for further analysis
