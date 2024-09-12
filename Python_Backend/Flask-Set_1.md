# Set-1
## Basic Questions
1. **Python Fundamentals:**

   - **What are Python’s key features, and why do you prefer using Python for backend development?**

     Python is an interpreted, high-level, general-purpose language with several features like dynamic typing, readability, a large standard library, and support for multiple programming paradigms (procedural, object-oriented, functional). For backend development, Python’s simplicity allows rapid development and scalability, while frameworks like Flask and Django provide robust features for API development.

     **Example:** Flask is lightweight, making it great for microservices. Django comes with many built-in features like ORM, user authentication, etc., saving time for developers.

   - **Explain the difference between `deepcopy` and `shallow copy` in Python.**

     A **shallow copy** creates a new object, but references to nested objects are shared between the original and the copy. A **deepcopy**, on the other hand, creates a new object and recursively copies all objects found within, ensuring no references are shared.

     **Example:**
     ```python
     import copy
     original = [[1, 2, 3], [4, 5, 6]]
     shallow = copy.copy(original)
     deep = copy.deepcopy(original)

     shallow[0][0] = 10
     print(original)  # [[10, 2, 3], [4, 5, 6]]
     deep[0][0] = 20
     print(original)  # [[10, 2, 3], [4, 5, 6]]
     ```

   - **What is the difference between lists and tuples in Python?**

     Lists are mutable, meaning they can be changed after creation (e.g., adding or removing elements), while tuples are immutable, meaning their content cannot be altered once created.

     **Example:**
     ```python
     my_list = [1, 2, 3]
     my_list.append(4)  # List can be changed
     
     my_tuple = (1, 2, 3)
     # my_tuple.append(4)  # Error: Tuples are immutable
     ```

   - **How would you handle file handling in Python? Can you give an example of reading and writing files?**

     File handling in Python can be done using the `open()` function. You can read files using `'r'` mode and write using `'w'` or `'a'` mode.

     **Example:**
     ```python
     # Writing to a file
     with open('example.txt', 'w') as file:
         file.write('Hello, World!')

     # Reading from a file
     with open('example.txt', 'r') as file:
         content = file.read()
         print(content)  # Output: Hello, World!
     ```

   - **What are Python decorators, and how would you use them in a web application?**

     A decorator in Python is a function that wraps another function to add extra functionality. They are often used in Flask for routes or adding authentication checks.

     **Example:**
     ```python
     from functools import wraps

     def login_required(f):
         @wraps(f)
         def decorated_function(*args, **kwargs):
             if not user_logged_in:
                 return 'Please log in first!'
             return f(*args, **kwargs)
         return decorated_function

     @login_required
     def view_dashboard():
         return 'Welcome to the dashboard!'
     ```

2. **Object-Oriented Programming:**

   - **Explain the four pillars of object-oriented programming (OOP).**

     - **Encapsulation:** Bundling data and methods that operate on that data within one class.
     - **Abstraction:** Hiding complex details and exposing only the necessary parts of an object.
     - **Inheritance:** Allowing one class to inherit attributes and methods from another class.
     - **Polymorphism:** Using a common interface for different underlying forms (e.g., method overloading, overriding).

   - **How does inheritance work in Python? What is the difference between single and multiple inheritance?**

     In Python, a class can inherit attributes and methods from a parent class. **Single inheritance** involves one parent class, while **multiple inheritance** involves multiple parent classes.

     **Example:**
     ```python
     class Animal:
         def speak(self):
             return "Animal sound"

     class Dog(Animal):  # Single Inheritance
         def speak(self):
             return "Bark!"

     class Cat(Animal):
         def speak(self):
             return "Meow!"

     class Hybrid(Dog, Cat):  # Multiple Inheritance
         pass
     ```

   - **What is method overloading and method overriding in Python?**

     - **Method overloading** is not directly supported in Python, but you can achieve it by using default arguments.
     - **Method overriding** occurs when a child class provides a specific implementation for a method that is already defined in its parent class.

     **Example:**
     ```python
     class Parent:
         def show(self):
             return "Parent class"

     class Child(Parent):
         def show(self):  # Overriding
             return "Child class"
     ```

