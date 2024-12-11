# Library Management System

## Overview
This Library Management System provides APIs for librarians and library users to manage and access book borrowing details. It features user management, book borrowing request handling, and history tracking with essential rules and constraints. The backend is implemented in Python, utilizing an SQL database.

## Features
### Librarian APIs
1. **Create a New Library User:** Register users with email and password.
2. **View Book Borrow Requests:** Retrieve all pending requests.
3. **Approve/Deny Borrow Requests:** Manage borrow requests.
4. **View User Borrow History:** View the history of books borrowed by a specific user.

### Library User APIs
1. **List Books:** Retrieve the list of available books.
2. **Borrow a Book:** Submit a request to borrow a book for specific dates.
3. **View Borrow History:** View the user's borrowing history.

### Key Rules
- A book cannot be borrowed by more than one user during the same period.
- Each book is unique, even if multiple copies exist with the same name.
- Basic Authentication is required for all APIs.

#### Error Handling
- Handle invalid or incomplete requests.
- Ensure no overlapping borrow dates for the same book.
- Validate requests for non-existent users or books.

## Bonus Features
- Download borrow history as a CSV file.
- Implement JWT-based authentication instead of Basic Authentication.
- Provide detailed API documentation using Swagger or Postman.

## Installation and Setup
### Prerequisites
- Python 3.9+
- SQL Database (e.g., SQLite, MySQL, or PostgreSQL)
- Required Python libraries: `Flask`, `SQLAlchemy`, `Flask-JWT-Extended`, `Marshmallow`

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/library-management-system.git
   cd library-management-system
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Set up the database schema by running the provided migration script:
   ```bash
   python setup_database.py
   ```
4. Run the Flask application:
   ```bash
   python app.py
   ```
5. Access the APIs at `http://127.0.0.1:5000`.

## API Endpoints
### Librarian APIs
1. **Create a New User**  
   - **POST** `/api/librarian/users`
   - **Payload:**
     ```json
     {
       "email": "user@example.com",
       "password": "securepassword"
     }
     ```

2. **View All Book Borrow Requests**  
   - **GET** `/api/librarian/requests`

3. **Approve/Deny Borrow Requests**  
   - **POST** `/api/librarian/requests/{request_id}`
   - **Payload:**
     ```json
     {
       "status": "approved" // or "denied"
     }
     ```

4. **View a User's Borrow History**  
   - **GET** `/api/librarian/users/{user_id}/history`

### Library User APIs
1. **List Books**  
   - **GET** `/api/user/books`

2. **Borrow a Book**  
   - **POST** `/api/user/borrow`
   - **Payload:**
     ```json
     {
       "book_id": 1,
       "start_date": "2024-01-01",
       "end_date": "2024-01-10"
     }
     ```

3. **View Personal Borrow History**  
   - **GET** `/api/user/history`

### Bonus Features
1. **Download Borrow History**  
   - **GET** `/api/user/history/download`

2. **JWT Authentication**  
   Replace Basic Authentication with JWT by using `Flask-JWT-Extended`.

### Authentication
- Basic Authentication: Include the `Authorization` header with `Basic` credentials.
- JWT Authentication: Include the `Authorization` header with the `Bearer` token.

## Database Schema
### Tables
1. **Users**
   - `id`: Primary key
   - `email`: Unique
   - `password`: Hashed password
   - `role`: Librarian or User

2. **Books**
   - `id`: Primary key
   - `title`: Name of the book
   - `author`: Author of the book
   - `available`: Boolean to check availability

3. **BorrowRequests**
   - `id`: Primary key
   - `user_id`: Foreign key referencing `Users`
   - `book_id`: Foreign key referencing `Books`
   - `start_date`: Requested borrow start date
   - `end_date`: Requested borrow end date
   - `status`: Pending, Approved, or Denied

4. **BorrowHistory**
   - `id`: Primary key
   - `user_id`: Foreign key referencing `Users`
   - `book_id`: Foreign key referencing `Books`
   - `borrow_date`: Date when the book was borrowed
   - `return_date`: Date when the book was returned

## Tools and Technologies
- **Framework:** Flask
- **Database:** SQLite/MySQL/PostgreSQL
- **Authentication:** Basic Authentication (with optional JWT)
- **Documentation:** Swagger/Postman

## How to Contribute
1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature-name
   ```
3. Commit your changes and push the branch:
   ```bash
   git push origin feature-name
   ```
4. Open a Pull Request.

## License
This project is licensed under the MIT License.

