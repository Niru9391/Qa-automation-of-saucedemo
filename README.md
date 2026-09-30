# E-Commerce Test Automation Framework

## About the Project

This project is a **test automation framework for an e-commerce web application**, developed using **Python, Selenium WebDriver, and PyTest**. The framework is designed to automate functional testing of web application workflows and validate REST APIs. It follows the **Page Object Model (POM)** to keep the automation code organized, reusable, maintainable, and scalable.

## Technologies Used

The framework uses **Python 3.11** as the programming language, **Selenium WebDriver 4.x** for browser automation, and **PyTest** as the test execution framework. REST API testing is performed using the Python **Requests** library. The project uses **pytest-html and Allure** for generating test execution reports. Configuration settings are managed using `configparser` and a `config.ini` file. **GitHub Actions** is used to automate test execution as part of the CI/CD pipeline.

## Project Structure

The project is organized into separate directories based on their responsibilities. The `config` directory contains configuration files such as application URLs, credentials, and test settings. The `pages` directory contains Page Object Model classes, including reusable Selenium methods and page-specific actions and locators. The `api` directory contains helper methods used for REST API testing.

The `tests` directory contains separate UI and API test cases. UI tests include login scenarios and data-driven login tests, while API tests validate REST API functionality. The `test_data` directory contains CSV files used as input for data-driven testing. The `utils` directory contains reusable utilities such as CSV data readers. The `reports` directory stores generated HTML, Allure, and screenshot reports. The `conftest.py` file contains PyTest fixtures and hooks, while `pytest.ini` contains test markers and PyTest configuration.

## Test Coverage

The framework currently contains **27 automated test cases**. These include **10 UI tests** for login and related user flows, **7 data-driven UI tests** using CSV test data, and **10 REST API tests** for product and customer-related API validation.

The tests can be executed individually or as complete test suites depending on the testing requirement.

## UI Automation

The UI automation is implemented using **Selenium WebDriver and the Page Object Model**. The framework automates login, session validation, navigation, and other user interactions on the e-commerce application.

The Page Object Model separates page locators and page actions from the actual test cases. This makes the test code easier to understand and reduces duplication when the application UI changes.

## Data-Driven Testing

The framework supports **data-driven testing using CSV files**. Login test data is maintained separately from the automation code, allowing multiple combinations of test data to be executed without creating separate test methods for each scenario.

This approach makes it easier to add new test cases and maintain existing test data.

## API Testing

REST API testing is implemented using the **Python Requests library**. The API tests validate endpoints by checking HTTP status codes, response data, and expected API behavior.

This provides an additional layer of testing beyond UI automation and helps validate the application's backend services independently.

## Test Reporting

The framework generates detailed test execution reports using **pytest-html and Allure**. These reports provide information about test results, passed and failed test cases, and execution details.

The framework also captures **screenshots automatically when a UI test fails**, making it easier to identify and debug failures.

## CI/CD Integration

The automation framework is integrated with **GitHub Actions**. Tests are automatically executed when code is pushed to the repository or when a pull request is created.

The framework supports **headless Chrome execution**, which allows the Selenium tests to run in CI/CD environments without opening a visible browser window.

This integration helps ensure that application changes are continuously validated through automated testing.

## Test Execution

To run the project locally, first install the required dependencies using the following command:

```bash
pip install -r requirements.txt
```

To execute all automated tests, run:

```bash
pytest -v
```

Specific test suites can be executed using PyTest markers. For example:

```bash
pytest -m smoke -v
pytest -m ui -v
pytest -m api -v
pytest -m regression -v
```

An HTML test report can be generated using:

```bash
pytest -v --html=reports/html/report.html --self-contained-html
```

An Allure report can be generated using:

```bash
pytest -v --alluredir=reports/allure
allure serve reports/allure
```

## Test Applications

For UI automation, the framework uses **SauceDemo**, which provides an e-commerce-style web application for testing login, sessions, navigation, and shopping workflows.

For API testing, the framework uses **JSONPlaceholder** to simulate REST API interactions and validate API responses.

## Key Features

The framework provides a reusable **Page Object Model architecture**, data-driven testing, REST API validation, automatic screenshots on failures, HTML and Allure reporting, PyTest markers for selective execution, headless browser execution, and GitHub Actions-based CI/CD automation.

Overall, the project demonstrates an end-to-end approach to **QA automation**, combining UI testing, API testing, test data management, reporting, and continuous integration into a single automation framework.

## Test Execution Summary

The current automation suite contains **27 automated test cases covering both UI and REST API testing**. The test suite is designed to provide repeatable and maintainable automated validation of the application and can be extended with additional functional, regression, API, and end-to-end scenarios as the project grows.
