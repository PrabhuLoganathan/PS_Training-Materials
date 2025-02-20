# Selenium Cucumber BDD Assessment


---
## **Instructions:**
1. Clone the existing Selenium-Cucumber-BDD-Maven framework.
2. Implement the required step definitions for each feature file.
3. Run the tests using TestNG Runner.
4. Generate reports using Extent/Allure.
5. Push the completed code to a Git repository.

---

## **Assessment Tasks**

### **1. Handling Multiple Tabs/Windows**

#### **Feature File: `multiple_tabs.feature`**
```gherkin
Feature: Handling multiple browser tabs
  Scenario: Verify switching between multiple tabs
    Given User navigates to "https://example.com"
    When User clicks on a link that opens a new tab
    Then User switches to the new tab
    And User verifies the new tab has title "New Tab Title"
    And User switches back to the main tab
```

---

### **2. Handling Alerts**

#### **Feature File: `alerts.feature`**
```gherkin
Feature: Handling browser alerts
  Scenario: Verify alert handling
    Given User navigates to "https://example.com/alerts"
    When User clicks on an alert button
    Then User accepts the alert
    When User clicks on a confirmation alert button
    Then User dismisses the alert
```

---

### **3. Using Scenario Outline**

#### **Feature File: `login.feature`**
```gherkin
Feature: Login functionality
  Scenario Outline: Login with multiple credentials
    Given User navigates to "https://example.com/login"
    When User enters username "<username>" and password "<password>"
    And User clicks on login button
    Then User should see the dashboard

  Examples:
    | username   | password  |
    | user1      | pass123   |
    | user2      | pass456   |
```

---

### **4. Using Data Table**

#### **Feature File: `registration.feature`**
```gherkin
Feature: User Registration
  Scenario: Register a new user
    Given User is on the registration page
    When User enters the following details:
      | First Name | Last Name | Email           | Password  |
      | John       | Doe       | john@test.com   | pass123   |
    Then User clicks the submit button
    And User should see a success message
```

---

### **5. Validating Element Presence with Custom XPath**

#### **Feature File: `element_validation.feature`**
```gherkin
Feature: Validating element presence with custom XPath
  Scenario: Verify the presence of a specific element
    Given User navigates to "https://example.com"
    Then User verifies the element with XPath "//div[@class='custom-element']" is present
```

---

## **Assessment Submission**
1. Implement the step definitions and automation logic in your Selenium framework.
2. Run the tests and attach the Extent/Allure report.
3. Push the code to your Git repository.
4. Submit the repository link along with the generated test report.

---

## **Evaluation Criteria:**
- **Correct Implementation:** Step definitions correctly automate the scenarios.
- **XPath Usage:** Custom XPath selectors effectively locate elements.
- **Proper Handling:** Alerts and multiple windows are handled appropriately.
- **Data-Driven Testing:** Scenario Outline and Data Tables are correctly used.
- **Reporting:** Extent/Allure reports should show test execution results.

---
### **Bonus (Optional)**
- Implement parallel execution for scenarios using TestNG.
- Integrate the framework with Jenkins for CI/CD automation.

