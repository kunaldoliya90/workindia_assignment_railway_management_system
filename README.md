# Railway Management System API

A robust railway management system built using Django, enabling users to register, log in, check seat availability, book seats, and view their booking details. This system incorporates role-based access control (Admin and User) and efficiently handles concurrent seat bookings to prevent race conditions.

---

## 🚀 Features

- 👥 **User Roles:** Separate functionalities for Admin and User, ensuring a clear distinction of responsibilities.  
- 🔒 **Secure Bookings:** Prevents double-booking issues with advanced race condition handling.  
- 🔑 **Effortless Authentication:** Secure login and registration functionality for seamless user experience.  
- 📖 **APIs:** Well-documented endpoints for easy integration with frontend or other systems.  
- 🗄️ **Database Support:** Powered by PostgreSQL for reliable, efficient, and scalable data storage.  
- ⏱️ **Real-time Updates:** Dynamically updates seat availability in real time during booking operations.  
- 🛡️ **Role-based Access Control:** Admin-specific APIs secured with API key authentication for enhanced security.  
- 🚆 **Customizable Trains:** Admins can easily add new trains, specifying source, destination, and total seat capacity.  
- 💻 **Platform Independence:** Fully functional on Windows, macOS, and Linux systems.  
- 📈 **Scalability:** Designed to handle multiple users and concurrent booking requests efficiently.  
- 🔧 **Extensibility:** Built with Django's modularity for easy addition of new features and integrations.  


---

## 🛠️ Installation Steps

1. **Clone the Repository:**

    ```bash
    git clone https://github.com/kunaldoliya90/workindia_assignment_railway_management_system.git
    cd workindia_assignment_railway_management_system
    ```

2. **Create and Activate a Virtual Environment:**

    ```bash
    python -m venv venv
    source venv/bin/activate  # For Windows: `venv\Scripts\activate`
    ```

3. **Install Dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

4. **Install PostgreSQL** if not already installed. Refer to the [PostgreSQL Documentation](https://www.postgresql.org/docs/) for installation instructions.

5. **Set Up PostgreSQL Database:**

    ```bash
    psql -U postgres -c "CREATE DATABASE railway_management_test;"
    ```

6. **Update Database Settings:**

    Edit the `DATABASES` section in `settings.py` with your PostgreSQL credentials:

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

## 🧑‍💻 Project Setup

1. **Apply Migrations:**

    ```bash
    python manage.py migrate
    ```

2. **Create a Superuser:**

    ```bash
    python manage.py createsuperuser
    ```

3. **Start the Development Server:**

    ```bash
    python manage.py runserver
    ```

---

## 📚 API Endpoints

All endpoints are prefixed with `/booking/`.

### 🛂 Authentication

1. **Register User:**
   - **Endpoint:** `/booking/register/`
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
   - **Endpoint:** `/booking/login/`
   - **Method:** `POST`
   - **Payload:**
     ```json
     {
       "username": "your_username",
       "password": "your_password"
     }
     ```

---

### 🔑 Admin Endpoints (Protected by API Key)

1. **Add a New Train:**
   - **Endpoint:** `/booking/add_train/`
   - **Method:** `POST`
   - **Payload:**
     ```json
     {
       "source": "Station_A",
       "destination": "Station_B",
       "total_seats": 100
     }
     ```

2. **Authorization Header:**  
   Include your API key in the header for admin-specific actions:
   ```bash
   X-API-KEY: your_secret_key
