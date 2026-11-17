# Bus-ticket-reservation-system
A MySQL-based database project that manages bus details, passenger information, seat availability, reservations, ticket records, and cancellations using SQL queries and database concepts.
Bus Reservation System.

**Description**
The Bus Reservation System is a MySQL database project that organizes bus journey details, passenger information, reservations, tickets, and cancellations.

**Objectives**
- Store bus, route, journey-date, fare, and seat-availability details.
- Maintain passenger information.
- Record reservations and ticket/seat details.
- Maintain cancellation and refund records.
- Retrieve booking and business information using SQL queries, views, and functions.
- 
**Modules**
1. Bus management
2. Passenger management
3. Reservation management
4. Ticket management
5. Cancellation management
6. SQL reports and functions
   
**Technologies**
- MySQL 8+
- SQL
- MySQL Workbench / MySQL Command Line Client
Database
bus_reservation_db
**Tables**
Table	Purpose	Important fields used in queries
bus	Bus and journey details	bid, bname, source, dest, jdate, cost, total_seats, aval
passenger	Passenger details	pno, pname, age, gender, email, phone
reservation	Booking records	rno, pno, bid, amt, seats_booked, status
ticket	Ticket and seat details	tid, rno, seat_no, status
cancellation	Cancellation and refund details	cno, rno, refund_amount, reason


**Relationships**
- One passenger can make multiple reservations.
- One bus can be referenced by multiple reservations.
- Ticket records refer to reservations.
- Cancellation records refer to reservations.
SQL Concepts
SELECT, WHERE, DISTINCT, ORDER BY, LIMIT, OFFSET, LIKE, BETWEEN, IN, NOT IN, NULL checks, logical operators, string/numeric/date functions, aggregate functions, GROUP BY, HAVING, joins, subqueries, EXISTS, NOT EXISTS, CASE, COALESCE, UNION, UNION ALL, DDL, DML, transactions, views, and user-defined stored functions.

**Scope restriction**: This project version intentionally excludes indexes, triggers, stored procedures, and related queries. Stored functions are included.

**Folder Structure**
bus-reservation-system/
├── database/
│   ├── 01_create_database.sql
│   ├── 02_create_tables.sql
│   ├── 03_insert_data.sql
│   ├── 04_queries.sql
│   ├── 05_views.sql
│   └── 07_functions.sql
├── documentation/
│   ├── PROJECT_DOCUMENTATION.md
│   └── ER_DIAGRAM.md
└── README.md

**Installation and Execution**
1. Install MySQL 8+.
2. Open MySQL Workbench or the command-line client.
3. Run the SQL files in this order:
   1. 01_create_database.sql
   2. 02_create_tables.sql
   3. 03_insert_data.sql
   4. 04_queries.sql
   5. 05_views.sql
   6. 07_functions.sql
4. Execute query examples and inspect the results.
   
**Command-line example:**
mysql -u your_username -p < 01_create_database.sql
Replace your_username with your MySQL username. Repeat for each file. In Workbench, open each script and execute it in the same order.
Example Queries
select bid, bname, source, dest, jdate, cost, aval
from bus
where source = 'Hyderabad';
select p.pname, r.rno, r.amt, r.status
from passenger p
join reservation r on p.pno = r.pno;
update bus b
left join (
    select bid, sum(seats_booked) booked
    from reservation
    where status = 'BOOKED'
    group by bid
) r on b.bid = r.bid
set b.aval = b.total_seats - coalesce(r.booked, 0)
where b.bid > 0;
Notes
- The refund function demonstrates 90% refund at least 24 hours before departure, 50% for 6 to less than 24 hours, and 0% for less than 6 hours. This is a sample project rule.
- The discounted-fare function demonstrates a 10% discount.
- The seat update assumes positive bus IDs and uses bid in the WHERE clause to comply with MySQL Safe Update Mode.
- For exact data types and constraints, refer to 02_create_tables.sql.
Future Enhancements
- Web/mobile interface and authentication.
- Online payment integration.
- Booking confirmation notifications.
- Live bus tracking.
- Reporting dashboards for routes, bookings, and revenue.
Author
Developed as a DBMS / MySQL learning project.
