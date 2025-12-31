# Demo-Login-Page-Project
A Google-style login system built with HTML, CSS, PHP, and MySQL. It mimics Google’s sign-in UI and stores user email and password in a database. Includes both plain-text (for testing) and secure hashed storage versions. Responsive design and simple admin panel to view stored users locally via XAMPP.

FOR KNOWLEDGE PURPOSE.

Google-Style Login (Demo)

A simple Google-like sign-in UI built with HTML/CSS and PHP + MySQL for backend storage.
This demo deliberately contains a plain-text password storage option for local testing only (insecure).
Use the secure hashed version for any real usage (instructions below).

------------------------------------------------------------
Project Overview
------------------------------------------------------------
- Responsive HTML/CSS front-end mimicking Google's login page.
- PHP backend that inserts submitted email and password into a MySQL 'users' table.
- users.php page (admin view) for browsing stored records.
- Two storage versions: 
  (1) store.php - secure (hashed passwords)
  (2) store_plain.php - insecure (plain-text passwords, for testing only)

Tech Stack:
HTML, CSS, PHP, MySQL, XAMPP (local server)

------------------------------------------------------------
Security Warning
------------------------------------------------------------
This repository contains an insecure demo variant that stores passwords as plain text.
Never deploy this to production or any public server.

------------------------------------------------------------
Project File Structure
------------------------------------------------------------
google-login/
│
├── index.html          # Frontend login page
├── connect.php         # Database connection
├── store_plain.php     # Stores plain-text password (insecure, demo only)
├── store.php           # Secure version (uses password_hash())
├── users.php           # Admin page to view stored users
├── README.txt          # This file

------------------------------------------------------------
Database Setup (MySQL via phpMyAdmin)
------------------------------------------------------------
1. Open phpMyAdmin and run this SQL:

CREATE DATABASE IF NOT EXISTS google_login;
USE google_login;

CREATE TABLE IF NOT EXISTS users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  email VARCHAR(100) NOT NULL,
  password VARCHAR(255) NOT NULL
);

2. Update connect.php if needed (default is fine for XAMPP):
   $servername = "localhost";
   $username = "root";
   $password = "";
   $database = "google_login";

------------------------------------------------------------
How to Run the Project (using XAMPP)
------------------------------------------------------------
1. Place project folder inside:
   C:\xampp\htdocs\google-login

2. Start Apache and MySQL from XAMPP Control Panel.

3. In your browser, open:
   http://localhost/google-login/index.html

4. Fill in the form and click "Next" to save data.

5. Check your database table 'users' in phpMyAdmin to see saved data.

------------------------------------------------------------
View Stored Users
------------------------------------------------------------
Visit:
   http://localhost/google-login/users.php?admin_pass=admin123
(Change the admin_pass value in the code for your own use.)

------------------------------------------------------------
Secure Version (Recommended)
------------------------------------------------------------
Use store.php instead of store_plain.php
This version hashes passwords using PHP's password_hash() and verifies with password_verify().

------------------------------------------------------------
Migrating Plain Passwords to Hashed (Optional)
------------------------------------------------------------
You can create migrate_hash.php with this code:

<?php
include 'connect.php';
$res = $conn->query("SELECT id, password FROM users");
while ($r = $res->fetch_assoc()) {
  $id = $r['id'];
  $plain = $r['password'];
  $hash = password_hash($plain, PASSWORD_DEFAULT);
  $conn->query("UPDATE users SET password='$hash' WHERE id=$id");
}
echo "Migration complete";
$conn->close();
?>

------------------------------------------------------------
.gitignore (Recommended)
------------------------------------------------------------
/connect.php
/*.sql
/.env
/vendor/
node_modules/
.DS_Store

------------------------------------------------------------
Summary
------------------------------------------------------------
- This project demonstrates front-end + back-end integration with a realistic UI.
- Plain-text password storage is for educational use only.
- Always use password hashing in production.

