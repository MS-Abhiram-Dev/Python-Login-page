# README for Flask Login Page Application

This README provides a comprehensive guide to a simple login page implementation using Flask, a popular web framework in Python. The application features an HTML login form and Python code to manage login functionality.

## Prerequisites

Ensure that you have Python and Flask installed on your system. You can install Flask using pip:

```bash
pip install Flask
```

## Directory Structure

The project has the following directory structure:

```
/login_app
│
├── app.py
└── templates
    └── login.html
```

## Code Implementation

### 1. `app.py`

This file sets up the Flask server and contains the logic for handling user authentication.

```python
from flask import Flask, render_template, request, redirect, url_for, flash, session

app = Flask(__name__)
app.secret_key = 'your_secret_key'  # Change this to a random secret key

# Simulated user database
users = {
    "user1": "password1",
    "user2": "password2"
}

@app.route('/')
def home():
    return render_template('login.html')

@app.route('/login', methods=['POST'])
def login():
    username = request.form['username']
    password = request.form['password']
    
    if username in users and users[username] == password:
        session['username'] = username
        return redirect(url_for('dashboard'))
    else:
        flash('Invalid username or password')
        return redirect(url_for('home'))

@app.route('/dashboard')
def dashboard():
    if 'username' in session:
        return f'Hello, {session["username"]}! Welcome to your dashboard.'
    return redirect(url_for('home'))

@app.route('/logout')
def logout():
    session.pop('username', None)
    return redirect(url_for('home'))

if __name__ == '__main__':
    app.run(debug=True)
```

### 2. `templates/login.html`

This is the HTML file that provides the structure for the login form.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Page</title>
</head>
<body>
    <h2>Login</h2>
    <form action="/login" method="POST">
        <label for="username">Username:</label><br>
        <input type="text" id="username" name="username" required><br><br>
        <label for="password">Password:</label><br>
        <input type="password" id="password" name="password" required><br><br>
        <input type="submit" value="Login">
    </form>

    {% with messages = get_flashed_messages() %}
      {% if messages %}
        <ul>
          {% for message in messages %}
            <li>{{ message }}</li>
          {% endfor %}
        </ul>
      {% endif %}
    {% endwith %}
</body>
</html>
```

## Running the Application

To run the application, follow these steps:

1. Create a directory named `login_app` and navigate into it.
2. Create a subdirectory named `templates` inside `login_app`.
3. Create the `app.py` file and the `login.html` file with the provided code.
4. Run the Flask application:

```bash
python app.py
```

5. Open your web browser and navigate to `http://127.0.0.1:5000/` to see the login page.

## Note

- This application is a basic example and should not be used in production as-is. For a secure application, consider implementing proper user authentication methods, password hashing, and a secure session management system.

## License

This project is licensed under the MIT License. See the LICENSE file for more information. 

---

By following this README, you should be able to set up and run the Flask login application easily!
