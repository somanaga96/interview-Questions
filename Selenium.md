1)Select the option without Select Class

Ans : 
driver.get("https://letcode.in/dropdowns");
        WebElement state = driver.findElement(By.cssSelector("select#fruits"));
        state.click();
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(5));
        WebElement option = wait.until(ExpectedConditions.elementToBeClickable(
                By.xpath("//option[text()='Banana']")
        ));
        option.click();
2)  Exception
Selenium provides a wide range of exceptions to handle different scenarios that can occur during the execution of automated tests. Here’s a list of common exceptions in Selenium and their explanations:

### 1. **NoSuchElementException**
   - **Description**: Thrown when an element could not be found in the DOM.
   - **Example**: Trying to find an element that doesn’t exist using `findElement(By.id("nonExistentId"))`.

 ### 2. **ElementNotVisibleException**
   - **Description**: Thrown when an element is present in the DOM but is not visible (i.e., it has a `display: none` or `visibility: hidden` CSS property).
   - **Example**: Trying to click on an element that exists in the DOM but is hidden.

### 3. **TimeoutException**
   - **Description**: Thrown when a command does not complete in the specified time.
   - **Example**: Waiting for an element to appear using `WebDriverWait` but it never does.



### 4. **StaleElementReferenceException**
   - **Description**: Thrown when a reference to an element is now "stale" because the element is no longer present in the DOM.
   - **Example**: After a page refresh or a navigation, the element reference becomes stale.

### 5. **NoSuchFrameException**
   - **Description**: Thrown when the frame being switched to is not found.
   - **Example**: Trying to switch to a frame that doesn’t exist using `driver.switchTo().frame("frameName")`.

### 6. **NoSuchWindowException**
   - **Description**: Thrown when trying to switch to a window that is not found.
   - **Example**: Attempting to switch to a window that has been closed or never existed.

### 7. **NoAlertPresentException**
   - **Description**: Thrown when switching to an alert, but the alert is not present.
   - **Example**: Using `driver.switchTo().alert()` when there is no alert displayed.

### 8. **InvalidElementStateException**
   - **Description**: Thrown when a command could not be completed because the element is in an invalid state.
   - **Example**: Trying to interact with an input element that is disabled.

### 9. **ElementClickInterceptedException**
   - **Description**: Thrown when an element is clicked but the click is intercepted by another element (like a popup or overlay).
   - **Example**: Clicking a button that is covered by another element.

### 10. **InvalidSelectorException**
   - **Description**: Thrown when the selector used to find an element is not valid.
   - **Example**: Using an XPath expression or CSS selector that is syntactically incorrect.

### 11. **ElementNotSelectableException**
   - **Description**: Thrown when trying to select an element that cannot be selected.
   - **Example**: Attempting to select a disabled dropdown option.

### 12. **WebDriverException**
   - **Description**: The base exception class in Selenium. It is thrown when something goes wrong with the WebDriver.
   - **Example**: Issues with the driver or communication between the browser and Selenium.

### 13. **SessionNotFoundException**
   - **Description**: Thrown when the WebDriver session is not found or is invalid.
   - **Example**: Trying to use a session after the browser has been closed.

### 14. **MoveTargetOutOfBoundsException**
   - **Description**: Thrown when attempting to move the mouse to an element that is outside the viewport.
   - **Example**: Using the `Actions` class to move to an element that is not within the visible area.

### 15. **UnhandledAlertException**
   - **Description**: Thrown when there is an unexpected alert on the page and it has not been handled.
   - **Example**: If an alert appears unexpectedly during execution and the script doesn’t handle it.

### 16. **JavascriptException**
   - **Description**: Thrown when there is an issue with JavaScript execution.
   - **Example**: Running a `JavascriptExecutor` script that contains an error.

### 17. **NotFoundException**
   - **Description**: A generic exception class for not found exceptions (used as a superclass for more specific exceptions like `NoSuchElementException`, `NoSuchFrameException`, etc.).
   - **Example**: Attempting to locate an element that doesn’t exist.

### 18. **InvalidArgumentException**
   - **Description**: Thrown when an invalid argument is passed to a method.
   - **Example**: Passing an invalid argument to a method that expects a specific format.

### 19. **InvalidCookieDomainException**
   - **Description**: Thrown when trying to set a cookie in a domain that does not match the current domain.
   - **Example**: Attempting to set a cookie with a domain attribute that doesn’t match the current page’s domain.

### 20. **UnsupportedCommandException**
   - **Description**: Thrown when a command is not supported by the driver.
   - **Example**: Using a WebDriver command that is not implemented in a specific browser driver.

### 21. **NoSuchSessionException**
   - **Description**: Thrown when the session does not exist (usually because the browser has been closed).
   - **Example**: Trying to interact with the browser after it has been closed.

### 22. **UnexpectedAlertPresentException**
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

Understanding these exceptions helps you write more robust and error-tolerant Selenium tests.
