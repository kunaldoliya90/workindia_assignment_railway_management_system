# Railway Management System API

This project is a Django-based railway management system that enables users to register, log in, check seat availability, book seats, and view booking details. It implements role-based access control (Admin and User) and handles race conditions for concurrent seat bookings.


## Installation

1. **Clone the repository:**

    ```bash
    git clone https://github.com/aboutaditya/WorkIndiaXRailwayManagement.git
    ```

2. **Create and activate a virtual environment:**

    ```bash
    python -m venv venv
    source venv/bin/activate  # For Windows: `venv\Scripts\activate`
    ```

3. **Install the required packages:**

    ```bash
    pip install -r requirements.txt
    ```

4. **Install PostgreSQL** if it's not already installed. You can follow the [official PostgreSQL documentation](https://www.postgresql.org/docs/).

5. **Create a PostgreSQL database:**

    ```bash
    psql -U postgres -c "CREATE DATABASE railway_management_test;"
    ```

6. **Update the `DATABASES` section in `settings.py` with your PostgreSQL credentials:**

    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'railway_management_test',
            'USER': 'your_postgres_username',
            'PASSWORD': 'your_postgres_password',
            'HOST': 'localhost',
            'PORT': '5432',
        }
    }
    ```

---

## Setup

1. **Run migrations:**

    ```bash
    python manage.py migrate
    ```

2. **Create a superuser (admin):**

    ```bash
    python manage.py createsuperuser
    ```

3. **Start the Django development server:**

    ```bash
    python manage.py runserver
    ```

---

## API Endpoints

All API endpoints are prefixed with `/booking/`.

### Authentication Endpoints

1. **Register User:**
   - **URL:** `/booking/register/`
   - **Method:** `POST`
   - **Payload:**
     ```json
     {
       "username": "your_username",
       "password": "your_password",
       "is_admin": false
     }
     ```

2. **Login User:**
   - **URL:** `/booking/login/`
   - **Method:** `POST`
   - **Payload:**
     ```json
     {
       "username": "your_username",
       "password": "your_password"
     }
     ```

### Admin Endpoints

(Protected by API Key)

1. **Add a New Train:**
   - **URL:** `/booking/add_train/`
   - **Method:** `POST`
   - **Payload:**
     ```json
     {
       "source": "Station_A",
       "destination": "Station_B",
       "total_seats": 100
     }
     ```

2. **API Key:** You must include an API key in the `X-API-KEY` header when accessing admin endpoints:
   ```bash
   X-API-KEY: your_secret_key
