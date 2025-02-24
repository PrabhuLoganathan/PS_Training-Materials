Here are example programs for each advanced Selenium topic you listed:

---

### **1. Handling JavaScript Alerts**
JavaScript alerts, confirmations, and prompts can be handled using Selenium’s `Alert` interface.

```java
import org.openqa.selenium.Alert;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class HandleJSAlert {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        driver.get("https://the-internet.herokuapp.com/javascript_alerts");

        // Click the button to trigger the alert
        driver.findElement(By.xpath("//button[text()='Click for JS Alert']")).click();

        // Switch to alert
        Alert alert = driver.switchTo().alert();
        System.out.println("Alert Text: " + alert.getText());

        // Accept alert
        alert.accept();

        driver.quit();
    }
}
```

---

### **2. Handling Multiple Windows/Tabs**
You can switch between different windows using `getWindowHandles()`.

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.By;
import java.util.Set;

public class HandleMultipleWindows {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        driver.get("https://demo.automationtesting.in/Windows.html");

        // Click on a link that opens a new window
        driver.findElement(By.xpath("//a[contains(text(),'Open New Seperate Windows')]")).click();
        driver.findElement(By.xpath("//button[text()='click']")).click();

        // Store the main window handle
        String mainWindowHandle = driver.getWindowHandle();

        // Get all window handles
        Set<String> allWindows = driver.getWindowHandles();

        // Switch to the new window
        for (String window : allWindows) {
            if (!window.equals(mainWindowHandle)) {
                driver.switchTo().window(window);
                System.out.println("New Window Title: " + driver.getTitle());
                driver.close(); // Close the new window
            }
        }

        // Switch back to main window
        driver.switchTo().window(mainWindowHandle);
        driver.quit();
    }
}
```

---

### **3. Handling Webpage Iframes**
You can switch to an iframe using `switchTo().frame()`.

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.By;

public class HandleIFrame {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        driver.get("https://the-internet.herokuapp.com/iframe");

        // Switch to iframe by index or ID
        driver.switchTo().frame("mce_0_ifr");

        // Perform actions inside the iframe
        driver.findElement(By.id("tinymce")).clear();
        driver.findElement(By.id("tinymce")).sendKeys("Hello, Iframe!");

        // Switch back to the main content
        driver.switchTo().defaultContent();

        driver.quit();
    }
}
```

---

### **4. Handling Native Pop-Up Windows**
Native file upload/download pop-ups can be handled using Robot or AutoIT.

#### **Using Robot Class**
```java
import java.awt.*;
import java.awt.event.KeyEvent;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.By;

public class HandleFileUpload {
    public static void main(String[] args) throws AWTException {
        WebDriver driver = new ChromeDriver();
        driver.get("https://demo.guru99.com/test/upload/");

        // Click to upload file
        driver.findElement(By.id("file_wraper0")).click();

        // Using Robot class to simulate file selection
        Robot robot = new Robot();
        robot.delay(2000);

        // Paste file path
        Toolkit.getDefaultToolkit().getSystemClipboard().setContents(new StringSelection("C:\\path\\to\\file.txt"), null);
        robot.keyPress(KeyEvent.VK_CONTROL);
        robot.keyPress(KeyEvent.VK_V);
        robot.keyRelease(KeyEvent.VK_V);
        robot.keyRelease(KeyEvent.VK_CONTROL);
        
        // Press Enter
        robot.keyPress(KeyEvent.VK_ENTER);
        robot.keyRelease(KeyEvent.VK_ENTER);

        driver.quit();
    }
}
```

---

### **5. Working with AutoIT**
AutoIT is useful for handling Windows file upload popups.

#### **AutoIT Script (`fileupload.au3`):**
```autoit
ControlFocus("Open","","Edit1")
ControlSetText("Open","","Edit1","C:\path\to\file.txt")
ControlClick("Open","","Button1")
```

#### **Java Code to Trigger AutoIT Script**
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.By;
import java.io.IOException;

public class HandleAutoIT {
    public static void main(String[] args) throws IOException {
        WebDriver driver = new ChromeDriver();
        driver.get("https://demo.guru99.com/test/upload/");

        // Click upload button
        driver.findElement(By.id("file_wraper0")).click();

        // Run AutoIT script
        Runtime.getRuntime().exec("C:\\path\\to\\fileupload.exe");

        driver.quit();
    }
}
```

---

### **6. Hands-on Assignments**
Here are a few assignments for practice:

#### **Assignment 1: Handle Multiple Alerts**
- Navigate to `https://the-internet.herokuapp.com/javascript_alerts`
- Handle all three alert types: simple alert, confirmation alert, and prompt.