3. **Basic Web Development with Python Flask:**

   - **What is Python Flask, and why would you use it in a project?**

     Flask is a micro web framework written in Python. It is lightweight and modular, making it easy to scale for small to medium web applications. It allows developers to quickly set up RESTful APIs without boilerplate code.

   - **How do you handle user authentication in Flask?**

     Flask provides extensions like `Flask-Login` for managing user sessions. You can handle authentication via forms, cookies, JWT, or OAuth.

     **Example:**
     ```python
     from flask import Flask, render_template, redirect, url_for, session

     @app.route('/login', methods=['POST'])
     def login():
         session['user'] = request.form['username']
         return redirect(url_for('dashboard'))
     ```

   - **Can you explain the role of blueprints in Flask?**

     Blueprints in Flask allow you to organize your application into reusable modules. They help in structuring large applications by grouping routes, templates, and static files.

     **Example:**
     ```python
     from flask import Blueprint

     user_blueprint = Blueprint('user', __name__)

     @user_blueprint.route('/profile')
     def profile():
         return 'User profile page'

     # Register blueprint
     app.register_blueprint(user_blueprint, url_prefix='/user')
     ```

4. **Databases and SQL:**

   - **What is the difference between SQL and NoSQL databases? When would you choose one over the other?**

     - **SQL databases** (e.g., MySQL, PostgreSQL) are relational and use structured query language for defining and manipulating data. They are ideal when data integrity, relationships, and complex querying are required.
     - **NoSQL databases** (e.g., MongoDB, Cassandra) are non-relational, schema-less, and store data in formats like key-value pairs, documents, or wide-column stores. They are used for unstructured data, scaling horizontally, and handling large datasets.

     You would choose **SQL** for transactional systems and **NoSQL** for distributed, large-scale applications like social media or real-time analytics.

   - **How would you optimize a SQL query for faster performance?**

     - Use **indexes** to speed up query lookups.
     - Avoid **SELECT \***, query only the necessary columns.
     - Use **JOINs** judiciously and avoid unnecessary joins.
     - Optimize by caching frequently queried data.
     - Analyze the query execution plan.

     **Example:**
     ```sql
     EXPLAIN ANALYZE SELECT name, age FROM users WHERE age > 30;
     ```

   - **What are indexes in databases, and how do they improve performance?**

     Indexes are database structures that allow faster retrieval of rows by creating a key lookup. By indexing frequently queried columns, the database can avoid scanning the entire table.

     **Example:**
     ```sql
     CREATE INDEX idx_age ON users(age);
     ```

## Intermediate Questions

1. **Backend Development & API Design:**

   - **Can you walk me through how you would design a RESTful API in Python using Flask?**

     To design a RESTful API in Flask, follow these steps:
     1. **Setup Flask:** Install Flask and set up the basic application structure.
     2. **Define Endpoints:** Use Flask routes to define API endpoints (GET, POST, PUT, DELETE).
     3. **Data Handling:** Utilize request data and responses. Use JSON for data interchange.
     4. **Error Handling:** Implement error handling and validation.
     5. **Documentation:** Use tools like Swagger for API documentation.

     **Example:**
     ```python
     from flask import Flask, jsonify, request

     app = Flask(__name__)

     tasks = [
         {'id': 1, 'title': 'Learn Python', 'done': False},
         {'id': 2, 'title': 'Build Flask API', 'done': False}
     ]

     @app.route('/tasks', methods=['GET'])
     def get_tasks():
         return jsonify({'tasks': tasks})

     @app.route('/tasks/<int:task_id>', methods=['GET'])
     def get_task(task_id):
         task = next((task for task in tasks if task['id'] == task_id), None)
         if task is None:
             return jsonify({'error': 'Task not found'}), 404
         return jsonify({'task': task})

     if __name__ == '__main__':
         app.run(debug=True)
     ```

   - **How do you ensure that your APIs are scalable and secure?**

     - **Scalability:** Use load balancers to distribute traffic, implement caching mechanisms (e.g., Redis), and consider database sharding.
     - **Security:** Implement authentication (e.g., JWT), use HTTPS, validate inputs to prevent injection attacks, and ensure proper authorization checks.

   - **What is CORS, and how do you handle it in your web applications?**

     **Cross-Origin Resource Sharing (CORS)** is a security feature that restricts how resources on a web page can be requested from another domain. To handle CORS in Flask, use the `flask-cors` extension to allow specific domains.

     **Example:**
     ```python
     from flask_cors import CORS
     from flask import Flask

     app = Flask(__name__)
     CORS(app, resources={r"/*": {"origins": "*"}})

     @app.route('/')
     def home():
         return 'CORS is enabled for all origins'
     ```

   - **Explain the process of Extract, Transform, Load (ETL) and how you have implemented it in your projects.**

     - **Extract:** Collect data from various sources (e.g., databases, APIs).
     - **Transform:** Clean and format the data according to requirements.
     - **Load:** Insert the transformed data into the target database or data warehouse.

     **Example:** In a project, you might use Python scripts with libraries like `pandas` for transformation and `SQLAlchemy` for loading data into a SQL database.

     ```python
     import pandas as pd
     from sqlalchemy import create_engine

     # Extract
     data = pd.read_csv('data.csv')

     # Transform
     data['new_column'] = data['old_column'] * 2

     # Load
     engine = create_engine('sqlite:///mydatabase.db')
     data.to_sql('table_name', engine, if_exists='replace')
     ```

   - **How do you handle data transformation in Python? Any specific libraries you prefer?**

     Data transformation can be handled using libraries like `pandas` for data manipulation, `numpy` for numerical operations, and `dask` for handling large datasets.

     **Example:**
     ```python
     import pandas as pd

     data = pd.read_csv('data.csv')
     data['new_column'] = data['existing_column'].apply(lambda x: x * 10)
     ```

