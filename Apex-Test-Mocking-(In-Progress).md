Notes:

- Can't test static methods at all
- Methods need to be very modularized as it's borderline impossible to do good mocking with mega methods.
- Service layer code should be tested for real (potentially using mocks for dependencies though) to make sure the user gets the expected results.
- Really only meant for Domain and application layer tests
- Speeds up testing significantly

Easiest code to use IMO:https://github.com/surajp/universalmock
Also have good object data mocking classes here (originally built by Caleb Weaver): https://github.com/Coding-With-The-Force/SalesforceBestPractices/tree/master/MockDataBuilder
