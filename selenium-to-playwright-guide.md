# Playwright with TypeScript for Java + Selenium Users

This cheat sheet is written for engineers who already know **Java, Selenium, RestAssured, and Page Object Model**, and want to learn **Playwright with TypeScript** quickly.

---

## Basic Example

```ts
import { test, expect } from '@playwright/test';

test('Login', async ({ page }) => {
  await page.goto('https://example.com');
  await expect(page).toHaveTitle(/Example/);
});
```

---

## Why `await` is needed

In Java, Selenium code is usually **blocking**, so one line finishes before the next starts.

In Playwright, browser actions are **async**. That means most browser actions return a **Promise** and you must use `await`.

### Java

```java
driver.get("https://example.com");
driver.findElement(By.id("login")).click();
```

### Playwright

```ts
await page.goto('https://example.com');
await page.locator('#login').click();
```

### Rule to remember

> If the line talks to the browser, it usually needs `await`.

---

## Selenium Java vs Playwright TypeScript

### 1) Browser and Navigation

| Action | Selenium Java | Playwright TypeScript |
|---|---|---|
| Open URL | `driver.get("https://site.com");` | `await page.goto('https://site.com');` |
| Get title | `driver.getTitle();` | `await page.title();` |
| Get current URL | `driver.getCurrentUrl();` | `page.url()` |
| Refresh page | `driver.navigate().refresh();` | `await page.reload();` |
| Go back | `driver.navigate().back();` | `await page.goBack();` |
| Go forward | `driver.navigate().forward();` | `await page.goForward();` |
| Close tab/page | `driver.close();` | `await page.close();` |
| Quit browser | `driver.quit();` | Handled automatically by Playwright Test |

---

### 2) Locators

| Locator Type | Selenium Java | Playwright TypeScript |
|---|---|---|
| By ID | `driver.findElement(By.id("user"));` | `page.locator('#user')` |
| By CSS | `driver.findElement(By.cssSelector("input[name='q']"));` | `page.locator("input[name='q']")` |
| By XPath | `driver.findElement(By.xpath("//button[text()='Save']"));` | `page.locator("//button[text()='Save']")` |
| By text | Usually XPath | `page.getByText('Save')` |
| By label | Usually custom XPath | `page.getByLabel('Username')` |
| By placeholder | Usually XPath/CSS | `page.getByPlaceholder('Search')` |
| By role | Usually not direct | `page.getByRole('button', { name: 'Save' })` |
| By test id | Custom attribute | `page.getByTestId('save-btn')` |

---

### 3) Element Actions

| Action | Selenium Java | Playwright TypeScript |
|---|---|---|
| Click | `element.click();` | `await page.locator('#id').click();` |
| Double click | `new Actions(driver).doubleClick(element).perform();` | `await page.locator('#id').dblclick();` |
| Right click | `new Actions(driver).contextClick(element).perform();` | `await page.locator('#id').click({ button: 'right' });` |
| Hover | `new Actions(driver).moveToElement(element).perform();` | `await page.locator('#id').hover();` |
| Drag and drop | `new Actions(driver).dragAndDrop(src, dest).perform();` | `await page.dragAndDrop('#src', '#dest');` |
| Scroll page | `JavascriptExecutor` | `await page.mouse.wheel(0, 500);` |
| Focus element | Usually JS or click | `await page.locator('#id').focus();` |

---

### 4) Input / `sendKeys()` / Keyboard

| Action | Selenium Java | Playwright TypeScript | Notes |
|---|---|---|---|
| Type text | `element.sendKeys("John");` | `await page.locator('#name').fill('John');` | Best for forms |
| Type like real keyboard | `element.sendKeys("John");` | `await page.locator('#name').type('John');` | Character by character |
| Clear and type | `element.clear(); element.sendKeys("John");` | `await page.locator('#name').fill('John');` | `fill()` clears first |
| Clear field only | `element.clear();` | `await page.locator('#name').fill('');` | Simple clear |
| Press Enter in element | `element.sendKeys(Keys.ENTER);` | `await page.locator('#name').press('Enter');` | On that element |
| Global key press | `actions.sendKeys(Keys.ENTER).perform();` | `await page.keyboard.press('Enter');` | On page keyboard |
| Shortcut | `element.sendKeys(Keys.CONTROL, "A");` | `await page.keyboard.press('Control+A');` | Copy/select-all style |
| Sequential typing | N/A | `await page.locator('#name').pressSequentially('Hello');` | Rarely needed |
| Upload file | `element.sendKeys(filePath);` | `await page.locator('input[type=file]').setInputFiles('file.pdf');` | File upload |

