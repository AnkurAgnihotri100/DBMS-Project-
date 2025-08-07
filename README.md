# DBMS-Project-
> A database system inspired by **popular payment apps like Paytm**, designed as a **mini payment application with limited features**, and implemented using ER modeling and SQL.

---

## 📌 Project Highlights

- Developed a **mini payment application** database inspired by apps like **Paytm**.
- Designed an **ER model** covering core features such as user profiles, payments, bill handling, insurance services, and fund transfers.
- Converted the ER model into normalized relational schemas up to **BCNF**.
- Implemented advanced **SQL** and **Relational Algebra** queries for analytical and transactional operations.

---

## 🧱 Key Entities

- `User(user_id, phone_no)`
- `Account(account_num, user_id, IFSC_code, acc_type)`
- `Bank(IFSC_code, bank_name, branch_name)`
- `Bill(transaction_id, user_id, date, time, amount, status)`
  - Specializations: 
    - `Telephone_Bill(transaction_id, telephone_number)`
    - `Ticket(transaction_id, booking_id)`
- `Insurance(insurance_id, transaction_id, user_id, type, ini_date, ter_date, amount, duration)`
- `Transfer_Fund(transaction_id, receiver_id, user_id, date, time, amount, status)`
- `Profile(user_id, first_name, last_name, dob, email)`

---

## 📊 Functional Dependencies & Normalization

- All tables normalized to **BCNF** to reduce redundancy and preserve data integrity.
- Sample decomposition:
  - `Account(account_num, acc_type, IFSC_code, user_id)`
  - `Bank(IFSC_code, branch_name, bank_name)`
- Dependencies like:
  - `account_num → IFSC_code, acc_type, bank_name, branch`
  - `transaction_id → date, time, amount, status`

---

## 🔄 ER to Relational Schema Conversion

- Mapped all strong and weak entities.
- Managed one-to-one, one-to-many, and many-to-many relationships.
- Example:
  - One-to-many `User` ↔ `Account` transformed by embedding `user_id` in `Account`.

---

## 🧪 Sample SQL Queries

```sql
-- 1. Find user id and booking id of those users who booked tickets successfully
SELECT user_id, booking_id 
FROM ticket 
JOIN bill USING(transaction_id) 
WHERE status = 'Success';

-- 2. Find average insurance amount for insurances > 10,000
SELECT AVG(amount) 
FROM insurance 
WHERE amount > 10000;

-- 3. Find user_id, insurance type, termination date for amount < 1Cr & duration < 4 yrs
SELECT user_id, insurance_type, ter_date 
FROM insurance 
WHERE amount < 10000000 AND duration < 4;
