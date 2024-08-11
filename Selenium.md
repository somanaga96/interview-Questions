1)Selection the option without Select Class
Ans : 
driver.get("https://letcode.in/dropdowns");
        WebElement state = driver.findElement(By.cssSelector("select#fruits"));
        state.click();
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(5));
        WebElement option = wait.until(ExpectedConditions.elementToBeClickable(
                By.xpath("//option[text()='Banana']")
        ));
        option.click();
2)  