---

### 5) Read Data from Elements

| Action | Selenium Java | Playwright TypeScript |
|---|---|---|
| Get text | `element.getText();` | `await page.locator('#id').textContent();` |
| Get input value | `element.getAttribute("value");` | `await page.locator('#id').inputValue();` |
| Get attribute | `element.getAttribute("class");` | `await page.locator('#id').getAttribute('class');` |
| Check visible | `element.isDisplayed();` | `await page.locator('#id').isVisible();` |
| Check enabled | `element.isEnabled();` | `await page.locator('#id').isEnabled();` |
| Check checked | `element.isSelected();` | `await page.locator('#id').isChecked();` |

---

### 6) Assertions

| Assertion | Selenium Java | Playwright TypeScript |
|---|---|---|
| Title | `Assert.assertEquals(driver.getTitle(), "Home");` | `await expect(page).toHaveTitle('Home');` |
| URL | `Assert.assertEquals(driver.getCurrentUrl(), url);` | `await expect(page).toHaveURL(url);` |
| Visible element | `Assert.assertTrue(element.isDisplayed());` | `await expect(locator).toBeVisible();` |
| Hidden element | Custom logic | `await expect(locator).toBeHidden();` |
| Element text | `Assert.assertEquals(element.getText(), "Hello");` | `await expect(locator).toHaveText('Hello');` |
| Partial text | Custom logic | `await expect(locator).toContainText('Hello');` |
| Input value | `Assert.assertEquals(element.getAttribute("value"), "abc");` | `await expect(locator).toHaveValue('abc');` |
| Count | Custom list size assert | `await expect(locator).toHaveCount(3);` |
| Checked checkbox | `Assert.assertTrue(element.isSelected());` | `await expect(locator).toBeChecked();` |
| Enabled | `Assert.assertTrue(element.isEnabled());` | `await expect(locator).toBeEnabled();` |

> In Playwright, prefer `expect(locator)...` over `isVisible()` for test validation because `expect()` auto-waits and fails properly.

---

### 7) Waits

| Action | Selenium Java | Playwright TypeScript | Notes |
|---|---|---|---|
| Hard wait | `Thread.sleep(5000);` | `await page.waitForTimeout(5000);` | Avoid when possible |
| Explicit wait visible | `WebDriverWait + ExpectedConditions.visibilityOfElementLocated(...)` | `await expect(locator).toBeVisible();` | Preferred |
| Wait for URL | Custom explicit wait | `await page.waitForURL('**/dashboard');` | Good after navigation |
| Wait for load | `document.readyState` logic | `await page.waitForLoadState('load');` | Use when needed |
| Wait for network idle | Custom JS/network logic | `await page.waitForLoadState('networkidle');` | Use carefully |

### Playwright advantage

Most actions in Playwright already **auto-wait**, so you usually do **not** need lots of explicit waits like Selenium.

---

### 8) Dropdowns, Checkboxes, Radio Buttons

| Action | Selenium Java | Playwright TypeScript |
|---|---|---|
| Select dropdown by value | `new Select(element).selectByValue("IN");` | `await page.locator('#country').selectOption('IN');` |
| Select dropdown by label | `new Select(element).selectByVisibleText("India");` | `await page.locator('#country').selectOption({ label: 'India' });` |
| Select dropdown by index | `new Select(element).selectByIndex(2);` | `await page.locator('#country').selectOption({ index: 2 });` |
| Check checkbox | `if (!element.isSelected()) element.click();` | `await page.locator('#agree').check();` |
| Uncheck checkbox | Custom logic | `await page.locator('#agree').uncheck();` |
| Radio button | `element.click();` | `await page.locator('#male').check();` |

---

### 9) Screenshots, Videos, Traces

| Action | Selenium Java | Playwright TypeScript |
|---|---|---|
| Page screenshot | `((TakesScreenshot) driver).getScreenshotAs(...)` | `await page.screenshot({ path: 'page.png' });` |
| Element screenshot | Usually crop manually | `await page.locator('#card').screenshot({ path: 'card.png' });` |
| Attach screenshot to report | Framework-specific | `await testInfo.attach('name', { body: buffer, contentType: 'image/png' });` |
| Record trace | Usually external/reporting tools | `trace: 'on-first-retry'` in config |
| Record video | Framework/grid specific | `video: 'retain-on-failure'` in config |

---

### 10) Frames, Alerts, Tabs, Windows