#### **Assignment 2: Handle Multiple Windows**
- Open `https://demo.automationtesting.in/Windows.html`
- Click to open multiple new windows
- Switch between them and print each title.

#### **Assignment 3: Handle iFrames**
- Open `https://the-internet.herokuapp.com/iframe`
- Switch to the iframe and input custom text.

#### **Assignment 4: Handle File Upload with AutoIT**
- Go to `https://demo.guru99.com/test/upload/`
- Upload a file using AutoIT.

### **Handling Native Windows Popups in Selenium**

Selenium alone cannot handle native Windows popups (such as file upload dialogs) because they are not part of the browser DOM. To handle such popups, we use **Robot Class** or **AutoIT**.

---

## **1. Handling Native Windows Popups using Robot Class**
Robot class in Java can simulate keyboard and mouse actions to interact with Windows-based popups.

### **Example: Handling File Upload Popup Using Robot Class**
```java
import java.awt.*;
import java.awt.datatransfer.StringSelection;
import java.awt.event.KeyEvent;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class HandleNativePopupRobot {
    public static void main(String[] args) throws AWTException, InterruptedException {
        WebDriver driver = new ChromeDriver();
        driver.get("https://demo.guru99.com/test/upload/");

        // Click on the "Choose File" button
        driver.findElement(By.id("file_wraper0")).click();
        Thread.sleep(2000); // Wait for file upload window to open

        // Set the file path to clipboard
        String filePath = "C:\\Users\\YourUsername\\Documents\\testfile.txt";
        StringSelection selection = new StringSelection(filePath);
        Toolkit.getDefaultToolkit().getSystemClipboard().setContents(selection, null);

        // Use Robot class to paste and press Enter
        Robot robot = new Robot();
        robot.delay(1000);

        // Press CTRL + V to paste the file path
        robot.keyPress(KeyEvent.VK_CONTROL);
        robot.keyPress(KeyEvent.VK_V);
        robot.keyRelease(KeyEvent.VK_V);
        robot.keyRelease(KeyEvent.VK_CONTROL);

        // Press ENTER
        robot.keyPress(KeyEvent.VK_ENTER);
        robot.keyRelease(KeyEvent.VK_ENTER);

        // The file should now be uploaded
        System.out.println("File Uploaded Successfully!");

        driver.quit();
    }
}
```
**Explanation:**
1. Clicks on the file upload button.
2. Uses **Robot class** to handle the popup.
3. Copies file path to the clipboard.
4. Simulates **CTRL + V** to paste the file path.
5. Presses **Enter** to upload the file.

---

## **2. Handling Native Windows Popups Using AutoIT**
AutoIT is a scripting language specifically designed for automating Windows GUI tasks.

### **Step 1: Create an AutoIT Script (`fileUpload.au3`)**
```autoit
ControlFocus("Open","","Edit1")
ControlSetText("Open","","Edit1","C:\Users\YourUsername\Documents\testfile.txt")
ControlClick("Open","","Button1")
```
**Explanation:**
- `ControlFocus("Open","","Edit1")` → Focus on the file dialog box.
- `ControlSetText("Open","","Edit1","C:\Users\YourUsername\Documents\testfile.txt")` → Set the file path.
- `ControlClick("Open","","Button1")` → Click the Open button.

### **Step 2: Compile the Script to `.exe`**
1. Download and install **AutoIT**.
2. Open the AutoIT Editor.
3. Save the script as `fileUpload.au3`.
4. Right-click the `.au3` file and select **Compile Script** (Generates `fileUpload.exe`).

### **Step 3: Call AutoIT Script from Selenium Java**
```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import java.io.IOException;

public class HandleNativePopupAutoIT {
    public static void main(String[] args) throws IOException {
        WebDriver driver = new ChromeDriver();
        driver.get("https://demo.guru99.com/test/upload/");

        // Click the "Choose File" button
        driver.findElement(By.id("file_wraper0")).click();

        // Execute the AutoIT script
        Runtime.getRuntime().exec("C:\\path\\to\\fileUpload.exe");

        System.out.println("File Uploaded Successfully!");

        driver.quit();
    }
}
```

**Key Differences:**
| **Method** | **Best for** | **Requires External Tool?** |
|------------|-------------|--------------------------|
| **Robot Class** | Simple file uploads | No |
| **AutoIT** | Complex popups with multiple actions | Yes |

---

### **3. Handling Native Windows Authentication Popups (Basic Auth)**
Some websites require authentication popups (username/password) when you try to access them.

#### **Solution 1: Pass Credentials in URL**
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class HandleAuthPopup {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        
        // Format: https://username:password@website.com
        driver.get("https://admin:admin@the-internet.herokuapp.com/basic_auth");

        System.out.println("Authentication Successful!");
        driver.quit();
    }
}
