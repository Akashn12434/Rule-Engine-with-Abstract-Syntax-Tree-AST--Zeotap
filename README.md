### Rule Engine with Abstract Syntax Tree (AST)
# Objective
The aim of this project is to build a three-tier rule engine application with a user-friendly interface (UI), an API layer, and a backend. This application evaluates user eligibility based on attributes like age, department, income, and spending by using rules represented as an Abstract Syntax Tree (AST). The rules can be dynamically created, combined, and modified.

### Table of Contents
Objective

How to Run the Application

Data Structure

Data Storage

API Design

Test Cases

Bonus Features

Non-Functional Requirements




1. Project Overview

This rule engine empowers users to dynamically define and update rules using an AST structure.
###  Key features of the application include:

Creation and storage of conditional rules based on user attributes.

Merging multiple rules into a single AST.

Evaluation of user eligibility by processing the rules against provided data.

Storage of rules and metadata in an SQL database.


### Technologies Used
Backend Framework: Flask (Python)

Frontend: HTML, CSS, JavaScript (if required)

Database: SQLite with SQLAlchemy ORM

Additional Libraries:

SQLAlchemy (for ORM)

Werkzeug (for API management)

### Setup and Installation
1. Clone the Repository
git clone https://github.com/Akashn12434/Rule-Engine-with-AST.git

cd Rule-Engine-with-AST

2. Create a Virtual Environment

python -m venv venv


venv\Scripts\activate      # For Windows

3. Install Dependencies

pip install -r requirements.txt

4. Run the Application:

python app.py  # Replace 'app.py' with the correct entry point if necessary

The application will be available at: http://127.0.0.1:5000.


### Rule Engine API Endpoints
Create Rule

Endpoint: /create_rule

Method: POST

Description: Accepts a rule string and returns its AST representation.

Combine Rules

Endpoint: /combine_rules

Method: POST

Description: Merges a list of rules into a unified AST for evaluation.

2. Data Structure

The rule engine utilizes a Node class to construct the AST. Here’s a basic example of the Node class:


class Node:
    def __init__(self, node_type, left=None, right=None, value=None):
        
        self.type = node_type  # 'operator' or 'operand'
        
        self.left = left       # Left child node reference
        
        self.right = right     # Right child node reference
        
        self.value = value     # Value for operand nodes (optional)
        
This class enables the creation of nodes representing rules in the form of an AST, facilitating dynamic rule manipulation.

3. Data Storage
   
SQLite is used as the database for storing rules and application metadata. Here’s the table schema:

sql

CREATE TABLE rules (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    
    rule_string TEXT NOT NULL,
    
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
    
);

Sample rules can be inserted like this:

sql

INSERT INTO rules (rule_string) VALUES

    ("((age > 30 AND department = 'Sales') OR (age < 25 AND department = 'Marketing')) AND (salary > 50000 OR experience > 5)"),
    
    ("((age > 30 AND department = 'Marketing')) AND (salary > 20000 OR experience > 5)");
    

4. API Design
The following key API functions are available:

1. Create Rule
Function: create_rule(rule_string)
Description: Accepts a rule string and returns a Node object representing the AST.
2. Combine Rules
Function: combine_rules(rules)
Description: Merges multiple rule strings into a single AST for evaluation.
3. Evaluate Rule
Function: evaluate_rule(json_data)
Description: Evaluates the AST using user-provided attribute data, returning True or False based on eligibility.

### 5. Test Cases
Creating Rules:

Test the creation of individual rules with create_rule and verify the AST structure.
Combining Rules:

Test combining multiple rules using combine_rules and ensure the AST reflects the merged logic.
Evaluating Rules:

Provide sample user data in JSON format and test rule evaluation using evaluate_rule.
Exploring Additional Scenarios:

Experiment with various rule combinations and test evaluation accuracy.
### 6. Bonus Features
Error Handling:

Incorporate mechanisms to handle invalid rule strings or data formats.
Validations:

Ensure attribute data is validated against a predefined schema or catalog.
Rule Editing:

Enable users to modify existing rules dynamically.
User-Defined Functions:

Plan to support more complex rule conditions with user-defined functions.
7. Non-Functional Requirements
Security:

Implement SQL injection prevention measures and input validation.
Performance:

Enhance rule evaluation efficiency through caching or optimization strategies.
Scalability:

Design the system to scale with increasing rule evaluations and data loads.


