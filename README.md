# Library Management System

A lightweight, console-based Library Management System built with Python. The application facilitates catalog management, patron registration, and basic circulation workflows including borrowing and returning books.

---

## Features

- **Book Catalog Management**:
  - View all books currently in inventory with available stock levels.
  - Add new books with duplicate ID validation.
  - Search books by title (case-insensitive substring match).
- **Patron Management**:
  - Register new users with unique user IDs.
  - Track individual borrowed books per user.
- **Circulation System**:
  - Borrow books (automatically validates user existence, book existence, and inventory levels).
  - Return books (restores stock level and updates user borrow list).
  - Inspect list of currently checked-out books per user.

---

## Project Structure

```text
.
├── main.py          # Core application logic, classes, and CLI loop
├── README.md        # Project overview and setup instructions
└── STATEMENT.md     # Problem statement, scope, and technical design
```

---

## Requirements

- Python 3.6 or higher
- Standard Python libraries (`sys`, `os`—no external dependencies required)

---

## Getting Started

### 1. Clone or Download the Repository

Save `main.py` to your working directory.

### 2. Run the Application

Execute the Python script using your terminal or command prompt:

```bash
python main.py
```

---

## Usage Guide & Menu Options

Upon starting, the application preloads a small set of books and users for demonstration. You will be greeted with the following interactive menu:

```text
-----> Welcome to the Library Management System <-----

1. View all books
2. Add books
3. Search for a book by title
4. Borrow a book
5. Return a book
6. View borrowed books
7. Add new User
8. Exit
```

### Key Workflows

- **Search Books (`Option 3`)**: Enter any part of a title (e.g., `potter` or `1984`) to locate matching items.
- **Borrow a Book (`Option 4`)**: Enter your User ID and the Book ID. If copies are available (`quantity > 0`), the checkout completes and stock decreases by 1.
- **Return a Book (`Option 5`)**: Enter your User ID and the Book ID. If you currently hold the book, it is cleared from your record and stock increments by 1.
- **View Borrowed Books (`Option 6`)**: Enter a User ID to see all titles currently on loan to that patron.
