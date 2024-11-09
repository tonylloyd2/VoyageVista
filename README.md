# VoyageVista

```markdown
# 

This project is a Trip Agency Management System designed to help travel agencies manage their trip offerings and bookings efficiently. It includes a user-facing interface for browsing and booking trips and an administrative interface for managing listings, tracking bookings, and generating reports.

## Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Database Setup](#database-setup)
- [Sales Prediction Model](#sales-prediction-model)
- [License](#license)

## Project Overview
The Trip Agency Management System allows users to browse, search, and book trips or tours by destination, duration, price, and activity type. Administrators can manage trip listings, set availability, update pricing, and generate reports. Additionally, the project includes a machine learning model for sales prediction based on advertising costs.

## Features
- **User Interface**: Users can browse, search, and view trip details.
- **Booking System**: Online booking, including date selection and traveler information.
- **Admin Interface**: Manage trips, pricing, availability, and generate booking reports.
- **Sales Prediction**: Forecast revenue based on advertising costs using a machine learning model with Weka.

## Technologies Used
- **Java EE**: Servlets, JSP, and JDBC.
- **Database**: MariaDB (or MySQL).
- **Machine Learning**: Weka library for Java, integrated with the application.
- **Server**: Apache Tomcat 9 or higher.

## Requirements
- **Java**: OpenJDK 11 or higher
- **Apache Tomcat**: Version 9 or 11
- **MariaDB**: Version 11.4 or compatible MySQL server
- **Weka Library**: Integrated with the application for sales prediction

## Installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/your-username/trip-agency-management-system.git
cd trip-agency-management-system
```

### Step 2: Install Dependencies
Ensure that all required packages are installed. This includes:
- Java
- Apache Tomcat
- MariaDB

### Step 3: Set Up Tomcat
1. Extract and install Tomcat to `/opt/tomcat`.
2. Make sure the `bin` scripts are executable:
   ```bash
   sudo chmod +x /opt/tomcat/apache-tomcat-9.0.34/bin/*.sh
   ```

### Step 4: Set Up Environment Variables
Set the `JAVA_HOME`, `CATALINA_HOME`, and `CATALINA_PID` in your Tomcat service configuration (`/etc/systemd/system/tomcat.service`).

## Configuration

### Database Configuration
1. **Start MariaDB**:
   ```bash
   sudo systemctl start mariadb
   ```

2. **Secure MariaDB**:
   If `mysql_secure_installation` is unavailable, run the following commands manually in the MariaDB shell:
   ```sql
   ALTER USER 'root'@'localhost' IDENTIFIED BY 'your_password';
   DELETE FROM mysql.user WHERE User='';
   FLUSH PRIVILEGES;
   ```

3. **Create Database and Tables**:
   - Access MariaDB:
     ```bash
     sudo mysql -u root -p
     ```
   - Run the following to set up the database:
     ```sql
     CREATE DATABASE trip_agency;
     USE trip_agency;

     CREATE TABLE trips (
         id INT PRIMARY KEY AUTO_INCREMENT,
         destination VARCHAR(255),
         duration INT,
         price DECIMAL(10, 2),
         activity_type VARCHAR(255),
         description TEXT
     );

     CREATE TABLE bookings (
         id INT PRIMARY KEY AUTO_INCREMENT,
         trip_id INT,
         booking_date DATE,
         participants INT,
         customer_name VARCHAR(255),
         customer_email VARCHAR(255),
         FOREIGN KEY (trip_id) REFERENCES trips(id)
     );
     ```

### Sales Prediction Model Setup
1. Ensure Weka is included in the project dependencies.
2. Load the provided dataset for training the regression model to predict revenue based on advertising costs.

## Running the Application

### Start Tomcat
```bash
sudo systemctl start tomcat
```

### Access the Application
- **User Interface**: `http://localhost:8080/trip-agency-management-system`
- **Admin Interface**: `http://localhost:8080/trip-agency-management-system/admin`

## Database Setup
1. Connect to MariaDB and initialize the database using the SQL commands provided in the [Database Configuration](#database-configuration) section.
2. Use prepared SQL queries to fetch and update trip and booking data.

## Sales Prediction Model
The sales prediction model uses the Weka library to train a regression model based on historical advertising costs and revenue data. To update predictions:
1. Increase advertising cost by 10% for future predictions.
2. Use Weka’s `LinearRegression` model or equivalent in Java to output forecasted revenue.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
```

This `README.md` provides a comprehensive guide to installing, configuring, and using your project. Adjust paths and URLs as needed for your setup. Let me know if you need any other sections or specific details!