2. **Data Structures and Algorithms:**

   - **What are some common Python libraries used for data structures and algorithms?**

     Common libraries include:
     - `collections` for specialized container datatypes (e.g., `deque`, `Counter`).
     - `heapq` for heap queue algorithms.
     - `sortedcontainers` for sorted list, dict, and set data structures.

   - **How would you implement a binary search in Python?**

     Binary search is an efficient algorithm for finding an item in a sorted list by repeatedly dividing the search interval in half.

     **Example:**
     ```python
     def binary_search(arr, target):
         left, right = 0, len(arr) - 1
         while left <= right:
             mid = (left + right) // 2
             if arr[mid] == target:
                 return mid
             elif arr[mid] < target:
                 left = mid + 1
             else:
                 right = mid - 1
         return -1
     ```

   - **What are Python’s built-in data structures, and when would you use each of them?**

     - **List:** Ordered, mutable collection of items. Used for maintaining a collection of items in a specific order.
     - **Tuple:** Ordered, immutable collection of items. Used when you need a fixed collection of items.
     - **Set:** Unordered collection of unique items. Used for membership tests and eliminating duplicates.
     - **Dictionary:** Unordered collection of key-value pairs. Used for fast lookups by key.

     **Example:**
     ```python
     my_list = [1, 2, 3]
     my_tuple = (1, 2, 3)
     my_set = {1, 2, 3}
     my_dict = {'key1': 'value1', 'key2': 'value2'}
     ```

3. **Deployment and Cloud Technologies:**

   - **How do you deploy a Flask application on AWS or Azure?**

     - **AWS:** Use AWS Elastic Beanstalk for easy deployment, or set up an EC2 instance and deploy your Flask application manually using a WSGI server like Gunicorn.
     - **Azure:** Use Azure App Service to deploy your Flask application, or set up a virtual machine and deploy manually.

     **Example for AWS Elastic Beanstalk:**
     1. Package your Flask app with a `requirements.txt` and `application.py`.
     2. Deploy using the AWS Elastic Beanstalk CLI.

   - **What is your experience with using Docker or Kubernetes for backend applications?**

     **Docker** is used to containerize applications, making them portable and consistent across environments. **Kubernetes** is used to orchestrate and manage containerized applications.

     **Example:**
     ```dockerfile
     # Dockerfile for a Flask app
     FROM python:3.8-slim
     WORKDIR /app
     COPY requirements.txt requirements.txt
     RUN pip install -r requirements.txt
     COPY . .
     CMD ["python", "app.py"]
     ```

     **Example Kubernetes Deployment:**
     ```yaml
     apiVersion: apps/v1
     kind: Deployment
     metadata:
       name: flask-app
     spec:
       replicas: 3
       selector:
         matchLabels:
           app: flask-app
       template:
         metadata:
           labels:
             app: flask-app
         spec:
           containers:
           - name: flask-app
             image: my-flask-app:latest
             ports:
             - containerPort: 5000
     ```

   - **What is the role of a load balancer in a backend infrastructure?**

     A load balancer distributes incoming network traffic across multiple servers to ensure no single server becomes overwhelmed. It improves availability and reliability by balancing the load and providing failover in case of server failures.

4. **Security Best Practices:**

   - **What security measures would you implement in a Flask application to prevent SQL injection?**

     - Use **parameterized queries** or **ORMs** like SQLAlchemy to avoid directly embedding user input into SQL queries.
     - Validate and sanitize user inputs.
     - Use **prepared statements**.

     **Example with SQLAlchemy:**
     ```python
     from sqlalchemy.orm import sessionmaker

     Session = sessionmaker(bind=engine)
     session = Session()
     result = session.execute("SELECT * FROM users WHERE username = :username", {'username': user_input})
     ```

   - **How do you handle sensitive information, like passwords, in web applications?**

     - Use **hashing algorithms** like bcrypt to store passwords securely.
     - Implement **secure password policies**.
     - Use **environment variables** to store sensitive configurations.

     **Example with bcrypt:**
     ```python
     from flask_bcrypt import Bcrypt
     bcrypt = Bcrypt()

     password_hash = bcrypt.generate_password_hash('my_password').decode('utf-8')
     is_valid = bcrypt.check_password_hash(password_hash, 'my_password')
     ```

   - **What is CSRF, and how do you prevent it in Python web applications?**

     **Cross-Site Request Forgery (CSRF)** is an attack that tricks users into performing actions they didn’t intend. Prevent CSRF by using anti-CSRF tokens and validating them on the server side.

     **Example with Flask-WTF:**
     ```python
     from flask_wtf import FlaskForm
     from wtforms import StringField, SubmitField
     from wtforms.validators import DataRequired

     class MyForm(FlaskForm):
         name = StringField('Name', validators=[DataRequired()])
         submit = SubmitField('Submit')


     ```

