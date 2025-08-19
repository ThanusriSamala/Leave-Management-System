
# 🗂 Leave Management System (Flask + SQLite)

A simple **Leave Management System API** built using **Python (Flask)** and **SQLite**.
It supports adding employees, applying for leave, approving/rejecting requests, and checking leave balance.

---

## 📌 Features

*  Add new employees with unique email IDs.
*  Employees can apply for leave with start & end dates.
*  HR/Admin can approve or reject leave requests.
*  Tracks leave balance for each employee.
*  Input validation & error handling.
*  SQLite database for data storage.

---

## 🛠 Tech Stack

* **Backend**: Python 3.x, Flask
* **Database**: SQLite
* **Tools**: Postman (for API testing)

---

## ⚙️ Project Setup

### 1. Clone the Repository

```bash
git clone https://github.com/ThanusriSamala/Leave-Management-System
cd Leave-Management-System
```

### 2. Create Virtual Environment (recommended)

```bash
python -m venv venv
# Activate environment
source venv/bin/activate     # Linux/Mac
venv\Scripts\activate        # Windows
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Initialize the Database

```bash
python database.py
```

(Creates **database.db** with `Employees` & `LeaveRequests` tables)

### 5. Run the Application

```bash
python app.py
```

The API will run at:
👉 [http://127.0.0.1:5000/](http://127.0.0.1:5000/)

---

## 🗄️ Database Design & ER Diagram

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/091cd777-4eca-4d26-b132-078de9255583" />


### Entities

* **Employee**: name, email (unique), department, joining date, leave balance
* **LeaveRequest**: start date, end date, reason, status (Pending/Approved/Rejected), linked to employee

**Relationship**: Each employee can have multiple leave requests (**1-to-many**)

### Tables

#### Employees

| Column        | Type    | Key/Index | Description                  |
| ------------- | ------- | --------- | ---------------------------- |
| id            | INTEGER | PK        | Unique employee ID           |
| name          | TEXT    |           | Employee name                |
| email         | TEXT    | Unique    | Employee email               |
| department    | TEXT    |           | Department                   |
| joining\_date | TEXT    |           | Date of joining (YYYY-MM-DD) |
| total\_leaves | INTEGER |           | Allotted leave days          |
| leaves\_taken | INTEGER |           | Leaves already taken         |

#### LeaveRequests

| Column       | Type    | Key/Index | Description               |
| ------------ | ------- | --------- | ------------------------- |
| id           | INTEGER | PK        | Unique leave request ID   |
| employee\_id | INTEGER | FK        | References Employees(id)  |
| start\_date  | TEXT    |           | Leave start date          |
| end\_date    | TEXT    |           | Leave end date            |
| reason       | TEXT    |           | Reason for leave          |
| status       | TEXT    |           | Pending/Approved/Rejected |
| applied\_on  | TEXT    |           | Date of application       |

---

## 📮 API Endpoints

### 1. Test Server

**GET /**
Response:

```json
{ "message": "Leave Management System API" }
```

### 2. Add Employee

**POST /employee**

```json
{ 
  "name": "Thanu", 
  "email": "Thanu@example.com", 
  "department": "IT", 
  "joining_date": "2025-01-10" 
}
```

Response:

```json
{"message": "Employee added successfully"}
```

### 3. Apply for Leave

**POST /leave**

```json
{ 
  "employee_id": 1, 
  "start_date": "2025-08-10", 
  "end_date": "2025-08-12", 
  "reason": "Vacation" 
}
```

Response:

```json
{"message": "Leave request submitted successfully, pending approval."}
```

### 4. Approve/Reject Leave

**PUT /leave/\<leave\_id>**

```json
{ "status": "Approved" }
```

or

```json
{ "status": "Rejected" }
```

Response:

```json
{"message": "Leave approved successfully."}
```

### 5. Get Leave Balance

**GET /employee/<id>/balance**
Example: `GET /employee/1/balance`
Response:

```json
{ 
  "employee_id": 1, 
  "total_leaves": 20, 
  "leaves_taken": 5, 
  "remaining_leaves": 15 
}
```

---

## 🧩 Class/Module Design

| Class/Module        | Main Methods                                   | Responsibility      |
| ------------------- | ---------------------------------------------- | ------------------- |
| **EmployeeService** | `add_employee`, `get_balance`                  | Manages employees   |
| **LeaveService**    | `apply_leave`, `approve_leave`, `reject_leave` | Handles leave logic |

---

📷 API Testing Screenshots
1. Test Server
   
      <img width="1919" height="1008" alt="image" src="C:\Users\thanu\Desktop\LMS Project\Leave-Management-System\screenshots\Test_server.png" />

2. Add Employee
   
    <img width="1919" height="1001" alt="image" src="C:\Users\thanu\Desktop\LMS Project\Leave-Management-System\screenshots\Add_Employee.png" />

3. Apply for Leave
   
    <img width="1919" height="1003" alt="image" src="C:\Users\thanu\Desktop\LMS Project\Leave-Management-System\screenshots\Apply_leave.png" />

4. Approve/Reject Leave

   <img width="1919" height="1009" alt="image" src="C:\Users\thanu\Desktop\LMS Project\Leave-Management-System\screenshots\Leave_approved.png" />

5. Get Leave Balance

    <img width="1919" height="1001" alt="image" src="C:\Users\thanu\Desktop\LMS Project\Leave-Management-System\screenshots\leave_balance.png" />


## ✅ Assumptions

* Each employee starts with **20 days** total leave.
* Dates follow `YYYY-MM-DD` format.
* Weekends & holidays are counted in leave days (improvable).
* Only **Pending** leave requests can be approved/rejected.

---

## 🔮 Future Improvements

### Scalability

*  Migrate SQLite → PostgreSQL/MySQL
*  Docker & Kubernetes deployment
*  Redis caching

### Features

*  Build frontend (web/mobile)
*  Authentication & role-based access
*  Support half-day / different leave types
*  Auto-skip weekends & holidays
*  Email/SMS notifications

### Optimizations

*  Database indexing
*  Bulk import/export employee data
*  Analytics dashboard

### Deployment

*  Continuous Integration & Testing
*  Integration with HRMS/Payroll

---

## 🎯 High-Level Design
 <img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/95a81bff-4a32-4c0e-8ae7-256cf3b9a148" />


**Flow:**
 \[Frontend / Postman] → **Flask API** → **SQLite Database**

