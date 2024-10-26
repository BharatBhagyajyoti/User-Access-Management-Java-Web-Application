User Access Management System
-----------------------------
Project Overview
----------------
The User Access Management System is a web application designed to manage user access to software applications within an organization. It allows employees to sign up, request software access, and enables managers and admins to approve or reject these requests. Built with Java Servlets, JSP, JDBC, and Oracle SQL, this application follows an MVC architecture and is managed by Maven.

Features
---------
- User Registration and Authentication: New users can sign up, log in, and create a basic account with an "Employee" role.
- Role-Based Access: Employees can request access, Managers can approve or reject requests, and Admins can manage applications.
- Software Management: Admins can add and update available software applications.
- Request Tracking: Managers can track and process access requests efficiently.

Technologies Used
------------------
Frontend: JSP, HTML, CSS
Backend: Java Servlets, JDBC
Database: Oracle SQL
Project Management: Maven
Architecture: MVC (Model-View-Controller)

Database Structure
-------------------
1. Users Table
--
The users table stores registered users with unique credentials and a default "Employee" role for new sign-ups.


CREATE TABLE users (
    id NUMBER GENERATED ALWAYS AS IDENTITY,
    uname VARCHAR2(50) NOT NULL UNIQUE,
    upwd VARCHAR2(50) NOT NULL,
    uemail VARCHAR2(100) NOT NULL PRIMARY KEY,
    umobile VARCHAR2(20) NOT NULL UNIQUE,
    designation VARCHAR2(50),
    role VARCHAR2(50) DEFAULT 'Employee'
);

2. Software Table
--
The software table stores information about available software applications for which employees can request access.


CREATE TABLE software (
    id NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    name VARCHAR2(100) UNIQUE NOT NULL,
    description VARCHAR2(500)
);

3. Requests Table
--
The requests table records access requests submitted by employees, linking to both users and software tables, and allowing managers to approve or reject them.


CREATE TABLE requests (
    id NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    user_email VARCHAR2(100) NOT NULL,
    software_id NUMBER NOT NULL,
    reason VARCHAR2(500),
    status VARCHAR2(20) DEFAULT 'Pending' CHECK (status IN ('Pending', 'Approved', 'Rejected')),
    CONSTRAINT fk_user FOREIGN KEY (user_email) REFERENCES users(uemail) ON DELETE CASCADE,
    CONSTRAINT fk_software FOREIGN KEY (software_id) REFERENCES software(id) ON DELETE CASCADE
);


Getting Started
---------------
Prerequisites
-------------
->Java Development Kit (JDK 11 or higher)
->Apache Maven
->Oracle Database
->Apache Tomcat (or any compatible Java Servlet container)

Installation
-------------
1. Clone the repository:

git clone https://github.com/BharatBhagyajyoti/User-Access-Management-System.git

2.Navigate to the project directory and build the project:

cd User-Access-Management-System
mvn clean install

3.Configure the database settings in the JDBC connection file.
4.Run the application on your servlet container (e.g., Apache Tomcat).

Usage
------
Register as an employee.
Log in and request access to a software application.
Managers can log in to review and approve/reject access requests.
Admins can add and manage software applications in the system.
