LITTLE LEMON DJANGO REST FRAMEWORK CAPSTONE
===========================================

Project: littlelemon
App: restaurant
Database: MySQL
Environment: Pipenv

SETUP
-----
1. Install Python 3.11, MySQL Server and Pipenv.
2. Create the MySQL database:
   CREATE DATABASE littlelemon CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
3. Set environment variables before running the project:
   DB_NAME=littlelemon
   DB_USER=root
   DB_PASSWORD=your_mysql_password
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DJANGO_DEBUG=True
4. Run:
   pipenv install
   pipenv shell
   python manage.py makemigrations
   python manage.py migrate
   python manage.py createsuperuser
   python manage.py test
   python manage.py runserver

API PATHS FOR PEER REVIEW
-------------------------
Public:
GET    /api/
GET    /api/categories/
GET    /api/menu-items/
GET    /api/menu-items/{id}/
GET    /api/menu-items/?search=salad
GET    /api/menu-items/?ordering=price

Authentication:
POST   /auth/users/                  Register a user (Djoser)
POST   /auth/token/login/            Obtain token (username, password)
POST   /auth/token/logout/           Logout and invalidate token
POST   /api-token-auth/              Obtain DRF token

Manager group:
GET    /api/groups/manager/users
POST   /api/groups/manager/users     Add existing user; JSON {"username":"customer"}
POST   /api/menu-items/              Create menu item
PUT    /api/menu-items/{id}/         Update menu item
PATCH  /api/menu-items/{id}/         Partially update menu item
DELETE /api/menu-items/{id}/         Delete menu item

Bookings (authenticated):
GET    /api/bookings/
POST   /api/bookings/                JSON: {"name":"Alex","no_of_guests":2,"booking_date":"2026-12-01T19:00:00Z"}
GET    /api/bookings/{id}/
PUT    /api/bookings/{id}/
PATCH  /api/bookings/{id}/
DELETE /api/bookings/{id}/

Cart (authenticated):
GET    /api/cart/menu-items
POST   /api/cart/menu-items         JSON: {"menuitem":1,"quantity":2}
DELETE /api/cart/menu-items         Clear cart

Orders (authenticated):
GET    /api/orders
POST   /api/orders                  Create order from current user's cart
GET    /api/orders/{id}
PATCH  /api/orders/{id}
DELETE /api/orders/{id}             Manager only

INSOMNIA TOKEN AUTHENTICATION
-----------------------------
1. Register at POST /auth/users/ with {"username":"customer1","password":"StrongPass123!"}.
2. Obtain token at POST /auth/token/login/ with username and password.
3. In Insomnia, select Auth > Bearer Token only if using JWT. This project uses DRF TokenAuthentication:
   Add header: Authorization: Token <token>
4. Use Content-Type: application/json for JSON requests.

PERMISSIONS
-----------
- Menu list/detail is public. Menu create/update/delete requires Manager group.
- Booking endpoints require authentication; users see and manage their own bookings.
- Cart and orders require authentication.
- Manager can view all orders. Delivery Crew can view assigned orders and update status.
- Djoser registration and token endpoints are enabled.

TESTS
-----
Run: python manage.py test
The included tests cover public menu access, anonymous menu-write rejection,
authenticated booking creation and user-scoped booking retrieval.

GIT AND GITHUB
--------------
Initialize and push this project:
   git init
   git add .
   git commit -m "Build Little Lemon DRF capstone API"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
   git push -u origin main

IMPORTANT
---------
This project is generated from the assignment brief and is not the official Coursera starter project.
Configure your own local MySQL credentials. Do not commit passwords or .env files.
Run migrations and tests locally, and verify endpoints in Insomnia before submitting your GitHub URL.
