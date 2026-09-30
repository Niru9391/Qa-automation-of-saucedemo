# SauceDemo QA Automation

A Python-based Selenium automation project for testing the **SauceDemo web application**, with a focus on reliable login validation, negative scenarios, reusable page objects, and maintainable PyTest test cases.

**Application:** SauceDemo
**Automation:** Selenium WebDriver + Python
**Test Framework:** PyTest
**Design Pattern:** Page Object Model

---

## Why This Project?

Instead of writing Selenium commands directly inside every test, this project separates:

* **What we want to test** → test cases
* **How we interact with the page** → page objects
* **How the browser is prepared** → PyTest fixtures
* **Reusable Selenium operations** → base page

This separation makes the automation suite easier to read, debug, and extend.

---

## Automation Flow

```text
                 ┌─────────────────────┐
                 │      PyTest         │
                 │    Test Cases       │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │     LoginPage       │
                 │    Page Object      │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │     BasePage        │
                 │ Reusable Selenium   │
                 │     Methods         │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │  Selenium WebDriver │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │      SauceDemo      │
                 └─────────────────────┘
```

---

## What Is Currently Automated?

The current implementation concentrates on the **login functionality**.

### Login Page Checks

* Login page availability
* Username field visibility
* Password field visibility
* Login button interaction
* Successful login validation
* Empty credential validation
* Invalid password validation
* Error message validation
* Login-page state validation

The test suite is intentionally kept focused so that additional workflows can be introduced without making the framework difficult to maintain.

---

## Example Test Scenarios

| Scenario                        | Expected Result                       |
| ------------------------------- | ------------------------------------- |
| Valid username + valid password | User reaches inventory page           |
| Empty username                  | Username validation message displayed |
| Invalid password                | Authentication error displayed        |
| Login page loaded               | Required login elements are visible   |
| Failed authentication           | User remains on login page            |

---

## Framework Design

The project follows the **Page Object Model (POM)**.

For example, login-related locators are maintained inside `login_page.py` rather than being repeated throughout the test cases.

```python
USERNAME_INPUT = (By.ID, "user-name")
PASSWORD_INPUT = (By.ID, "password")
LOGIN_BUTTON = (By.ID, "login-button")
ERROR_MESSAGE = (By.CSS_SELECTOR, "[data-test='error']")
```

The page object then exposes reusable actions:

```python
login_page.login(username, password)
login_page.click_login()
login_page.get_error_message()
login_page.is_logged_in()
```

This keeps the test itself focused on **test intent instead of Selenium implementation details**.

---

## Repository Layout

```text
Qa-automation-of-saucedemo/
│
├── .github/
│   └── workflows/
│
├── config/
│
├── pages/
│   ├── base_page.py
│   └── login_page.py
│
├── test_data/
│
├── tests/
│   └── ui/
│       └── test_login.py
│
├── utils/
│
├── conftest.py
├── pytest.ini
├── requirements.txt
├── README.md
└── .gitignore
```

---

## Test Execution

### Install dependencies

```bash
python -m pip install -r requirements.txt
```

### Run all tests

```bash
python -m pytest -v
```

### Run login tests

```bash
python -m pytest tests/ui/test_login.py -v
```

### Run a specific test

```bash
python -m pytest tests/ui/test_login.py::test_login_with_invalid_password -v
```

---

## Test Environment

The automation is designed to run against:

```text
https://www.saucedemo.com/
```

The browser is controlled through Selenium WebDriver.

The project uses a PyTest fixture to manage browser setup and cleanup so individual tests do not need to duplicate WebDriver initialization code.

---

## Reliability Approach

The framework uses reusable Selenium methods and explicit waiting mechanisms rather than putting unnecessary delays throughout test cases.

The intention is to make tests:

**Readable → Stable → Reusable → Easy to Debug**

When a test fails, the failure can be traced from the test case to the corresponding page-object method and locator.

---

## Test Data

Login credentials and scenario-specific values can be maintained separately from the test implementation.

This allows additional combinations to be introduced without rewriting the test structure.

For example:

```text
Valid credentials
Invalid password
Invalid username
Empty username
Empty password
```

---

## CI Integration

The repository contains a GitHub A
