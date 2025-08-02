# Task-03: Automated Login Test for a Web Application

## 📌 Objective:
Automate login functionality testing for the [Swag Labs Demo Website](https://www.saucedemo.com/) using Selenium in Python.

## ✅ Tools & Libraries:
- Python
- Selenium
- Chrome WebDriver

## 🔐 Credentials Used:
- **Valid User**: `standard_user`
- **Password**: `secret_sauce`
- Includes various test cases for locked out user, invalid credentials, UI issues, etc.

## 🔁 Test Scenarios:
| Test Case ID | Username                  | Password       | Expected Result                           | Type       |
|--------------|---------------------------|----------------|--------------------------------------------|------------|
| TC_01        | standard_user             | secret_sauce   | Successfully logs in                       | Positive   |
| TC_02        | locked_out_user           | secret_sauce   | Error: User is locked out                  | Negative   |
| TC_03        | invalid_user              | wrong_pass     | Error: Username/password mismatch          | Negative   |
| TC_04        | *(empty)*                 | secret_sauce   | Error: Username is required                | Negative   |
| TC_05        | standard_user             | *(empty)*      | Error: Password is required                | Negative   |
| TC_06        | performance_glitch_user   | secret_sauce   | Delayed login                              | Edge Case  |
| TC_07        | visual_user               | secret_sauce   | Visual layout issues                       | Visual Bug |

## ▶️ How to Run:
```bash
pip install selenium
python login_test.py
