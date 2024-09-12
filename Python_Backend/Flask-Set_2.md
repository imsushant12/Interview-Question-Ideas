# Set-2
## Beginner Level Questions
1. **What is the difference between synchronous and asynchronous programming in Python?**

   - **Synchronous programming**: Tasks are executed one at a time, waiting for each to complete before moving to the next.
   - **Asynchronous programming**: Allows tasks to run in the background, not waiting for one to finish before starting the next, making it suitable for I/O-bound operations.

   **Example**: In Python, you can use the `asyncio` module for asynchronous programming.

   ```python
   import asyncio

   async def fetch_data():
       await asyncio.sleep(2)  # Simulate I/O operation
       return "Data fetched"

   async def main():
       result = await fetch_data()
       print(result)

   asyncio.run(main())
   ```

2. **Explain what a RESTful API is.**

   A **RESTful API** is an architectural style for building web services. REST stands for **Representational State Transfer**, and it uses HTTP methods like `GET`, `POST`, `PUT`, and `DELETE` to perform operations on resources represented by URIs. 

   **Key features**:
   - **Stateless**: Each request from the client to the server must contain all the information needed to understand and process the request.
   - **Scalability**: Due to its stateless nature, it can handle large amounts of requests.
   - **Uniform Interface**: It follows standard HTTP methods and status codes.

   **Example**:
   - `GET /users/`: Retrieves a list of users.
   - `POST /users/`: Creates a new user.

3. **What is CORS, and why is it important in web development?**

   **CORS** stands for **Cross-Origin Resource Sharing**. It is a security feature implemented in web browsers to restrict how resources on a web page can be requested from another domain.

   **Importance**:
   - CORS prevents malicious websites from accessing sensitive information from other domains via JavaScript.
   - It’s crucial for protecting APIs from unauthorized use.

   **In Flask**:
   ```python
   from flask import Flask
   from flask_cors import CORS

   app = Flask(__name__)
   CORS(app)  # Enables CORS for the entire app
   ```


4. **What are Python decorators, and how are they useful in web development?**

   **Answer**:
   - A **decorator** is a function that modifies the behavior of another function or method without changing its actual code.
   - In web development, decorators can be used to add functionality like logging, authentication, or rate-limiting to routes or views in frameworks like Flask or Django.

   **Example**: Adding a simple logging decorator.
   ```python
   def log_decorator(func):
       def wrapper(*args, **kwargs):
           print(f"Calling {func.__name__}")
           return func(*args, **kwargs)
       return wrapper

   @log_decorator
   def hello_world():
       print("Hello World")

   hello_world()
   ```


5. **What are Python's built-in data structures, and when would you use each?**

   **Answer**:
   Python has several built-in data structures, each with specific use cases:
   - **List**: An ordered, mutable sequence used when you need to store elements in order and may need to modify them.
   - **Tuple**: An ordered, immutable sequence, typically used when you want to store data that should not change.
   - **Dictionary**: A key-value pair structure, used when you need to quickly look up data via keys.
   - **Set**: An unordered collection of unique elements, useful for eliminating duplicates.

   **Example**:
   ```python
   my_list = [1, 2, 3]
   my_tuple = (1, 2, 3)
   my_dict = {'name': 'Alice', 'age': 25}
   my_set = {1, 2, 3, 1}  # Duplicates removed, set is {1, 2, 3}
   ```

6. **What is the difference between Flask and Django?**

   **Answer**:
   - **Flask**: A micro-framework that provides the basic components needed for web development but leaves decisions about structure, database, etc., to the developer.
   - **Django**: A full-featured web framework that comes with built-in features like authentication, an ORM (Object-Relational Mapping), and an admin interface.

   **When to use Flask**: For smaller or highly customized projects.
   **When to use Django**: For larger applications that need rapid development and built-in features.

## Intermediate Level Questions
1. **How would you implement authentication and authorization in Flask?**

   - **Authentication** is about verifying the identity of a user (who they are).
   - **Authorization** is about determining what actions a user is allowed to perform (what they can do).

   In Flask, authentication can be handled using **Flask-Login** or **JWT (JSON Web Tokens)**. Authorization can be implemented by checking user roles after authentication.

   **Example** with JWT:
   ```python
   from flask import Flask, jsonify, request
   import jwt
   import datetime

   app = Flask(__name__)
   app.config['SECRET_KEY'] = 'your_secret_key'

   @app.route('/login', methods=['POST'])
   def login():
       auth = request.form
       if auth and auth['username'] == 'admin' and auth['password'] == 'admin':
           token = jwt.encode({'user': auth['username'], 'exp': datetime.datetime.utcnow() + datetime.timedelta(hours=1)},
                              app.config['SECRET_KEY'])
           return jsonify({'token': token})
       return 'Login failed'

   @app.route('/protected', methods=['GET'])
   def protected():
       token = request.headers['Authorization'].split(" ")[1]
       try:
           jwt.decode(token, app.config['SECRET_KEY'])
           return 'Access granted'
       except:
           return 'Invalid token'
   ```

