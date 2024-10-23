
# Restaurant Management System Core Java Project

This project is a simple Restaurant Management System developed using **Core Java**. It provides functionality for managing employees, menu items, and customer orders within a restaurant. The system allows managers to oversee staff and menu items, while staff can take and manage customer orders. The system also tracks sales and generates reports.

## System Architecture

The project follows a **Model-View-Controller (MVC)** architecture, where:
- **Controller**: Handles user inputs and controls the flow of the program.
- **Model (Database)**: Manages data related to orders, employees, and menu items.
- **View (UserInterface)**: Displays the user interface for interacting with the system.

### High-Level Structure
- **Controller.java**: Manages program flow, processes user inputs, and interacts with the database.
- **UserInterface.java**: Presents the menus, inputs, and data to the user.
- **Database.java**: Handles loading, saving, and retrieving data for staff, menu items, and orders.

## Core Components

### 1. **Controller**
The main class that coordinates the application's operations. It manages different system states such as login, menu display, order processing, employee management, and report generation.

#### Key Methods:
- **mainLoop()**: Controls the primary flow of the system. Based on user input, it moves between scenes such as login, menu display, and employee management.
- **userLogin()**: Manages the login process for both employees and managers.
- **createOrder()**: Handles the creation of new orders by staff.
- **selectOrderMenu()**: Provides options to manage orders, such as creating, updating, and closing orders.
- **generateReports()**: Generates daily sales and payment reports.

### 2. **UserInterface**
The class responsible for interacting with the user. It displays menus, prompts for input, and shows data. It can render the main menu, employee management options, and order details.

#### Key Methods:
- **showMainMenu(userType)**: Displays different menus based on whether the user is a manager or employee.
- **displayMessage(message)**: Outputs messages to the user.
- **userInput()**: Collects input from the user.

### 3. **Database**
This component manages data for employees, menu items, and orders. It loads initial data from files and saves any modifications.

#### Key Methods:
- **loadFiles()**: Loads employee, menu, and order data from files.
- **addOrder()**: Creates a new order.
- **findStaffByID(id)**: Searches and retrieves a staff member by their ID.
- **generateOrderReport()**: Generates a report of all orders for the day.
- **editMenuItemData()**: Edits details of a menu item such as its name, price, or type.

## Main Features

### 1. **Login System**
- Managers and staff can log in using their unique IDs and passwords.
- The system sets the current user based on their role (Manager or Employee).

```java
private void userLogin() {
    cView.loginView();
    printMessageToView("Login as manager? (Y/N)");
    // ... (login logic)
}
```

### 2. **Employee Management (Manager Only)**
- Managers can add, edit, and delete employee records.
- Staff can be clocked in and out for work.

```java
private void addNewStaff() {
    cView.addNewStaffView();
    // Gather details like name, password, role
    // Add the new staff to the database
    cDatabase.addStaff(newID, newLastName, newFirstName, newPassword, isManager);
}
```

### 3. **Menu Management (Manager Only)**
- Managers can add, edit, and remove menu items (Main course, Drinks, Alcohol, Dessert).

```java
private void addNewMenuItem() {
    int newID = generateMenuID();
    // Gather details like name, price, type
    // Add the new menu item to the database
    cDatabase.addMenuItem(newID, newName, newPrice, newType);
}
```

### 4. **Order Management**
- Staff can create new customer orders by selecting items from the menu.
- Orders can be updated, closed, or canceled.

```java
private void createOrder() {
    int newOrderID = cDatabase.addOrder(currentUserID, currentUserName);
    editOrderItem(newOrderID);  // Allows adding items to the order
}
```

### 5. **Sales and Payment Reports**
- The system generates sales reports and payment details for the day, accessible by managers.

```java
private void generateReports() {
    cDatabase.generateOrderReport(todaysDate);
    cDatabase.generatePaymentReport(todaysDate);
}
```

## Sample Code Snippets

### Adding a New Employee

```java
private void addNewStaff() {
    printMessageToView("Enter first name:");
    String firstName = cView.userInput();
    printMessageToView("Enter last name:");
    String lastName = cView.userInput();
    // Additional inputs like password and manager role
    cDatabase.addStaff(newID, lastName, firstName, newPassword, isManager);
}
```

### Creating an Order

```java
private void createOrder() {
    int newOrderID = cDatabase.addOrder(currentUserID, currentUserName);
    editOrderItem(newOrderID); // Add items to the order
}
```

### Generating a Report

```java
private void generateSalesReports() {
    if(cDatabase.checkIfAllOrderClosed()) {
        String filename = cDatabase.generateOrderReport(todaysDate);
        printMessageToView("Report generated: " + filename);
    } else {
        printMessageToView("Please close all orders before generating reports.");
    }
}
```
## Final Notes

This Restaurant Management System provides the essential tools needed to manage restaurant operations, from handling orders to managing employees and menu items. The system's modular design allows for future updates and feature additions. Developers can expand the project by integrating additional modules, enhancing security, or optimizing performance.

For any issues, questions, or contributions, please refer to the documentation or submit a request through the project's repository.

