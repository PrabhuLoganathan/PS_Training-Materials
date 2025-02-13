# Selenium WebDriver - Hands-on Assignments

## 1️⃣ Creating Test Scripts in WebDriver

### Steps to Create a Basic Test Script in Selenium WebDriver
1. **Set up Selenium WebDriver** in your project.
2. **Initialize the WebDriver** instance.
3. **Open a web page** and interact with elements.
4. **Validate test results** by verifying expected behavior.
5. **Close the browser** properly after execution.

### Example: Basic Selenium WebDriver Script (Java)
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class BasicTest {
    public static void main(String[] args) {
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
        WebDriver driver = new ChromeDriver();
        driver.get("https://seleniumbase.io/demo_page");
        System.out.println("Page Title: " + driver.getTitle());
        driver.quit();
    }
}
```

---

## 2️⃣ Selenium WebDriver Commands and Operations

### Commonly Used WebDriver Commands:
- **Navigating to URLs:** `driver.get("https://seleniumbase.io/demo_page");`
- **Fetching Page Title:** `driver.getTitle();`
- **Finding Elements:** `driver.findElement(By.id("elementId"));`
- **Typing in a Textbox:** `element.sendKeys("Hello");`
- **Clicking a Button:** `element.click();`
- **Getting Text from an Element:** `element.getText();`
- **Clearing Input Field:** `element.clear();`
- **Handling Alerts:** `driver.switchTo().alert().accept();`

---

## 3️⃣ Automation Scenarios for SeleniumBase Demo Page

### 🔹 Scenario 1: Automating Text Input Fields
**Steps:**
1. Locate the text input field using `By.id("myTextInput")`.
2. Enter a value into the text box.
3. Validate the entered text.

**Example Code:**
```java
WebElement textBox = driver.findElement(By.id("myTextInput"));
textBox.sendKeys("Test Input");
Assert.assertEquals(textBox.getAttribute("value"), "Test Input");
```

### 🔹 Scenario 2: Handling Dropdown Menus
**Steps:**
1. Hover over the dropdown to reveal options.
2. Click on a dropdown option.
3. Validate the selected option text.

**Example Code:**
```java
WebElement dropdown = driver.findElement(By.id("myDropdown"));
Actions action = new Actions(driver);
action.moveToElement(dropdown).perform();
driver.findElement(By.id("dropOption2")).click();
```

### 🔹 Scenario 3: Button Click Functionality
**Steps:**
1. Locate the button using `By.id("myButton")`.
2. Click the button.
3. Validate that the text color changes.

**Example Code:**
```java
WebElement button = driver.findElement(By.id("myButton"));
button.click();
WebElement updatedText = driver.findElement(By.id("pText"));
Assert.assertEquals(updatedText.getText(), "This Text is Purple");
```

### 🔹 Scenario 4: Handling Checkboxes
**Steps:**
1. Locate checkboxes and select them.
2. Validate if the checkbox is selected.

**Example Code:**
```java
WebElement checkbox = driver.findElement(By.id("checkBox1"));
checkbox.click();
Assert.assertTrue(checkbox.isSelected());
```

### 🔹 Scenario 5: Interacting with Sliders
**Steps:**
1. Locate the slider using `By.id("mySlider")`.
2. Adjust the slider value.
3. Validate the progress bar updates.

**Example Code:**
```java
WebElement slider = driver.findElement(By.id("mySlider"));
slider.sendKeys("80");
WebElement progressBar = driver.findElement(By.id("progressBar"));
Assert.assertEquals(progressBar.getAttribute("value"), "80");
```

### 🔹 Scenario 6: Handling Frames
**Steps:**
1. Switch to iframe using `driver.switchTo().frame("myFrame1")`.
2. Interact with elements inside the iframe.
3. Switch back to the default content.

**Example Code:**
```java
driver.switchTo().frame("myFrame1");
WebElement frameText = driver.findElement(By.tagName("h4"));
Assert.assertEquals(frameText.getText(), "iFrame Text");
driver.switchTo().defaultContent();
```

### 🔹 Scenario 7: Drag and Drop Functionality
**Steps:**
1. Locate draggable element and drop zone.
2. Perform drag and drop action.
3. Validate if the element is successfully dropped.

**Example Code:**
```java
WebElement source = driver.findElement(By.id("logo"));
WebElement target = driver.findElement(By.id("drop1"));
Actions action = new Actions(driver);
action.dragAndDrop(source, target).perform();
```

### 🔹 Scenario 8: Clicking on Links
**Steps:**
1. Locate and click the link.
2. Validate the redirected page title.

**Example Code:**
```java
WebElement link = driver.findElement(By.id("myLink1"));
link.click();
Assert.assertEquals(driver.getTitle(), "SeleniumBase");
```

---

## 4️⃣ Conclusion
Selenium WebDriver allows for automated testing of different UI components efficiently. By implementing these hands-on scenarios, testers can ensure better test coverage and robust automation for web applications. 🚀

