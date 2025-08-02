Task-04: Cross-Browser Testing with BrowserStack customized for Flipkart.

✅ Task-04: Cross-Browser Testing with BrowserStack (for Flipkart)

---

 🧾 Objective:

Run automated login test** for **[https://www.flipkart.com](https://www.flipkart.com) on multiple browsers and devices using BrowserStack's Selenium Grid.

🔧 Step-by-Step Implementation for Flipkart

✅ 1. BrowserStack Setup

* Sign up on: [https://www.browserstack.com/users/sign\_up](https://www.browserstack.com/users/sign_up)
* Copy your Username and Access Key from [BrowserStack Automate](https://automate.browserstack.com/)

---

✅ 2. Selenium Script to Test Login (Python)

🔽 flipkart_login_test.py

  python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time

 Replace with your BrowserStack credentials
USERNAME = 'your_browserstack_username'
ACCESS_KEY = 'your_browserstack_access_key'

desired_cap = {
    'browser': 'Chrome',
    'browser_version': 'latest',
    'os': 'Windows',
    'os_version': '10',
    'name': 'Flipkart Login Test',
    'build': 'Task-04 BrowserStack'
}

driver = webdriver.Remote(
    command_executor=f'https://{USERNAME}:{ACCESS_KEY}@hub-cloud.browserstack.com/wd/hub',
    desired_capabilities=desired_cap
)

# Test Steps
driver.get("https://www.flipkart.com")
time.sleep(3)

 Close initial login popup
try:
    close_btn = driver.find_element(By.XPATH, "//button[contains(text(),'✕')]")
    close_btn.click()
    time.sleep(1)
except:
    pass

 Click login button (top right)
driver.find_element(By.XPATH, "//a[text()='Login']").click()
time.sleep(2)

 Enter mobile number (test number for demo)
driver.find_element(By.XPATH, "//input[@class='_2IX_2- VJZDxU']").send_keys("9999999999")
driver.find_element(By.XPATH, "//button[@type='submit']").click()
time.sleep(3)

NOTE: You can't fully automate OTP in production. Use dummy mobile if Flipkart test env exists.

print("✅ Flipkart login page loaded successfully.")
driver.quit()
```

---

 ✅ 3. **Run the Same Test in Different Browsers**

Modify only `desired_cap` part:

 🔁 Firefox

```python
desired_cap = {
    'browser': 'Firefox',
    'browser_version': 'latest',
    'os': 'Windows',
    'os_version': '11',
    ...
}


 🔁 Safari

   python
desired_cap = {
    'browser': 'Safari',
    'os': 'OS X',
    'os_version': 'Monterey',
    ...
}


#### 🔁 Edge

   python
desired_cap = {
    'browser': 'Edge',
    'os': 'Windows',
    'os_version': '10',
    ...
}


 📋 Final Test Result Table (Example):

| Browser | OS         | Result    | Observations                          |
| ------- | ---------- | --------- | ------------------------------------- |
| Chrome  | Windows 10 | ✅ Success | UI loads fine, login popup works well |
| Firefox | Windows 11 | ✅ Success | Slight delay in rendering popups      |
| Safari  | macOS      | ❗ Partial | Close button doesn’t align properly   |
| Edge    | Windows 10 | ✅ Success | All buttons & popups function well    |


 🧾 What You Submit for Internship:

1. ✅ `flipkart_login_test.py` – test script file
2. ✅ Screenshots or logs from BrowserStack
3. ✅ A `.docx` or `.md` file including:

   * Objective
   * Steps performed
   * Observations from each browser
   * Issues and recommendations (if any)

 📂 Bonus Template: Test Report Format

 📄 Flipkart Cross-Browser Testing Report (Markdown)

```markdown
 Task-04: Cross-Browser Testing for Flipkart

 ✅ Objective:
Test Flipkart login popup across different browsers using BrowserStack.

 🌐 Browsers Tested:
- Chrome (Windows 10)
- Firefox (Windows 11)
- Safari (macOS)
- Edge (Windows 10)

 🧪 Test Steps:
1. Visit https://www.flipkart.com
2. Close initial popup
3. Click on "Login"
4. Enter mobile number
5. Observe UI behavior

 📊 Results:

| Browser  | OS         | Result   | Notes                                |
|----------|------------|----------|--------------------------------------|
| Chrome   | Windows 10 | Pass     | Everything works as expected         |
| Firefox  | Windows 11 | Pass     | Slight delay in popup response       |
| Safari   | macOS      | Partial  | Layout shift on mobile field         |
| Edge     | Windows 10 | Pass     | Smooth UI, login popup stable        |

