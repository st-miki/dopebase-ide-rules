# Python - Best Practices & Coding Rules

## Code Style & Formatting
- Follow PEP 8 style guide for consistent code formatting
- Use meaningful variable and function names that clearly express intent
- Keep functions small and focused on a single responsibility
- Use proper indentation (4 spaces) and line length (79 characters)
- Use type hints for better code documentation and IDE support
- Follow consistent naming conventions: snake_case for variables/functions, PascalCase for classes

## Python Best Practices
- Use list comprehensions and generator expressions for clean, efficient code
- Prefer explicit over implicit code; avoid magic methods when possible
- Use context managers (`with` statements) for resource management
- Implement proper error handling with try-except blocks
- Use virtual environments for dependency management
- Follow the Zen of Python principles

## Data Structures & Algorithms
- Use appropriate data structures for the task (list, dict, set, tuple)
- Leverage Python's built-in functions and libraries
- Use collections module for specialized data structures
- Implement proper data validation and type checking
- Use pandas for data manipulation and analysis
- Optimize performance with proper algorithm selection

## Object-Oriented Programming
- Use classes for complex data structures and behavior
- Implement proper inheritance and composition patterns
- Use properties and descriptors for attribute access control
- Implement proper `__str__` and `__repr__` methods
- Use abstract base classes for interface definition
- Follow SOLID principles for maintainable code

## Error Handling & Logging
- Use specific exception types instead of bare except clauses
- Implement proper logging with the logging module
- Use custom exceptions for domain-specific errors
- Handle errors gracefully with proper user feedback
- Use context managers for proper resource cleanup
- Implement proper error recovery and retry mechanisms

## Testing
- Write unit tests for all functions and methods
- Use pytest for comprehensive testing framework
- Implement proper test fixtures and parametrization
- Mock external dependencies in tests
- Aim for high test coverage on critical paths
- Use property-based testing for edge cases

## Performance Optimization
- Use appropriate data structures for performance
- Leverage NumPy for numerical computations
- Use multiprocessing for CPU-intensive tasks
- Implement proper caching strategies
- Profile code to identify bottlenecks
- Use generators for memory-efficient iteration

## Package Management
- Use pip and requirements.txt for dependency management
- Use virtual environments for project isolation
- Use Poetry or pipenv for advanced dependency management
- Implement proper package structure and setup.py
- Use proper versioning and semantic versioning
- Document dependencies and installation instructions

## Web Development
- Use Flask or Django for web application development
- Implement proper REST API design with FastAPI
- Use proper request validation and error handling
- Implement proper authentication and authorization
- Use proper database ORM and migrations
- Follow web security best practices

## Data Science & Analysis
- Use Jupyter notebooks for exploratory data analysis
- Use pandas for data manipulation and analysis
- Use matplotlib and seaborn for data visualization
- Use scikit-learn for machine learning
- Implement proper data preprocessing and validation
- Use proper statistical methods and validation

## Code Organization
- Organize code into logical modules and packages
- Use proper import statements and avoid circular imports
- Implement proper separation of concerns
- Use configuration files for environment-specific settings
- Create proper documentation with docstrings
- Use proper version control and commit messages

## Security
- Validate all user inputs and external data
- Use proper authentication and authorization
- Implement proper password hashing and storage
- Use secure communication protocols (HTTPS)
- Follow OWASP security guidelines
- Implement proper error handling without information leakage

