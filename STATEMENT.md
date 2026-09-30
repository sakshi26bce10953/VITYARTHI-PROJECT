# Project Statement: Library Management System

## 1. Problem Statement

Small organizations, reading clubs, and academic departments frequently require a straightforward, low-friction mechanism to track book inventory and patron circulation without the overhead of enterprise database servers or web infrastructure. 

Manual record-keeping often leads to inventory discrepancies, duplicate record assignments, and untracked loans. This project provides a centralized, object-oriented command-line solution to handle core day-to-day library interactions reliably.

---

## 2. Objectives

- **Automate Circulation**: Manage borrowing and returning workflows with real-time stock adjustment.
- **Data Integrity**: Enforce unique IDs across both user registrations and book catalog entries.
- **Ease of Use**: Deliver an intuitive menu-driven terminal interface requiring zero external dependencies.
- **Modularity**: Implement clear separation of concerns using Object-Oriented Programming (OOP) principles.

---

## 3. Scope of the System

### In-Scope
- In-memory data store for books and registered users.
- Validation checks for:
  - Non-negative inventory before borrowing.
  - Verification that a returned book was actually checked out by that user.
  - Uniqueness constraints on `user_id` and `book_id`.
- Case-insensitive search capabilities across book titles.

### Out-of-Scope (Future Enhancements)
- Persistent storage (file system serialization via JSON/CSV or relational databases like SQLite).
- Due date tracking, overdue fine calculation, and loan period enforcement.
- Role-based access control (distinguishing administrators from patrons).
- Graphic User Interface (GUI) or REST API integration.

---

## 4. Technical Architecture & Design

The application follows an Object-Oriented design consisting of three primary domain models and an orchestration CLI loop:

```
+------------------------------------+
|               Library              |
+------------------------------------+
| - books: List[Book]                |
| - users: List[User]                |
+------------------------------------+
| + add_book(book)                   |
| + register_user(user)              |
| + search_book_by_title(title)      |
| + list_books()                     |
| + add_new_book()                   |
+-----------------+------------------+
                  |
         +--------+--------+
         |                 |
         v                 v
+-----------------+   +--------------------+
|      Book       |   |        User        |
+-----------------+   +--------------------+
| - book_id: int  |   | - user_id: int     |
| - title: str    |   | - name: str        |
| - author: str   |   | - borrowed_books   |
| - quantity: int |   +--------------------+
+-----------------+   | + borrow_book()    |
| + check_avail() |   | + return_book()    |
| + update_qty()  |   | + view_borrowed()  |
+-----------------+   +--------------------+
```

### Component Breakdown

1. **`Book` Class**:
   - Encapsulates book entity attributes (`book_id`, `title`, `author`, `quantity`).
   - Handles inventory verification (`check_availability`) and stock delta operations (`update_quantity`).

2. **`User` Class**:
   - Manages patron profile details (`user_id`, `name`).
   - Maintains the active collection of borrowed book instances (`borrowed_books`).
   - Handles borrow and return checks per user.

3. **`Library` Class**:
   - Acts as the central aggregate root and catalog container.
   - Manages lists of `Book` and `User` instances.
   - Handles catalog lookups, listing, and ID conflict prevention.

4. **`main()` Function**:
   - Initializes sample data.
   - Executes the primary CLI control loop handling input validation, routing, and termination.