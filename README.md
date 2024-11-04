# EX-09-Restful-and-Soap-Installation-Overview

## Aim 

To create a simple RESTful API built with Flask that adds two numbers using GET or POST requests. It can handle both JSON and URL parameters to perform addition.

# Addition API with Flask - README

This is a simple RESTful API built with Flask that adds two numbers using GET or POST requests. It can handle both JSON and URL parameters to perform addition.

## Prerequisites

Before running the project, ensure you have the following installed:

1. **Python** (version 3.6 or above)
2. **pip** (Python package manager)
3. **Flask** (Python web framework)

## Project Setup

### 1. Install Flask

If Flask is not already installed, you can install it via pip:

```
pip install Flask
```

### 2. Project Files

Create a Python file (e.g., app.py) and paste the following code into it:

```
from flask import Flask, request, jsonify

app = Flask(__name__)

# Route to add two numbers
@app.route('/add', methods=['GET', 'POST'])
def add_numbers():
    if request.method == 'POST':
        # Get JSON data from request
        data = request.get_json()
        num1 = data.get('num1')
        num2 = data.get('num2')
    else:  # For GET requests, get parameters from the query string
        num1 = request.args.get('num1', type=float)
        num2 = request.args.get('num2', type=float)

    # Check if both numbers are provided
    if num1 is None or num2 is None:
        return jsonify({"error": "Please provide both num1 and num2"}), 400
    
    # Return the result of the addition
    result = num1 + num2
    return jsonify({"num1": num1, "num2": num2, "result": result})

# Root route (Optional)
@app.route('/')
def home():
    return "Welcome to the Addition API! Use the /add endpoint to add two numbers."

if __name__ == '__main__':
    app.run(debug=True)
```

### 3. Running the API

To start the Flask development server, open the terminal or command prompt and run the following command in the project directory:

```
python app.py
```

### Output

![Screenshot 2024-10-23 113402](https://github.com/user-attachments/assets/0fb6811c-9821-4231-8699-a71ee0c7afba)

By default, the API will run on http://127.0.0.1:5000/.


### 4. Testing the API

### Using GET Request

You can also test the API using a browser or tools like curl for GET requests. Example:

```
curl "http://127.0.0.1:5000/add?num1=5&num2=10"
```

### Expected Output (JSON):

```
PS G:\VCC\RESTFUL> curl "http://127.0.0.1:5000/add?num1=5&num2=10"
StatusCode        : 200                                                                                                                               
StatusDescription : OK                                                                                                                                
Content           : {
                      "num1": 5.0,
                      "num2": 10.0,
                      "result": 15.0
                    }
```

![image](https://github.com/user-attachments/assets/72c679c8-806b-4ceb-8cb5-394075ca9970)


### Using POST Request
(via Invoke-RestMethod PowerShell)
You can test the API using PowerShell with a POST request:

```
Invoke-RestMethod -Uri http://127.0.0.1:5000/add -Method POST -Body '{"num1": 5, "num2": 10}' -ContentType "application/json"
```

### Expected Output:

```
num1 num2 result
---- ---- ------
   5   10     15
```

![Screenshot 2024-10-23 113341](https://github.com/user-attachments/assets/8b122695-1884-4dcf-b090-a7e6b2f8f247)



### Conclusion

This simple Flask-based REST API demonstrates how to handle both GET and POST requests to perform an addition operation. You can expand this to handle more complex operations or features as needed.