| Action | Selenium Java | Playwright TypeScript |
|---|---|---|
| Switch to frame by name/id | `driver.switchTo().frame("frame1");` | `const frame = page.frame({ name: 'frame1' });` |
| Work inside iframe | `driver.switchTo().frame(element);` | `const frameLocator = page.frameLocator('#frame');` |
| Switch back to main page | `driver.switchTo().defaultContent();` | Not needed with `frameLocator`; otherwise use `page` again |
| Handle alert accept | `driver.switchTo().alert().accept();` | `page.on('dialog', dialog => dialog.accept());` |
| Handle alert dismiss | `driver.switchTo().alert().dismiss();` | `page.on('dialog', dialog => dialog.dismiss());` |
| New tab/window | `driver.switchTo().newWindow(WindowType.TAB);` | `const newPage = await context.newPage();` |
| Capture popup window | Custom window handles logic | `const popup = await page.waitForEvent('popup');` |

---

### 11) Mouse and Advanced UI Actions

| Action | Selenium Java | Playwright TypeScript |
|---|---|---|
| Mouse move | `Actions.moveToElement(element).perform();` | `await page.locator('#menu').hover();` |
| Mouse click at coordinates | `Actions.moveByOffset(x, y).click().perform();` | `await page.mouse.click(x, y);` |
| Mouse down | Rare/custom | `await page.mouse.down();` |
| Mouse up | Rare/custom | `await page.mouse.up();` |
| Drag with mouse | `Actions.clickAndHold().moveToElement().release()` | `await page.dragAndDrop('#src', '#dest');` |

---

## Common XPath to Playwright-Friendly Locators

| XPath | Better Playwright Syntax |
|---|---|
| `//input[@placeholder='Search']` | `page.getByPlaceholder('Search')` |
| `//span[text()='Senior Partner']` | `page.getByText('Senior Partner')` |
| `//button[text()='Add']` | `page.getByRole('button', { name: 'Add' })` |
| `//label[text()='Username']/following-sibling::input` | `page.getByLabel('Username')` if label is linked properly |
| `//input[@id='user']` | `page.locator('#user')` |

---

## `fill()` vs `type()` vs `press()`

| Method | Syntax | Use Case |
|---|---|---|
| `fill()` | `await locator.fill('John')` | Best for input fields; clears existing value first |
| `type()` | `await locator.type('John')` | Simulates typing character by character |
| `press()` | `await locator.press('Enter')` | Press a keyboard key on that element |
| `keyboard.press()` | `await page.keyboard.press('Control+A')` | Global keyboard shortcuts |

---

## Small Utility Method Example

If you have a repeated block like search -> select -> clear, move it to a utility function.

```ts
import { Page, expect } from '@playwright/test';

export async function searchSelectClear(page: Page, text: string) {
  await page.getByPlaceholder('Search').fill(text);
  await expect(page.getByText(text, { exact: true })).toBeVisible();
  await page.locator(`//span[text()='${text}']/following-sibling::i`).click();
  await page.locator("i[data-icon-name='Clear']").click();
}
```

Usage:

```ts
await searchSelectClear(page, 'Senior Partner');
```

---

## Basic Playwright Test Structure

```ts
import { test, expect } from '@playwright/test';

test('Login', async ({ page }) => {
  await page.goto('https://pricing-staging.bain.com/login2');
  await page.getByText('Log in as test user 2').click();
  await expect(page).toHaveTitle('Configurator');
  await page.getByLabel('Opportunity Name').fill('Specific Resource Flags');
  await expect(page.getByText('Specific Resource Flags')).toBeVisible();
});
```

---

## Playwright Config Example

```ts
import { defineConfig } from '@playwright/test';

export default defineConfig({
  testDir: './tests',
  reporter: 'html',
  use: {
    browserName: 'chromium',
    headless: false,
    viewport: null,
    launchOptions: {
      args: ['--start-maximized'],
    },
    trace: 'on-first-retry',
    screenshot: 'only-on-failure',
    video: 'retain-on-failure',
  },
});
```

---

## Quick Notes for Selenium Users

- Playwright has **auto-waiting**, so fewer explicit waits are needed.
- Prefer `getByRole`, `getByText`, `getByLabel`, `getByPlaceholder` over XPath when possible.
- Use `expect()` for assertions instead of only checking `isVisible()`.
- Use `fill()` instead of `sendKeys()` for most form fields.
- Use `page.locator()` for flexible targeting.
- Browser setup and cleanup are mostly handled by Playwright Test.

---

## Suggested File Name

Use one of these names in GitHub:

- `README.md`
- `playwright-typescript-cheatsheet.md`
- `selenium-to-playwright-guide.md`

