Notes:

- Can't test static methods at all
- Methods need to be very modularized as it's borderline impossible to do good mocking with mega methods.
- Service layer code should ideally still use integration testing without mocks (potentially using mocks for dependencies though) to make sure the user 
  gets the expected results.
- Really only meant for Domain and Application layer tests
- Speeds up testing significantly
- To use effectively (i.e. good DML mocking to speed up testing) you need to implement the DAO (Data Access Object) design pattern in your org

Easiest library to use IMO: https://github.com/surajp/universalmock

Also have good object data mocking classes here (originally built by Caleb Weaver): https://github.com/Coding-With-The-Force/SalesforceBestPractices/tree/master/MockDataBuilder
