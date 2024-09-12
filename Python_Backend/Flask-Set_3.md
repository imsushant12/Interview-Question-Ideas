
# Set-3
**1. What is WSGI in terms of Python Flask?**  
WSGI (Web Server Gateway Interface) is a specification for web servers to communicate with Python web applications. Flask is a WSGI-compliant framework, meaning it can interface with a WSGI server to handle HTTP requests. WSGI acts as a middleware between the web server and the Flask application, making the app serve requests in a standard and efficient way.

**2. What is Werkzeug in Flask?**  
Werkzeug is a comprehensive WSGI utility library used by Flask. It provides essential functionality such as URL routing, request handling, and debugging. Flask uses Werkzeug internally for many operations, allowing developers to focus on building their applications without worrying about low-level HTTP protocol details.

**3. What is Jinja and why use it?**  
Jinja is a templating engine in Flask that allows the separation of HTML from Python code. It helps in generating dynamic HTML by embedding Python-like expressions within HTML templates. Jinja makes it easier to create web pages dynamically by inserting variables, loops, and conditional logic into the templates.

**4. What is a session in Flask and how to use it?**  
A session in Flask is a way to store data across different requests for a specific user. Flask sessions store data client-side using a secure cookie, encrypted with a secret key. Sessions are used to maintain the state of the user, like keeping them logged in, between multiple requests. It can be used by importing the `session` object from Flask and storing data in it like a dictionary.

```python
from flask import session
session['username'] = 'John'
```

**5. How does memory management work in Python and Python Flask?**  
Python uses automatic memory management with garbage collection. It tracks object references using reference counting and collects cyclic references through its garbage collector. Flask, being a Python framework, follows the same memory management principles, relying on Python’s garbage collector to free up memory for unused objects.

**6. What is pickling and unpickling and when to use them?**  
Pickling is the process of converting a Python object into a byte stream to save it to a file or transfer it over a network. Unpickling is the reverse process—converting the byte stream back to a Python object. It’s used for object serialization when you want to persist Python objects or transfer them across different environments.

**7. What is a blueprint in Python Flask?**  
A blueprint in Flask is a way to organize large applications by breaking them into smaller, reusable modules. It helps in structuring an application into components (like authentication, admin panel, etc.) that can be registered with a Flask app. Blueprints make the development process more modular and maintainable.

**8. What is Flask-WTF?**  
Flask-WTF is an extension for Flask that integrates the WTForms library with Flask. It simplifies handling web forms by providing built-in validation, CSRF protection, and custom error handling. Flask-WTF is helpful for creating secure, manageable forms with minimal code.

**9. What are RESTful APIs and why use them?**  
RESTful APIs (Representational State Transfer) are web services that conform to REST architecture principles. They use HTTP methods like GET, POST, PUT, and DELETE to operate on resources. RESTful APIs are widely used because they are stateless, scalable, and simple to implement, making them ideal for building web services that interact with clients via standard HTTP methods.

**10. How is horizontal scaling different from vertical scaling?**  
Horizontal scaling refers to adding more machines (or nodes) to handle increasing load, while vertical scaling involves upgrading the existing machine (e.g., adding more CPU or RAM). Horizontal scaling is more flexible and better for distributed systems, while vertical scaling has physical limitations.

**11. What is Flask-Login and why use it?**  
Flask-Login is an extension that manages user sessions in a Flask application. It simplifies tasks like logging users in and out, handling session cookies, and restricting access to certain views for authenticated users. It's useful when you need to implement authentication without writing a lot of boilerplate code.

**12. What is Flask-JWT and what exactly is JWT and why use it?**  
Flask-JWT is an extension that provides JSON Web Token (JWT) authentication for Flask applications. JWT is a compact, self-contained token used to verify the identity of users and secure data transmission between parties. It’s widely used in APIs for stateless authentication, where each request contains a token rather than relying on server-side sessions.

**13. What is CORS and why use it?**  
CORS (Cross-Origin Resource Sharing) is a security feature implemented in web browsers to prevent unauthorized cross-origin HTTP requests. In Flask, enabling CORS allows your app to accept requests from other domains, which is essential for applications where the frontend and backend are hosted on different servers.

**14. What is the difference between `is` and `==`?**  
The `is` operator checks if two objects are the same object in memory (i.e., identity comparison). In contrast, `==` checks if two objects have the same value (i.e., value comparison). For example:
```python
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b)  # True (same value)
print(a is b)  # False (different objects in memory)
```

**15. What is the difference between shallow copy and deep copy?**  
A shallow copy creates a new object but references the elements of the original object (if they are mutable), while a deep copy creates a completely independent copy of both the object and its elements. In Python, you can use the `copy` module for shallow (`copy.copy()`) and deep copies (`copy.deepcopy()`).


**16. What is the difference between an array and a list in Python?**  
An array in Python (from the `array` module) is a collection of elements of the same type and is optimized for numerical operations. A list, on the other hand, is a more flexible built-in data structure that can contain elements of any type, making it more versatile but less memory-efficient for homogeneous data.

**17. Is Python flask MVC or MVT?**  
Flask follows the **MVC (Model-View-Controller)** pattern, although it’s often referred to as an **MVT (Model-View-Template)** pattern in Django.

In Flask:
- **Model**: Represents the data layer, often handled using databases like SQLAlchemy (an ORM tool) or any other database handling system.
- **View**: Refers to the function or logic that handles user requests and returns the response (HTML, JSON, etc.).
- **Controller**: This is the application logic, often encapsulated within view functions that control what data (model) is passed to the view (template) and how it's processed.

Flask doesn’t enforce this architecture strictly, giving developers flexibility in organizing the code, but it's more closely aligned with the MVC pattern, where the "View" in Flask corresponds to templates that render HTML. So, **Flask is an MVC framework**, but due to its flexibility, the terminology and structure can be adapted based on how the developer chooses to organize their application.
