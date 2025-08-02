
 🔐 Swag Labs Login Page – Key Information

🖼️ UI Elements:
Username Field

   Input field where the user enters their username.
         Password Field

   Input field where the user enters their password.
     Login Button

   Green-colored button labeled "Login" used to submit the form.


 ✅ Accepted Usernames:

These are predefined test usernames you can use for testing different scenarios in the Swag Labs application:

1. standard_user

   > Used for general positive login test (default user).
2. locked_out_user

   > Simulates a user who is not allowed to log in (negative test case).
3.  problem_user

   > Used to test issues like broken images or UI bugs.
4.  performance_glitch_user

   > Simulates performance lags or delays after login.
5.  error_user

   > Might trigger error-handling scenarios.
6.  visual_user

   > Used to test visual bugs or layout issues.

---

### 🔑 Password for All Users:

>  secret_sauce

Regardless of the username you use, the **password remains the same** for all users.

---

### 🔁 Test Scenarios You Can Perform:

| Type      | Username                  | Password      | Expected Outcome                                     |
| --------- | ------------------------- | ------------- | ---------------------------------------------------- |
| ✅ Valid   | `standard_user`           | secret\_sauce | Successfully logs in and redirects to inventory page |
| ❌ Locked  | `locked_out_user`         | secret\_sauce | Error: User is locked out                            |
| ❌ Visual  | `visual_user`             | secret\_sauce | Layout or styling issues may appear                  |
| ❌ Glitch  | `performance_glitch_user` | secret\_sauce | Takes time to load after login                       |
| ❌ Problem | `problem_user`            | secret\_sauce | UI may break, broken images                          |
| ❌ Error   | `error_user`              | secret\_sauce | May crash or throw unexpected errors                 |
| ❌ Invalid | `wrong_user`              | secret\_sauce | Login fails, "Username and password do not match"    |
| ❌ Empty   | *(empty)*                 | *(empty)*     | Validation errors shown                              |

---

Perfect! Here’s everything you need for **Task-03: Automated Login Test** using the **Swag Labs Login Page** (`https://www.saucedemo.com/`).

---

## ✅ Step 1: Sample Test Case Table

| Test Case ID | Description                        | Username                  | Password       | Expected Result                           | Type       |
| ------------ | ---------------------------------- | ------------------------- | -------------- | ----------------------------------------- | ---------- |
| TC\_01       | Login with valid user              | `standard_user`           | `secret_sauce` | Redirects to inventory page               | Positive   |
| TC\_02       | Login with locked out user         | `locked_out_user`         | `secret_sauce` | Error: User is locked out                 | Negative   |
| TC\_03       | Login with invalid credentials     | `invalid_user`            | `wrong_pass`   | Error: Username and password do not match | Negative   |
| TC\_04       | Login with empty username          | *(empty)*                 | `secret_sauce` | Error: Username is required               | Negative   |
| TC\_05       | Login with empty password          | `standard_user`           | *(empty)*      | Error: Password is required               | Negative   |
| TC\_06       | Login with glitch performance user | `performance_glitch_user` | `secret_sauce` | Logs in with delay                        | Edge Case  |
| TC\_07       | Login with visual bug user         | `visual_user`             | `secret_sauce` | Layout issues may be present              | Visual Bug |

---

## ✅ Step 2: Selenium Script (Python)

Make sure you have:

bash
pip install selenium

 🔍 Full Code:

python
from selenium import webdriver
from selenium.webdriver.common.by import By
import time

# Create a dictionary of test cases
test_cases = [
    {"username": "standard_user", "password": "secret_sauce", "expected": "success"},
    {"username": "locked_out_user", "password": "secret_sauce", "expected": "locked_out"},
    {"username": "invalid_user", "password": "wrong_pass", "expected": "error"},
    {"username": "", "password": "secret_sauce", "expected": "error"},
    {"username": "standard_user", "password": "", "expected": "error"},
    {"username": "performance_glitch_user", "password": "secret_sauce", "expected": "delay"},
]

def run_test_case(username, password, expected_result):
    driver = webdriver.Chrome()
    driver.get("https://www.saucedemo.com/")

    # Fill login form
    driver.find_element(By.ID, "user-name").send_keys(username)
    driver.find_element(By.ID, "password").send_keys(password)
    driver.find_element(By.ID, "login-button").click()
    
    time.sleep(2)

    if expected_result == "success":
        assert "inventory.html" in driver.current_url
        print(f"✅ PASS: {username} logged in successfully")
    elif expected_result == "locked_out":
        error = driver.find_element(By.CSS_SELECTOR, ".error-message-container").text
        assert "locked out" in error.lower()
        print(f"✅ PASS: {username} locked out as expected")
    elif expected_result == "delay":
        assert "inventory.html" in driver.current_url
        print(f"⚠️  PASS (with delay): {username} logged in after performance glitch")
    else:
        error = driver.find_element(By.CSS_SELECTOR, ".error-message-container").text
        assert "epic sadface" in error.lower()
        print(f"✅ PASS: Error shown for invalid input ({username})")

    driver.quit()

 Run all test cases
for case in test_cases:
    run_test_case(case["username"], case["password"], case["expected"])