2. **In Mongoose (MongoDB), we define a schema. Why is a schema not always required in NoSQL databases?**

   Unlike traditional relational databases, **NoSQL databases** like MongoDB are **schema-less**, meaning data can be stored in a flexible, non-tabular format (usually as JSON documents). 

   **Reason**:
   - NoSQL databases are designed to handle unstructured or semi-structured data, and they can easily accommodate changes in the structure of data over time.
   - While **schemas** can be defined in tools like **Mongoose** (to enforce some structure), it's not mandatory because the database itself doesn't impose strict rules.

   **Example**:
   - MongoDB allows documents in the same collection to have different fields.

3. **What are Blueprints in Flask, and how do they help in structuring larger applications?**

   **Blueprints** in Flask are a way to organize your application into modular components. They allow you to define parts of the app separately and register them to the main app later. This is especially useful in large applications to keep the codebase manageable.

   **Usage**:
   - Separate the app into modules like `auth`, `admin`, etc.
   - Each module can have its routes, templates, and static files.

   **Example**:
   ```python
   from flask import Blueprint

   auth_bp = Blueprint('auth', __name__)

   @auth_bp.route('/login')
   def login():
       return "Login page"
   ```

   In the main app:
   ```python
   from flask import Flask
   from auth import auth_bp

   app = Flask(__name__)
   app.register_blueprint(auth_bp)

   if __name__ == '__main__':
       app.run()
   ```
4. **How does Flask handle session management?**

   **Answer**:
   Flask uses **secure cookies** for session management. Each user gets a session that stores data (like user preferences or login status) on the client side, while the server signs the session cookie to ensure it has not been tampered with.

   **Example**:
   ```python
   from flask import Flask, session

   app = Flask(__name__)
   app.secret_key = 'supersecretkey'

   @app.route('/')
   def index():
       session['username'] = 'JohnDoe'
       return "Session set!"

   @app.route('/getsession')
   def getsession():
       return f"Logged in as {session['username']}"
   ```

5. **What is Gunicorn, and why is it used in deploying Flask applications?**

   **Answer**:
   **Gunicorn** (Green Unicorn) is a Python WSGI HTTP server that serves Flask (or other Python web applications) in production environments. It allows you to run multiple worker processes, enabling the app to handle more requests concurrently.

   **Why Gunicorn**:
   - Flask’s built-in server is not suitable for production due to performance and security concerns.
   - Gunicorn provides scalability and reliability in handling traffic spikes.

   **Command to run**:
   ```bash
   gunicorn app:app --workers 3
   ```

## Advanced Level Questions
1. **How would you implement horizontal scaling for a Python Flask web application?**

   Horizontal scaling involves adding more instances of your application across multiple servers (as opposed to vertical scaling, which means upgrading the hardware of a single server).

   **Steps**:
   - **Containerization**: Use **Docker** to package your Flask app.
   - **Load Balancing**: Use a load balancer (like **Nginx** or a cloud service like AWS ELB) to distribute traffic across multiple instances of your Flask app.
   - **Database considerations**: Ensure your database can handle increased load, possibly using replication or sharding for NoSQL databases.

   **Example** with Docker:
   - Create a `Dockerfile` to containerize your Flask app.
   - Use **Docker Compose** or **Kubernetes** to manage multiple instances of your app.


2. **Explain the pros and cons of using an ORM like SQLAlchemy in a Python web application.**

   **Pros**:
   - **Abstraction**: ORMs abstract away complex SQL queries, allowing developers to work with Python objects instead of raw SQL.
   - **Portability**: Since SQLAlchemy is database-agnostic, the same code can be used for different databases (e.g., MySQL, PostgreSQL).
   - **Security**: Reduces the risk of SQL injection by escaping user inputs.

   **Cons**:
   - **Performance**: ORMs can be slower than writing raw SQL, especially for complex queries.
   - **Learning curve**: It can be harder to optimize queries when you're not familiar with the underlying SQL being generated.

   **Example**:
   ```python
   from flask_sqlalchemy import SQLAlchemy
   db = SQLAlchemy(app)

   class User(db.Model):
       id = db.Column(db.Integer, primary_key=True)
       username = db.Column(db.String(80))

   user = User(username='John')
   db.session.add(user)
   db.session.commit()
   ```

