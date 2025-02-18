
# **Assignment: Selenium Test Automation Framework Development**
## **Objective:**
Develop a modular and scalable test automation framework using **Selenium with Java, Maven, BDD (Cucumber), and TestNG**, integrating **Extent Reports** for reporting.

---

## **Assignment Deliverables:**
### **Part 1: Core Framework Development**
1. **Framework Setup**
   - Create a **Maven** project.
   - Add dependencies for **Selenium WebDriver, Cucumber, TestNG, Extent Reports, and WebDriverManager**.

2. **Project Structure**
   - Organize the framework with a structured directory layout, including:
     - `utilities` for helper methods
     - `base` for setup and teardown logic
     - `stepDefinitions` for Cucumber steps
     - `runners` for executing tests
     - `testCases` for organizing test scripts
     - `features` for Gherkin feature files
     - `config.properties` for configurations

3. **Web Application Under Test**
   - Perform automated testing on the **My Contact Form** application.

4. **Test Scenarios (Feature Files)**
   - Write feature files following the **Gherkin syntax**.
   - Define clear **Given-When-Then** steps for:
     - Login functionality
     - e2e Form Submission
     

5. **Step Definitions**
   - Implement step definitions for each feature file.
   - Ensure correct mapping between **Gherkin steps** and **Selenium actions**.

6. **Page Object Model (POM)**
   - Create **Page Classes** for different web pages.
   - Implement **locators and methods** for interacting with elements.

7. **Test Execution with TestNG**
   - Configure **TestNG** for executing Cucumber feature files.
   - Ensure test execution runs smoothly without failures.

8. **Extent Reports Integration**
   - Implement **Extent Reports** for generating test reports.
   - Capture test execution logs and screenshots for failed cases.

9. **Parallel Execution**
   - Configure **TestNG.xml** to execute tests in **parallel** using multiple threads.

10. **GitHub Integration**
    - Push the framework to **GitHub**.
    - Maintain a well-documented **README.md**.


### **Part 2: Additional Functionalities**
12. **Broken Links Verification**
    - Implement a **utility method** to check for broken links in the web application.
    - Validate HTTP response codes (200 OK, 404 Not Found, etc.).
    - Log broken links in the test report.

13. **Taking Screenshots**
    - Capture screenshots for:
      - **Failed test cases** automatically.
      - **Specific test steps** (optional).
    - Save screenshots in a structured folder inside the project.

14. **Reading Data from Config and Property Files**
    - Implement methods to read **URLs, credentials, browser settings, and other configurations** from:
      - **config.properties** file
      - **Property file** (if separate data storage is used)

15. **Image URL Validation**
    - Extract **image URLs** from the application.
    - Check if the **image loads correctly** by verifying the HTTP status code.
    - Log image validation results in the test report.

---

## **Submission Requirements**
- **GitHub Repository** with project files.
- **Test Execution Report** (Extent Report or Cucumber HTML report).
- **Short README.md** explaining setup and usage.
- **Bonus:** Provide Jenkins job configuration details.

---

### **Evaluation Criteria**
| Criteria | Description | Marks |
|----------|------------|-------|
| Framework Setup | Correctly structured Maven project | 10 |
| Feature Files | Clear and well-defined Gherkin scenarios | 10 |
| Step Definitions | Properly implemented step definitions | 15 |
| Page Object Model | Well-structured page classes | 15 |
| TestNG & Cucumber | Successful integration and execution | 10 |
| Extent Reports | Proper test reporting setup | 10 |
| Parallel Execution | Running tests in multiple threads | 10 |
| GitHub Submission | Clean and well-documented repo | 10 |
| Broken Link Verification | Proper validation and logging | 5 |
| Screenshots | Capturing and saving screenshots correctly | 5 |
| Config & Property Files | Data retrieval implemented correctly | 5 |
| Image URL Validation | Image loading check implemented | 5 |

| **Total** | **100 Marks** |

---

### **Instructions for Students**
1. **Set up the framework** with the specified components.
2. **Run tests** and ensure they execute correctly.
3. **Generate Extent Reports** and validate test results.
4. **Push your project** to GitHub and share the repository link.





<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>SeleniumBase</groupId>
  <artifactId>SeleniumBase</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  
  <dependencies>
        <!-- Selenium WebDriver -->
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>4.18.1</version>
        </dependency>

        <!-- Cucumber Dependencies -->
        <dependency>
            <groupId>io.cucumber</groupId>
            <artifactId>cucumber-java</artifactId>
            <version>7.8.1</version>
        </dependency>
     


<!-- TestNG Dependency -->
<dependency>
    <groupId>org.testng</groupId>
    <artifactId>testng</artifactId>
    <version>7.7.0</version>
    <scope>test</scope>
</dependency>

    
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-testng</artifactId>
        <version>7.8.1</version>
    </dependency>
    
    <!-- Extent Reports -->
<dependency>
    <groupId>com.aventstack</groupId>
    <artifactId>extentreports</artifactId>
    <version>5.0.9</version>
</dependency>
<!-- Extent Reports Adapter for Cucumber -->
<dependency>
	<groupId>com.vimalselvam</groupId>
	<artifactId>cucumber-extentsreport</artifactId>
	<version>3.1.1</version>
</dependency>
<!-- https://mvnrepository.com/artifact/tech.grasshopper/extentreports-cucumber7-adapter--> 
<dependency>
    <groupId>tech.grasshopper</groupId>
    <artifactId>extentreports-cucumber7-adapter</artifactId>
    <version>1.10.1</version>
</dependency>

<!-- Allure Reports -->
<dependency>
    <groupId>io.qameta.allure</groupId>
    <artifactId>allure-cucumber7-jvm</artifactId>
    <version>2.22.0</version>
</dependency>

    </dependencies>

    <build>
        <plugins>
			
			      <plugin>
            <groupId>io.qameta.allure</groupId>
            <artifactId>allure-maven</artifactId>
            <version>2.10.0</version>
        </plugin>
			
         <!--   <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.0.0-M7</version>
                <configuration>
                    <includes>
                        <include>**/TestRunner.java</include>
                    </includes>
                </configuration>
            </plugin>-->
            

        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M7</version>
            <configuration>
                <suiteXmlFiles>
                    <suiteXmlFile>src/test/resources/testng.xml</suiteXmlFile>
                </suiteXmlFiles>
            </configuration>
        </plugin>


        </plugins>
    </build>
  
</project>




    plugin = {
                "pretty",
                "html:target/cucumber-reports.html",
                "json:target/cucumber.json",
                "com.aventstack.extentreports.cucumber.adapter.ExtentCucumberAdapter:",
                "io.qameta.allure.cucumber7jvm.AllureCucumber7Jvm"
        },