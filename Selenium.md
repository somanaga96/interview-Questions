### 1 **Select the option without Select Class**

Ans : 
```java
driver.get("https://letcode.in/dropdowns");
        WebElement state = driver.findElement(By.cssSelector("select#fruits"));
        state.click();
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(5));
        WebElement option = wait.until(ExpectedConditions.elementToBeClickable(
                By.xpath("//option[text()='Banana']")
        ));
        option.click();
```
2)  Exception
Selenium provides a wide range of exceptions to handle different scenarios that can occur during the execution of automated tests. Here’s a list of common exceptions in Selenium and their explanations:

### A. **NoSuchElementException**
   - **Description**: Thrown when an element could not be found in the DOM.
   - **Example**: Trying to find an element that doesn’t exist using `findElement(By.id("nonExistentId"))`.

 ### B. **ElementNotVisibleException**
   - **Description**: Thrown when an element is present in the DOM but is not visible (i.e., it has a `display: none` or `visibility: hidden` CSS property).
   - **Example**: Trying to click on an element that exists in the DOM but is hidden.

### C. **TimeoutException**
   - **Description**: Thrown when a command does not complete in the specified time.
   - **Example**: Waiting for an element to appear using `WebDriverWait` but it never does.



### D. **StaleElementReferenceException**
   - **Description**: Thrown when a reference to an element is now "stale" because the element is no longer present in the DOM.
   - **Example**: After a page refresh or a navigation, the element reference becomes stale.

### E. **NoSuchFrameException**
   - **Description**: Thrown when the frame being switched to is not found.
   - **Example**: Trying to switch to a frame that doesn’t exist using `driver.switchTo().frame("frameName")`.

### F. **NoSuchWindowException**
   - **Description**: Thrown when trying to switch to a window that is not found.
   - **Example**: Attempting to switch to a window that has been closed or never existed.

### G. **NoAlertPresentException**
   - **Description**: Thrown when switching to an alert, but the alert is not present.
   - **Example**: Using ```javadriver.switchTo().alert()``` when there is no alert displayed.

### H. **ElementNotSelectableException**
   - **Description**: Thrown when trying to select an element that cannot be selected.
   - **Example**: Attempting to select a disabled dropdown option.

### I. **WebDriverException**
   - **Description**: The base exception class in Selenium. It is thrown when something goes wrong with the WebDriver.
   - **Example**: Issues with the driver or communication between the browser and Selenium.

### J. **SessionNotFoundException**
   - **Description**: Thrown when the WebDriver session is not found or is invalid.
   - **Example**: Trying to use a session after the browser has been closed.

### K. **MoveTargetOutOfBoundsException**
   - **Description**: Thrown when attempting to move the mouse to an element that is outside the viewport.
   - **Example**: Using the `Actions` class to move to an element that is not within the visible area.

### L. **UnhandledAlertException**
   - **Description**: Thrown when there is an unexpected alert on the page and it has not been handled.
   - **Example**: If an alert appears unexpectedly during execution and the script doesn’t handle it.

### M. **JavascriptException**
   - **Description**: Thrown when there is an issue with JavaScript execution.
   - **Example**: Running a `JavascriptExecutor` script that contains an error.

### N. **NotFoundException**
   - **Description**: A generic exception class for not found exceptions (used as a superclass for more specific exceptions like `NoSuchElementException`, `NoSuchFrameException`, etc.).
   - **Example**: Attempting to locate an element that doesn’t exist.

### O. **InvalidArgumentException**
   - **Description**: Thrown when an invalid argument is passed to a method.
   - **Example**: Passing an invalid argument to a method that expects a specific format.

### P. **InvalidCookieDomainException**
   - **Description**: Thrown when trying to set a cookie in a domain that does not match the current domain.
   - **Example**: Attempting to set a cookie with a domain attribute that doesn’t match the current page’s domain.

### Q. **UnsupportedCommandException**
   - **Description**: Thrown when a command is not supported by the driver.
   - **Example**: Using a WebDriver command that is not implemented in a specific browser driver.

### R. **NoSuchSessionException**
   - **Description**: Thrown when the session does not exist (usually because the browser has been closed).
   - **Example**: Trying to interact with the browser after it has been closed.

### S. **UnexpectedAlertPresentException**
   - **Description**: Thrown when an unexpected alert appears, and it is not handled by the script.
   - **Example**: If an alert shows up unexpectedly during a test.

### Handling Exceptions in Selenium:
In your Selenium tests, you should handle these exceptions appropriately to ensure that your tests fail gracefully and provide useful debugging information.

Example of handling a `NoSuchElementException`:

```java
try {
    WebElement element = driver.findElement(By.id("elementId"));
    element.click();
} catch (NoSuchElementException e) {
    System.out.println("Element not found: " + e.getMessage());
}
```

### 2) **how to overcome stale element exception in selenium java**
**occurs when**
The page being refreshed.
Elements being dynamically updated or re-rendered.
Navigation to a new page or frame.
**solution**
A. Relocate the Element
When the DOM changes, the reference to the element becomes stale. To fix this, locate the element again before interacting with it.

Example:

```java
WebElement element = driver.findElement(By.id("myElement"));
// Perform some actions that update the DOM
try {
    element.click(); // This may throw StaleElementReferenceException
} catch (StaleElementReferenceException e) {
    element = driver.findElement(By.id("myElement")); // Relocate the element
    element.click();
}
```
B. Use a WebDriverWait
Using WebDriverWait ensures that the element is re-located or is in a stable state before interacting with it.

Example:

```java
Copy code
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
WebElement element = wait.until(ExpectedConditions.presenceOfElementLocated(By.id("myElement")));

// Perform actions on the element
element.click();
```

C. Handle with Retry Logic
If you suspect the DOM is unstable or changing dynamically, you can implement a retry mechanism to reattempt locating the element.

Example:

```java
public void clickElement(By locator) {
    int attempts = 0;
    while (attempts < 3) {
        try {
            driver.findElement(locator).click();
            break;
        } catch (StaleElementReferenceException e) {
            attempts++;
        }
    }
}
```
