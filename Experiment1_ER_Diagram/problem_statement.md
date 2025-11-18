# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

## Scenario A: City Fitness Club Management
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
*Paste or attach your diagram here*  


<img width="933" height="822" alt="GYM drawio" src="https://github.com/user-attachments/assets/25105c95-f7de-4b8a-b409-a8f95019db08" />




### Entities and Attributes

| Entity |           Attributes (PK, FK)               |         Notes                |
|--------|---------------------------                  |------------------------------|
|Member  | MemberID ,Type,StartDate                    | Store member details         |
|Trainer | TrainerID,Name,Contact	                   | Store Trainer details        |
|Program | ProgramID,Name,Cost                         | Programs like Zumbz/yoga     |
|Session | SessionID,Date,MemberID,TrainerID           | Tracks attendance            |
|Payment | PaymentID,Amount,MemberID,Date              | Tracks payments by members   |

### Relationships and Constraints

|    Relationship    | Cardinality   |                 Participation                  |                Notes                  |
|--------------------|---------------|------------------------------------------------|---------------------------------------|
|  Member-Program    |    M:N        | Optional(Member),Mandatory(Join)         |  Members may join multiple programs  |
|  Trainer-Program   |    M:N        | Optional(Trainer),Mandatory(Assign)        | Trainers may run multiple programs   |
|  Session-Member    |    1:N        | Mandatory (Session), Optional (Member) | Each session has one member  |
|  Session-Trainer    |    1:N        | Mandatory (Session), Optional (Trainer) | Each session has one trainer  |
|  Member-Payment    |    1:N        | Mandatory (Payment), Optional (Member/) | Payments linked to members  |

### Assumptions
- Program = recurring class; Session = specific instance.
- Payments cover both memberships and sessions.
- A Session links one Member and one Trainer.

---

## Scenario B: City Library Event & Book Lending System
**Business Context:**
The Central Library wants to manage book lending and cultural events.
**Requirements:**
- Members borrow books, with loan and return dates tracked.
- Each book has title, author, and category.
- Library organizes events; members can register.
- Each event has one or more speakers/authors.
- Rooms are booked for events and study.
- Overdue fines apply for late returns


### ER Diagram:
*Paste or attach your diagram here*  

<img width="1241" height="921" alt="Library drawio" src="https://github.com/user-attachments/assets/02fbeaf8-d9e6-4f16-8fa7-8f898f838c92" />



### Entities and Attributes

|  Entity |                              Attributes (PK, FK)                                  |         Notes           |
|---------|-----------------------------------------------------------------------------------|-------------------------|
| Member  | MemberID (PK), Name,Contact                                                     | Library members         |
| Book    | BookID (PK), Title, Author, Category                    | Books in collection     |
| Loan    | LoanID (PK),Date,Fine, MemberID (FK), BookID (FK)       | Tracks book borrowing   |
| Event   | EventID (PK), Name,Date,RoomID (FK)                     | Library cultural events |
| Speaker | SpeakerID (PK), Name,Contact                            | Event speakers/authors  |
| Booking | 	BookingID (PK), Date, RoomID (FK), MemberID (FK)     | Study room reservations |

### Relationships and Constraints

|       Relationship | Cardinality |                       Participation                    |               Notes              |
|--------------------|-------------|--------------------------------------------------------|----------------------------------|
| Member–Loan        |     1:N     |  Mandatory (Loan), Optional (Member)          | Members borrow books            |
| Member–Event       |     M:N     |  Mandatory (Registration), Optional | Members register for events      |
| Event–Speaker      |     M:N     |  Mandatory (EventSpeaker), Optional| Events may have multiple speakers|
| Event–Room         |     1:1     |  Mandatory (Event), Optional (Room)               | Each event in one room           |
| Room–Booking       |     1:N     |  Mandatory (Booking), Optional (Room)              | Rooms booked for study by members|

### Assumptions
- Overdue fines are stored per Loan record.
- BookCopy not modeled
- Rooms serve both events and study bookings.

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
*Paste or attach your diagram here*  

<img width="1571" height="811" alt="Restaurant drawio" src="https://github.com/user-attachments/assets/ce6499be-476f-4e16-b34d-64b942b302ea" />


### Entities and Attributes

|   Entity     |                                        Attributes (PK, FK)                                            |           Notes            |
|--------------|-------------------------------------------------------------------------------------------------------|----------------------------|
| Customer       | CustomerID, Name, Contact                                                                  | Customer details             |
| Waiter       | WaiterID, Name, Contact                                                                   | Waiter details             |
|  Table       | 	TableID, Number, Capacity                                                            | Restaurant tables          |
|  Reservation |  ResID, Date, Time, Guests, CustomerID, TableID                                                          | Table bookings             |
|  Order       | OrderID, ResID, Status| Orders linked              |
|  Dish        |  DishID, Name, Category                        | Menu items                 |
|  Bill        | 	BillID, ResID, Amounts                    | Final bill per reservation |  
|  Assignment  | AssignID, WaiterID, ResID                                                 | Resolves Waiter–Reservation|
### Relationships and Constraints

|      Relationship     | Cardinality |            Participation                                  |                Notes                    |
|-----------------------|-------------|-----------------------------------------------------------|-----------------------------------------|
|  Customer–Reservation |  1:N        |  Mandatory for Reservation, Optional for Customer         | One customer can have many reservations |
| Reservation–Table     |  1:1        |  Mandatory for Reservation, Optional for Tabl             | Each reservation is for one table       |
|   Order–Dish          |  M:N        |  Mandatory for Order_Item, Optional for Order/Dish        | An order can include many dishes        |
|  Reservation–Bill     |  1:1        |  Mandatory for Bill, Optional for Reservation             | One bill per reservation                |
| Waiter–Reservation    |  M:N        | Mandatory for Assignment, Optional for Waiter/Reservation | Multiple waiters can serve a reservation|

### Assumptions
- Walk-in customers are still recorded
- One bill per reservation
- Split payments not modeled; could extend with a Payment entity.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
