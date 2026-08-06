# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="1536" height="1024" alt="gym" src="https://github.com/user-attachments/assets/edc30d59-1adf-4048-9f86-c080a6dd4b47" />




### Entities and Attributes

| Entity         | Attributes (PK, FK)                                                     | Notes                                          |
| -------------- | ----------------------------------------------------------------------- | ---------------------------------------------- |
| **Member**     | **Member_id (PK)**, Name, Contact_no, Membership_type, Start_date       | Stores details of gym members.                 |
| **Trainer**    | **Trainer_id (PK)**, Name, Specialization, Experience                   | Stores trainer information.                    |
| **Assignment** | **Assignment_id (PK)**, Trainer_id (FK), Date, Duration                 | Stores training assignments given by trainers. |
| **Attendance** | **Attendance_id (PK)**, Member_id (FK), Date, Status                    | Records member attendance.                     |
| **Payment**    | **Payment_id (PK)**, Member_id (FK), Amount, Payment_date, Payment_type | Stores payment details of members.             |


### Relationships and Constraints

| Relationship                    | Cardinality        | Participation | Notes                                                                                |
| ------------------------------- | ------------------ | ------------- | ------------------------------------------------------------------------------------ |
| **Member – Training – Trainer** | Many-to-Many (M:N) | Total         | A member can train with multiple trainers, and a trainer can train multiple members. |
| **Assignment – Attendance**     | One-to-Many (1:M)  | Partial       | One assignment can have multiple attendance records.                                 |
| **Assignment – Payment**        | One-to-Many (1:M)  | Partial       | One assignment can be associated with multiple payment records.                      |


### Assumptions
- Each Member has a unique Member_id, and each Trainer has a unique Trainer_id.
- Every Assignment is conducted by one trainer, while a trainer can conduct multiple assignments.
- Each Payment and Attendance record belongs to one member and is identified by a unique primary key.
  
---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/a92fe53e-6477-4a3e-af66-333d6962fbb8" />



### Entities and Attributes

| Entity      | Attributes (PK, FK)                                   | Notes                                                                   |
| ----------- | ----------------------------------------------------- | ----------------------------------------------------------------------- |
| **Member**  | **Member_id (PK)**, Name, Contact_no                  | Stores information about library members.                               |
| **Book**    | **Book_id (PK)**, Title, Author, Category             | Stores details of books available in the library.                       |
| **Loan**    | **Loan_id (PK)**, Loan_date, Return_date, Fine_amount | Records book borrowing and return information, including overdue fines. |
| **Event**   | **Event_id (PK)**, Event_name, Event_date             | Stores information about library events.                                |
| **Speaker** | **Speaker_id (PK)**, Name, Expertise                  | Stores details of speakers/authors participating in events.             |
| **Room**    | **Room_id (PK)**, Room_name, Capacity                 | Stores details of library rooms used for events and study.              |


### Relationships and Constraints

| Relationship                       | Cardinality                        | Participation | Notes                                                                                       |
| ---------------------------------- | ---------------------------------- | ------------- | ------------------------------------------------------------------------------------------- |
| **Member – Borrows – Loan – Book** | Member (1:M) Loan, Book (1:M) Loan | Total         | A member can borrow many books, and each loan record corresponds to one borrowed book.      |
| **Member – Registers – Event**     | Many-to-Many (M:N)                 | Partial       | A member can register for multiple events, and each event can have many registered members. |
| **Event – Conducted By – Speaker** | Many-to-Many (M:N)                 | Total         | Each event has one or more speakers, and a speaker may participate in multiple events.      |
| **Event – Held In – Room**         | Many-to-One (M:1)                  | Total         | Each event is held in one room, while a room can host multiple events at different times.   |


### Assumptions
- Every loan is associated with exactly one member and one book, and overdue fines are stored in the Loan entity.
- A member may register for multiple events, and an event can have multiple members attending.
- Each event is conducted by one or more speakers and is scheduled in a single room, while rooms may be reused for different events at different times. 

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/83d1fd4d-c1c3-4f4a-a3df-d8b3bf18c17e" />



### Entities and Attributes
| Entity          | Attributes (PK, FK)                                                                                            | Notes                                                             |
| --------------- | -------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Customer**    | **Customer_id (PK)**, Name, Phone_no, Email                                                                    | Stores customer details for reservations and walk-ins.            |
| **Reservation** | **Reservation_id (PK)**, Res_date, Res_time, No_of_guests, Reservation_type (Walk-in/Reserved), Waiter_id (FK) | Stores reservation information and assigned waiter.               |
| **Waiter**      | **Waiter_id (PK)**, Name, Phone_no, Shift                                                                      | Stores waiter details.                                            |
| **Order**       | **Order_id (PK)**, Order_time, Reservation_id (FK)                                                             | Stores food orders linked to reservations.                        |
| **Order_Item**  | **Order_item_id (PK)**, Order_id (FK), Dish_id (FK), Quantity, Unit_price                                      | Represents individual dishes included in an order.                |
| **Dish**        | **Dish_id (PK)**, Dish_name, Price, Category_id (FK)                                                           | Stores menu items offered by the restaurant.                      |
| **Category**    | **Category_id (PK)**, Category_name                                                                            | Stores dish categories such as Starter, Main Course, and Dessert. |
| **Bill**        | **Bill_id (PK)**, Bill_date, Food_total, Service_charge, Tax, Grand_total, Reservation_id (FK)                 | Stores billing details generated for each reservation.            |


### Relationships and Constraints

| Relationship                             | Cardinality                                    | Participation | Notes                                                                                      |
| ---------------------------------------- | ---------------------------------------------- | ------------- | ------------------------------------------------------------------------------------------ |
| **Customer – Makes – Reservation**       | One-to-Many (1:M)                              | Partial       | A customer can make multiple reservations, while each reservation belongs to one customer. |
| **Reservation – Places – Order**         | One-to-Many (1:M)                              | Total         | Each reservation can have multiple orders, and every order belongs to one reservation.     |
| **Order – Contains – Order_Item – Dish** | Many-to-Many (M:N) (resolved using Order_Item) | Total         | An order contains multiple dishes, and a dish can appear in many different orders.         |
| **Reservation – Assigned_to – Waiter**   | Many-to-One (M:1)                              | Total         | Each reservation is served by one waiter, while a waiter can serve many reservations.      |
| **Reservation – Generates – Bill**       | One-to-One (1:1)                               | Total         | Every completed reservation generates one bill.                                            |
| **Dish – Belongs_to – Category**         | Many-to-One (M:1)                              | Total         | Every dish belongs to one category, while a category can contain many dishes.              |


### Assumptions
- Customers may either reserve a table in advance or be recorded as walk-in customers using the Reservation_type attribute.
- Each reservation is assigned to exactly one waiter, but a waiter can handle multiple reservations during a shift.
- Every bill is generated for a single reservation and includes the total food cost, service charge, applicable tax, and grand total.
  

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
