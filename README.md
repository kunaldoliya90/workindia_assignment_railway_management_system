<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Railway Management System API</title>
</head>
<body>

    <h1>Railway Management System API</h1>
    <p>
        This is a Django-based application that manages railway operations, including user registration, login, seat availability checks, booking seats, and viewing booking details. It features role-based access (Admin and User) and ensures proper handling of concurrent bookings.
    </p>

    <hr>

    <h2>Installation</h2>
    <ol>
        <li>
            <strong>Clone the repository</strong>
            <pre><code>git clone https://github.com/kunaldoliya90/workindia_assignment_railway_management_system.git</code></pre>
        </li>
        <li>
            <strong>Set up a virtual environment</strong>
            <pre><code>python -m venv venv</code></pre>
            <pre><code>source venv/bin/activate  # For Windows: venv\Scripts\activate</code></pre>
        </li>
        <li>
            <strong>Install dependencies</strong>
            <pre><code>pip install -r requirements.txt</code></pre>
        </li>
        <li>
            <strong>Install PostgreSQL</strong>
            <p>If you don’t already have PostgreSQL installed, follow the <a href="https://www.postgresql.org/docs/" target="_blank">official PostgreSQL guide</a>.</p>
        </li>
        <li>
            <strong>Create a PostgreSQL database</strong>
            <pre><code>psql -U postgres -c "CREATE DATABASE railway_management_test;"</code></pre>
        </li>
        <li>
            <strong>Configure the database in <code>settings.py</code></strong>
            <pre><code>
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
            </code></pre>
        </li>
    </ol>

    <hr>

    <h2>Setup</h2>
    <ol>
        <li>
            <strong>Apply database migrations</strong>
            <pre><code>python manage.py migrate</code></pre>
        </li>
        <li>
            <strong>Create an admin user</strong>
            <pre><code>python manage.py createsuperuser</code></pre>
        </li>
        <li>
            <strong>Run the development server</strong>
            <pre><code>python manage.py runserver</code></pre>
        </li>
    </ol>

    <hr>

    <h2>API Endpoints</h2>
    <p>All endpoints are prefixed with <code>/booking/</code>.</p>

    <h3>Authentication</h3>
    <ul>
        <li>
            <strong>Register a User</strong>
            <p><strong>URL:</strong> <code>/booking/register/</code></p>
            <p><strong>Method:</strong> POST</p>
            <p><strong>Request Body:</strong></p>
            <pre><code>
{
    "username": "your_username",
    "password": "your_password",
    "is_admin": false
}
            </code></pre>
        </li>
        <li>
            <strong>Login</strong>
            <p><strong>URL:</strong> <code>/booking/login/</code></p>
            <p><strong>Method:</strong> POST</p>
            <p><strong>Request Body:</strong></p>
            <pre><code>
{
    "username": "your_username",
    "password": "your_password"
}
            </code></pre>
        </li>
    </ul>

    <hr>

    <h3>Admin Features</h3>
    <p>Admin-only endpoints require an API key sent in the <code>X-API-KEY</code> header.</p>
    <ul>
        <li>
            <strong>Add a Train</strong>
            <p><strong>URL:</strong> <code>/booking/add_train/</code></p>
            <p><strong>Method:</strong> POST</p>
            <p><strong>Request Body:</strong></p>
            <pre><code>
{
    "source": "Station_A",
    "destination": "Station_B",
    "total_seats": 100
}
            </code></pre>
            <p><strong>Headers:</strong></p>
            <pre><code>X-API-KEY: your_admin_api_key</code></pre>
        </li>
    </ul>

    <hr>

    <h3>User Features</h3>
    <ul>
        <li>
            <strong>Check Seat Availability</strong>
            <p><strong>URL:</strong> <code>/booking/check_availability/&lt;source&gt;/&lt;destination&gt;/</code></p>
            <p><strong>Method:</strong> GET</p>
        </li>
        <li>
            <strong>Book a Seat</strong>
            <p><strong>URL:</strong> <code>/booking/book_seat/</code></p>
            <p><strong>Method:</strong> POST</p>
            <p><strong>Request Body:</strong></p>
            <pre><code>
{
    "train_id": 1
}
            </code></pre>
        </li>
        <li>
            <strong>View Booking Details</strong>
            <p><strong>URL:</strong> <code>/booking/booking_details/</code></p>
            <p><strong>Method:</strong> GET</p>
            <p><strong>Authorization:</strong> Requires user token in the header:</p>
            <pre><code>Authorization: Token your_user_token</code></pre>
        </li>
    </ul>

</body>
</html>