## Advanced Questions
1. **Performance Optimization:**

   - **How do you profile and optimize the performance of a Flask application?**

     - **Profiling:** Use tools like **Flask-DebugToolbar** or **cProfile** to identify performance bottlenecks.
     - **Optimization:** Optimize database queries, use caching, and minimize resource-heavy operations.

     **Example with Flask-DebugToolbar:**
     ```python
     from flask_debugtoolbar import DebugToolbarExtension
     app.debug = True
     app.config['DEBUG_TB_INTERCEPT_REDIRECTS'] = False
     toolbar = DebugToolbarExtension(app)
     ```

   - **What are some best practices for improving the scalability of a web application?**

     - **Database Scaling:** Use read replicas and partitioning.
     - **Caching:** Implement caching layers (e.g., Redis).
     - **Microservices:** Break down the application into smaller, manageable services.
     - **Load Balancing:** Distribute traffic across multiple servers.

   - **Can you explain the concept of horizontal vs. vertical scaling?**

     - **Horizontal Scaling:** Adding more servers to handle increased load. It distributes the load across multiple machines.
     - **Vertical Scaling:** Increasing the resources (CPU, RAM) of a single server. It involves upgrading the server to handle more load.

     **Example:** Horizontal scaling involves adding more instances of your web server, while vertical scaling might involve upgrading your existing server to a more powerful instance.

2. **Testing and Quality Assurance:**

   - **How do you write unit tests for a Flask application?**

     - Use **unittest** or **pytest** for writing tests.
     - Create test cases for your views, models, and forms.
     - Use **Flask testing utilities** to simulate requests and check responses.

     **Example with pytest:**
     ```python
     import pytest
     from app import app

     @pytest.fixture
     def client():
         app.config['TESTING'] = True
         return app.test_client()

     def test_home(client):
         response = client.get('/')
         assert b'Welcome to the home page' in response.data
     ```

   - **What is the importance of integration testing, and how do you perform it in Flask?**

     **Integration testing** ensures that different parts of the application work together correctly. Use tools like **pytest** or **Flask’s test client** to perform integration tests by simulating real-world scenarios.

     **Example:**
     ```python
     def test_login(client):
         response = client.post('/login', data={'username': 'test', 'password': 'password'})
         assert response.status_code == 200
         assert b'Welcome test' in response.data
     ```

   - **How do you handle continuous integration and deployment (CI/CD) for a Python application?**

     - Use CI/CD tools like **GitHub Actions**, **Travis CI**, or **Jenkins** to automate testing and deployment.
     - Set up pipelines to run tests, build Docker images, and deploy to staging or production environments.

     **Example GitHub Actions workflow:**
     ```yaml
     name: CI

     on: [push]

     jobs:
       build:
         runs-on: ubuntu-latest

         steps:
         - uses: actions/checkout@v2
         - name: Set up Python
           uses: actions/setup-python@v2
           with:
             python-version: '3.8'
         - name: Install dependencies
           run: |
             pip install -r requirements.txt
         - name: Run tests
           run: |
             pytest
     ```

3. **Advanced Framework Features:**

   - **How would you use Flask extensions to add functionality to your application?**

     Flask extensions provide additional features to Flask applications, such as authentication, database integration, and form handling.

     **Example:** Using `Flask-Login` for user session management.
     ```python
     from flask_login import LoginManager

     login_manager = LoginManager()
     login_manager.init_app(app)
     ```

   - **Can you explain how you would implement and manage background tasks in a Flask application?**

     Use task queues like **Celery** with a message broker (e.g., RabbitMQ, Redis) for managing background tasks.

     **Example with Celery:**
     ```python
     from celery import Celery

     celery = Celery('tasks', broker='redis://localhost:6379/0')

     @celery.task
     def add(x, y):
         return x + y
     ```

   - **What is your approach to handling large-scale data processing in a Flask application?**

     For large-scale data processing, consider:
     - Using **distributed computing** frameworks like **Apache Spark**.
     - Offloading heavy processing to **background tasks** using Celery.
     - **Optimizing data queries** and using efficient data formats.