3. **How do you ensure the security of sensitive data (like passwords) in a Flask application?**

   **Steps**:
   - **Use hashing algorithms** to store passwords (never store plain-text passwords). Libraries like `bcrypt` or `werkzeug.security` can be used.
   - **Use HTTPS** for secure communication between the client and the server.
   - **Environment variables**: Store sensitive information (e.g., API keys, database credentials) in environment variables, not in your codebase.

   **Example**:
   ```python
   from werkzeug.security import generate_password_hash, check_password_hash

   hashed_password = generate_password_hash('mypassword')
   if check_password_hash(hashed_password, 'mypassword'):
       print("Password matches")
   ```
4. **How would you design a highly scalable and fault-tolerant architecture for a Python-based web application?**

   **Answer**:
   - **Horizontal scaling**: Use containers (like Docker) or VM instances for each microservice and deploy them across multiple nodes to handle high traffic.
   - **Load balancing**: Use a load balancer (e.g., AWS ELB, Nginx) to distribute requests evenly across multiple instances.
   - **Database**: Use a distributed database (e.g., PostgreSQL with replication, or a NoSQL solution like MongoDB with sharding).
   - **Caching**: Implement caching using services like Redis or Memcached to reduce database load.
   - **Monitoring**: Integrate logging and monitoring tools like Prometheus or Grafana to detect failures and bottlenecks early.
   - **CI/CD pipeline**: Automate deployments using tools like Jenkins, CircleCI, or GitHub Actions for seamless updates and rollbacks.

5. **What are Python context managers, and how do they work with the `with` statement?**

   **Answer**:
   **Context managers** in Python are constructs that allow you to allocate and release resources precisely when needed. They are commonly used for resource management like opening and closing files or database connections.

   **The `with` statement** ensures that the resource is properly cleaned up after use, even if an exception occurs during processing.

   **Example**:
   ```python
   with open('file.txt', 'r') as file:
       data = file.read()
   # File automatically closed here
   ```

   **Custom Context Manager**:
   ```python
   class FileManager:
       def __enter__(self):
           self.file = open('file.txt', 'r')
           return self.file

       def __exit__(self, exc_type, exc_val, exc_tb):
           self.file.close()

   with FileManager() as file:
       data = file.read()
   ```

6. **How would you handle high availability in a Python web application with a database layer?**

   **Answer**:
   High availability means ensuring the application is always up and running, even in the event of failures. 

   **Approaches**:
   - **Database replication**: Use primary-replica setups for databases like PostgreSQL or MongoDB. If the primary node fails, the replica can take over.
   - **Load balancing**: Spread traffic across multiple instances of your app and database using load balancers to avoid a single point of failure.
   - **Automatic failover**: Implement tools like **pgBouncer** for PostgreSQL or built-in failover mechanisms in NoSQL databases like MongoDB.
   - **Backup strategies**: Regular backups are necessary to restore service in case of catastrophic failure. Automated backups in cloud services can ensure data recovery.

7.  **What are the advantages and challenges of using WebSockets for real-time communication in Python applications?**

   **Answer**:
   **Advantages**:
   - **Real-time updates**: WebSockets allow real-time bidirectional communication, making them perfect for chat applications, live updates, or gaming platforms.
   - **Low latency**: Since the connection remains open, there is less overhead compared to traditional HTTP polling.

   **Challenges**:
   - **Scaling**: WebSocket connections are persistent, which can create scaling challenges as the number of concurrent users increases.
   - **Security**: Securing WebSockets with SSL (WSS) is essential, as they are vulnerable to man-in-the-middle attacks.
   - **Concurrency**: Handling thousands of concurrent WebSocket connections requires proper server setup and event-loop architectures like **asyncio** or frameworks like **Sanic** or **Django Channels**.

   **Example**:
   Using **Flask-SocketIO**:
   ```python
   from flask import Flask, render_template
   from flask_socketio import SocketIO, emit

   app = Flask(__name__)
   socketio = SocketIO(app)

   @socketio.on('message')
   def handle_message(msg):
       print(f"Message: {msg}")
       emit('response', {'data': 'Message received!'}, broadcast=True)

   if __name__ == '__main__':
       socketio.run(app)
   ```
