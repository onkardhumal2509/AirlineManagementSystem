# ✈️ Airline Management System

A desktop-based Airline Management System built with **Java Swing** and **MySQL**, allowing users to manage flight bookings, passenger records, and cancellations through a simple GUI.

## Features

- **User Login** – Secure access to the system via a login screen
- **Add Passenger** – Register new passenger details (name, nationality, phone, address, Aadhar, gender)
- **Book Flight** – Search flights by source/destination and book tickets, generating a unique PNR
- **Cancel Booking** – Cancel an existing reservation using PNR
- **Flight Information** – View all available flights in a tabular format
- **Journey Details / Boarding Pass** – View reservation details and generate a boarding pass

## Tech Stack

- **Language:** Java (JDK 17+)
- **GUI:** Java Swing
- **Database:** MySQL
- **Database Connectivity:** JDBC (MySQL Connector/J)
- **Build Tool:** Apache Ant (NetBeans project)
- **Libraries Used:**
  - [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/) – JDBC driver for MySQL
  - [JCalendar](https://mvnrepository.com/artifact/com.toedter/jcalendar) – Date picker component (`JDateChooser`)
  - Custom `net.proteanit.sql.DbUtils` utility class – converts a `ResultSet` into a Swing `TableModel` (self-implemented, replacing the unmaintained `rs2xml` library)

## Prerequisites

Before running this project, make sure you have:

1. **JDK 17 or later** installed
2. **MySQL Server** installed and running
3. **NetBeans IDE** (recommended, since this is a NetBeans/Ant project) — or Apache Ant if running from the command line
4. **MySQL Connector/J** and **JCalendar** jar files (see setup steps below)

## Database Setup

Run the following SQL script to create the database and required tables:

```sql
CREATE DATABASE airlinemanagementsystem;
USE airlinemanagementsystem;

CREATE TABLE login (
    username VARCHAR(50),
    password VARCHAR(50)
);

CREATE TABLE passenger (
    name VARCHAR(100),
    nationality VARCHAR(50),
    phone VARCHAR(20),
    address VARCHAR(200),
    aadhar VARCHAR(20),
    gender VARCHAR(10)
);

CREATE TABLE flight (
    f_name VARCHAR(50),
    f_code VARCHAR(20),
    source VARCHAR(50),
    destination VARCHAR(50)
);

CREATE TABLE reservation (
    PNR VARCHAR(20),
    ticket_no VARCHAR(20),
    aadhar VARCHAR(20),
    name VARCHAR(100),
    nationality VARCHAR(50),
    flightname VARCHAR(50),
    flightcode VARCHAR(20),
    src VARCHAR(50),
    des VARCHAR(50),
    ddate VARCHAR(20)
);

CREATE TABLE cancel (
    PNR VARCHAR(20),
    name VARCHAR(100),
    cancelno VARCHAR(20),
    flightcode VARCHAR(20),
    ddate VARCHAR(20)
);

-- Seed data
INSERT INTO login VALUES ('admin', 'admin');
INSERT INTO flight VALUES ('Air India', 'AI-101', 'Pune', 'Delhi');
INSERT INTO flight VALUES ('IndiGo', '6E-202', 'Mumbai', 'Bangalore');
```

## Project Setup (NetBeans)

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/AirlineManagementSystem.git
   ```
2. Open the inner `AirlineManagementSystem` folder (the one containing `nbproject`, `src`, and `build.xml`) in NetBeans via **File → Open Project**.
3. Download the required libraries:
   - [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)
   - [JCalendar 1.4](https://repo1.maven.org/maven2/com/toedter/jcalendar/1.4/jcalendar-1.4.jar)
4. Add both jars to the project: right-click project → **Properties → Libraries → Compile** tab → **Add JAR/Folder**.
5. Update the database credentials in `src/airlinemanagementsystem/Conn.java` with your own MySQL username/password:
   ```java
   c = DriverManager.getConnection("jdbc:mysql:///airlinemanagementsystem", "root", "your_password");
   ```
6. **Clean and Build**, then **Run** the project.
7. Log in using the seed credentials:
   - **Username:** `admin`
   - **Password:** `admin`

## Screenshots

*(Add screenshots of the Login screen, Flight Booking screen, etc. here)*

## Known Limitations

- Passwords are stored and checked in plain text (not production-safe — for learning/demo purposes only)
- No input validation on forms
- No foreign key relationships between tables (flat schema)
- Desktop GUI only — no REST API or web interface

## Acknowledgements

Base project structure adapted from an open-source NetBeans/MySQL tutorial project, with dependency and build fixes applied to run on modern JDK/MySQL versions.

## License

This project is for educational purposes.
