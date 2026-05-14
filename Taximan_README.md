# Taximan 🚕

A cab booking application built with Python and MySQL, demonstrating relational database design, SQL query optimization, transaction management, and trigger-based automation. Built to simulate a real-world ride-hailing backend.

---

## What it does

Taximan models the core database layer of a cab booking platform — covering everything from user registration and ride requests to driver assignment, billing, and audit logging. The project focuses on **data integrity, transaction safety, and SQL fluency** rather than UI.

Key operations supported:
- Register riders and drivers
- Request and assign cab bookings
- Track ride status from request → in-progress → completed
- Calculate fares and generate billing records
- Enforce business rules via SQL triggers

---

## Features

- **Relational schema design** — normalized tables with foreign keys, constraints, and indexes
- **Transaction management** — ACID-compliant transactions for booking and payment flows
- **SQL triggers** — automated actions on insert/update events (e.g. auto-logging cancellations, updating driver availability)
- **10 analytical SQL queries** — covering aggregations, joins, subqueries, and window functions
- **Python connector layer** — `Connector.py` abstracts the MySQL connection; `Database transactions.py` handles booking logic

---

## Tech stack

| Component | Technology |
|---|---|
| Database | MySQL |
| Application layer | Python 3 |
| DB connector | `mysql-connector-python` |
| Schema design | ER diagram (included) |

---

## Project structure

```
Taximan/
├── cab_app/                    # Core application modules
├── Connector.py                # MySQL connection handler
├── Database transactions.py    # Booking & payment transaction logic
├── 10SQLQueries.sql            # Analytical queries on the dataset
├── Triggers.txt                # SQL trigger definitions
├── Relationship Schema.pdf     # Entity-relationship diagram
├── Transactions.pdf            # Transaction flow documentation
└── User Guide.pdf              # Setup and usage instructions
```

---

## How to run

**Prerequisites:** MySQL 8.0+, Python 3.8+

```bash
git clone https://github.com/arjunmoitra/Taximan.git
cd Taximan

# Install dependency
pip install mysql-connector-python

# Set up the database
# 1. Open MySQL and create a database named 'taximan'
# 2. Import the schema (see Relationship Schema.pdf for the ER diagram)

# Configure your credentials in Connector.py
# host, user, password, database

# Run the application
python "Database transactions.py"
```

---

## Sample SQL — analytical queries

```sql
-- Top 5 drivers by completed rides
SELECT driver_id, COUNT(*) AS completed_rides
FROM bookings
WHERE status = 'completed'
GROUP BY driver_id
ORDER BY completed_rides DESC
LIMIT 5;

-- Average fare by pickup zone
SELECT pickup_zone, ROUND(AVG(fare), 2) AS avg_fare
FROM rides
GROUP BY pickup_zone
ORDER BY avg_fare DESC;
```

Full query set in `10SQLQueries.sql`.

---

## Database design highlights

- **Triggers** handle side effects cleanly — e.g. when a booking is cancelled, a trigger automatically logs the event and resets driver availability without application-level code
- **Transactions** wrap multi-step operations (book → assign driver → deduct balance) so partial failures roll back completely
- Schema follows **3NF normalization** to eliminate redundancy

---

## What I learned

- Designing a **normalized relational schema** from real-world requirements
- Writing **stored triggers** to enforce business rules at the database level
- Managing **multi-step transactions** with proper rollback handling in Python
- Crafting **analytical SQL** with joins, subqueries, aggregations, and window functions

---

*Built by [Arjun Moitra](https://github.com/arjunmoitra)*
