24-57433-2_loginSystem

## Project Overview

This project is a C# Windows Forms Login and Registration System developed using Visual Studio and Microsoft SQL Server. The application allows users to register an account, log in using their credentials, access the home/dashboard screen, and log out securely.

The application uses a SQL Server database to store user information and uses an App.config file to manage the database connection string.

## Environment

- **Programming Language:** C#
- **IDE:** Visual Studio [your version]
- **.NET Version:** [your .NET version]
- **Database:** Microsoft SQL Server [your edition/version]
- **Database Management Tool:** SQL Server Management Studio (SSMS)
- **Connection:** SQL Server using Windows Authentication
- **Connection String Format:**
  `Data Source=localhost;Initial Catalog=SportShopDB;Integrated Security=True;TrustServerCertificate=True;`

> No database password or other sensitive credentials are included in the repository.

Database Creation:

I created the SportShopDB database using SQL Server Management Studio.

After connecting to the local SQL Server instance, I created the database and created the required tables inside it.

The application connects specifically to the SportShopDB database.

The database schema used for the project is provided separately in:

Schema.sql

Database Connection:

Initially, I tested the database connection directly from the C# application using SqlConnection.

The connection was successfully tested and the application displayed:

Connection Open!

After that, I created an App.config file and moved the connection string into the configuration file.

The application retrieves the connection string using:

ConfigurationManager.ConnectionStrings["connectionString"].ConnectionString

This makes the database connection easier to manage because the connection information is separated from the main C# source code.

Registration:

The registration form is responsible for creating a new user account.

The user enters the required registration information and the application sends the information to the SQL Server database.

The registration functionality is implemented in:

frmRegister.cs

The database connection is obtained from App.config.

Login:

The login functionality is implemented in:

frmLogin.cs

The user enters a username and password.

The application uses a SQL query to check whether the entered credentials match a user stored in the database.

The login query uses parameters:

string login = "SELECT * FROM tbl_users WHERE Username = @username AND Password = @password";

The values are passed using parameters:

cmd.Parameters.AddWithValue("@username", txtUsername.Text);
cmd.Parameters.AddWithValue("@password", txtPassword.Text);

If the credentials are correct, the dashboard form is opened and the login form is hidden.

If the credentials are incorrect, a Login Failed message is displayed and the username and password fields are cleared.

Logout:

The application provides a logout function that allows the user to leave the dashboard and return to the login screen.

The logout functionality is used to prevent the user from remaining inside the authenticated part of the application after choosing to log out.

Password Hashing:


Passwords should not be stored as plain text in a database because anyone who gains access to the database could directly read the users' passwords.

Instead, passwords should be converted into a secure hash before being stored.

During login, the entered password can be hashed again and compared with the stored hash.

SQL Injection Demonstration:


The project uses parameterized SQL queries for the login functionality.

For example:

string login = "SELECT * FROM tbl_users WHERE Username = @username AND Password = @password";


cmd.Parameters.AddWithValue("@username", txtUsername.Text);
cmd.Parameters.AddWithValue("@password", txtPassword.Text);

Parameterized queries are important because user input is treated as data rather than being directly inserted into the SQL command.

The vulnerable version, exploit input, fixed version, and demonstration results will be documented here.


Bonus Tasks:
No bonus tasks were attempted.


Problems Encountered and Solutions:


Database Connection:

One of the problems I encountered was connecting the C# Windows Forms application to SQL Server.

I first tested the connection using a SqlConnection and a connection string pointing to the local SQL Server instance.

After successfully establishing the connection, I moved the connection string into App.config.

I then installed the System.Configuration.ConfigurationManager NuGet package so that the application could access the connection string through ConfigurationManager.

App.config

The application initially used a hard-coded connection string in the C# code.

To make the project easier to configure, I created an App.config file and stored the database connection string there.

The C# application now retrieves the connection string from the configuration file.

Project Files:

Important files in this project include:

Login and Register.sln
App.config
frmLogin.cs
frmRegister.cs
frmDashboard.cs
README.md

The Visual Studio generated folders such as bin/, obj/, and .vs/ are excluded from the GitHub repository using .gitignore.

Conclusion:

This project demonstrates how a C# Windows Forms application can communicate with a Microsoft SQL Server database.

The project includes database connectivity, user registration, login functionality, dashboard navigation, and logout functionality.

The application also demonstrates the importance of using configuration files and parameterized SQL queries when developing database applications.

