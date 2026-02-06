# 🏋️‍♂️ GYM Management Database

## 📌 Project Description
This project is a **Gym Management Database** created using **MySQL**.  
It simulates a real-world gym system to manage **members, trainers, sessions, and equipment**.  
The database allows tracking of memberships, workout sessions, trainers’ specialties, and equipment status.  

Features include:  
- Creating databases and tables.  
- Inserting sample data.  
- Querying data for analytics and management.  
- Managing users with different roles and privileges.  

---

## 🗂️ Database Structure

### Members Table
Stores information about gym members.  

| Column Name      | Type         | Description                       |
|-----------------|--------------|-----------------------------------|
| Member_ID        | INT          | Primary Key, unique member ID     |
| NameMember       | VARCHAR(20)  | Member full name                  |
| JoinDate         | DATE         | Membership start date             |
| SubscriptionType | VARCHAR(15)  | Type of subscription (Monthly/Yearly) |

---

### Trainers Table
Stores information about gym trainers.  

| Column Name    | Type         | Description                     |
|----------------|--------------|---------------------------------|
| Trainer_ID     | INT          | Primary Key, unique trainer ID  |
| NameTrainer    | VARCHAR(20)  | Trainer full name               |
| Specialty      | VARCHAR(15)  | Trainer specialty (e.g., Yoga) |

---

### Sessions Table
Stores details about gym sessions.  

| Column Name    | Type          | Description                          |
|----------------|---------------|--------------------------------------|
| Session_ID     | INT           | Primary Key, unique session ID       |
| Member_ID      | INT           | Foreign Key from Members table       |
| Trainer_ID     | INT           | Foreign Key from Trainers table      |
| SessionDate    | DATE          | Date of the session                  |
| SessionTime    | TIME          | Start time of the session            |
| Duration       | INT           | Duration in minutes                  |
| SessionName    | CHAR(20)      | Name/type of session (e.g., Yoga)   |

---

### Equipments Table
Stores information about gym equipment.  

| Column Name     | Type          | Description                        |
|-----------------|---------------|------------------------------------|
| Equipment_ID    | INT           | Primary Key, unique equipment ID   |
| EquipmentName   | VARCHAR(20)   | Name of the equipment               |
| PurchaseDate    | DATE          | Purchase date of the equipment      |
| Status          | VARCHAR(15)   | Status (Good / Needs Repair)        |

---

## ⚡ Sample Queries

```sql
-- Show all members with monthly subscription
SELECT * FROM Members WHERE SubscriptionType = 'Monthly';

-- Find equipment that needs repair
SELECT * FROM Equipments WHERE Status = 'Needs Repair';

-- Join sessions with members and trainers
SELECT SessionName AS sn, SessionDate, TrainerName AS tn, NameMember AS mn
FROM Sessions AS s
JOIN Members AS m ON s.Member_ID = m.Member_ID
JOIN Trainers AS t ON s.Trainer_ID = t.Trainer_ID;

-- Average session duration by trainer
SELECT T.Trainer_ID, T.TrainerName, AVG(S.Duration) AS AverageDuration
FROM Trainers T
JOIN Sessions S ON T.Trainer_ID = S.Trainer_ID
GROUP BY T.Trainer_ID, T.TrainerName
ORDER BY AverageDuration DESC;
