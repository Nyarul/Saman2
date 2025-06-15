🚌 Transport Management System 🚗

📚 Overview
The Transport Management System (TMS) is a comprehensive solution designed to manage traffic violations, vehicle details, and user data. It tracks summonses issued, payment statuses, and violation details through a robust database system, ensuring efficient monitoring and management.

🗃️ Database Overview
Database: umt_transport_db
The umt_transport_db database stores all critical information for the Transport Management System. Below are the table structures that define how data is organized.

Tables in the Database:
summons Table
Column	Type	Description
id	int(11)	Unique identifier for each summons (Primary Key).
vehicle_id	int(11)	ID of the vehicle involved in the violation.
issued_by	int(11)	ID of the officer or entity issuing the summons.
violation_type	varchar(100)	Type of violation (e.g., speeding, illegal parking).
location	varchar(100)	Location where the violation occurred.
amount	decimal(8,2)	Fine amount for the violation.
status	enum('issued', 'paid', 'appealed')	Status of the summons (default is 'issued').
issued_at	timestamp	Timestamp when the summons was issued.
paid_at	timestamp NULL	Timestamp when the summons was paid. (NULL if unpaid).

sql
Copy
Edit
CREATE TABLE `summons` (
  `id` int(11) NOT NULL,
  `vehicle_id` int(11) NOT NULL,
  `issued_by` int(11) NOT NULL,
  `violation_type` varchar(100) NOT NULL,
  `location` varchar(100) NOT NULL,
  `amount` decimal(8,2) NOT NULL,
  `status` enum('issued', 'paid', 'appealed') DEFAULT 'issued',
  `issued_at` timestamp NOT NULL DEFAULT current_timestamp(),
  `paid_at` timestamp NULL DEFAULT NULL
);
users Table
Column	Type	Description
id	int(11)	Unique identifier for each user (Primary Key).
matric_no	varchar(20)	Matriculation number for students or ID for staff members.
staff_id	varchar(20)	Staff ID (for staff users).
role	enum('student', 'staff')	Role of the user, either 'student' or 'staff'.
password	varchar(255)	Hashed password for user authentication.
full_name	varchar(100)	Full name of the user.
email	varchar(100)	User's email address.
phone	varchar(20)	Contact phone number.
created_at	timestamp	Timestamp when the user was created.

sql
Copy
Edit
CREATE TABLE `users` (
  `id` int(11) NOT NULL,
  `matric_no` varchar(20) DEFAULT NULL,
  `staff_id` varchar(20) DEFAULT NULL,
  `role` enum('student', 'staff') DEFAULT NULL,
  `password` varchar(255) NOT NULL,
  `full_name` varchar(100) NOT NULL,
  `email` varchar(100) NOT NULL,
  `phone` varchar(20) DEFAULT NULL,
  `created_at` timestamp NOT NULL DEFAULT current_timestamp()
);
vehicles Table
Column	Type	Description
id	int(11)	Unique identifier for each vehicle (Primary Key).
user_id	int(11)	ID of the user who owns or operates the vehicle.
plate_number	varchar(20)	Vehicle plate number.
model	varchar(50)	Vehicle model.
created_at	timestamp	Timestamp when the vehicle was registered in the system.

sql
Copy
Edit
CREATE TABLE `vehicles` (
  `id` int(11) NOT NULL,
  `user_id` int(11) NOT NULL,
  `plate_number` varchar(20) NOT NULL,
  `model` varchar(50) DEFAULT NULL,
  `created_at` timestamp NOT NULL DEFAULT current_timestamp()
);
🏗️ Project Structure
The project is structured to facilitate development and management:

build/: Contains build-related files and compiled artifacts.

nbproject/: Project files for NetBeans IDE.

src/: Source code files for the system.

test/: Test files for the system's functionalities.

web/: Frontend files for the web-based user interface.

build.xml: Build configuration file.

🔧 Installation
To set up the system on your local machine, follow these steps:

Clone the repository (if applicable).

Install dependencies for the web application and backend (specific instructions can be added here depending on the tech stack used).

Set up the database by importing the SQL dump (umt_transport_db.sql) into your MariaDB or MySQL instance.

bash
Copy
Edit
mysql -u username -p < /path/to/umt_transport_db.sql
Configure your application settings, such as database credentials in configuration files.

Run the application by using the appropriate command for your environment (e.g., npm start, php artisan serve).

🎮 Usage
Once the system is running, you can:

View and manage traffic summonses: Add, update, and view summonses for vehicles.

Track payments: Update the status of a summons when a fine is paid.

Appeal process: Change the status of a summons if a violation is contested.

🤝 Contributing
We welcome contributions! To contribute:

Fork the repository.

Create a new feature branch.

Implement your changes.

Submit a pull request for review.

📝 License
This project is licensed under the MIT License. See the LICENSE file for more information.
