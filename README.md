# xpath-locators-selenium-webdriver

Creating XPath Locators for Selenium WebDriver: A Practical Guide [-->source](https://www.udemy.com/course/xpath-locators-for-selenium/learn/lecture/22800907?start=0#overview)

## Introduction to XPath

### What You Need to Know

XPath (XML Path Language) is a query language for selecting nodes from an XML document. It's widely used in web scraping and automated testing to locate elements on a web page.

### Helpful Tips Before We Start

- Ensure you understand the structure of the web page's HTML.
- Use browser developer tools to inspect elements and test XPath expressions.
- Practice writing simple XPath expressions before moving on to complex queries.

### Page Elements

Web pages are structured using HTML tags, each representing different elements like divs, inputs, buttons, etc. Understanding these tags is crucial for creating effective XPath expressions.

**Tools for Locating Page Elements:**

- **Chrome Dev Tools**: A set of web developer tools built directly into the Google Chrome browser. It allows developers to inspect the HTML and CSS of a webpage, debug JavaScript, and analyze network performance.

- **Mozilla Xpath Finder**: An add-on for Mozilla Firefox that helps users construct and evaluate XPath expressions. It simplifies the process of finding the correct XPath for locating elements on a webpage.

- **Ranorex Selocity**: A free Chrome browser extension for generating and validating XPath and CSS selectors. It provides features to help users create robust selectors for web elements.

- **Selectors Hub**: A Chrome and Firefox extension for generating and editing XPath and CSS selectors. It provides a visual interface for building selectors and supports advanced features for more complex selections.

## Selenium Locators

Selenium provides various ways to locate elements on a web page. Here are the most commonly used locators:

- **ID**
  - Locates an element by its unique ID attribute.
  - Example: `driver.find_element(By.ID, "elementId")`
- **NAME**
  - Locates an element by its name attribute.
  - Example: `driver.find_element(By.NAME, "elementName")`
- **CLASS NAME**
  - Locates elements by their class attribute.
  - Example: `driver.find_element(By.CLASS_NAME, "elementClass")`
- **LINK TEXT**
  - Locates a link (anchor) element by its exact text.
  - Example: `driver.find_element(By.LINK_TEXT, "Click Here")`
- **PARTIAL LINK TEXT**
  - Locates a link element by partial text.
  - Example: `driver.find_element(By.PARTIAL_LINK_TEXT, "Click")`
- **TAG NAME**
  - Locates elements by their tag name.
  - Example: `driver.find_element(By.TAG_NAME, "div")`
- **CSS**
  - Uses CSS selectors to locate elements.
  - Example: `driver.find_element(By.CSS_SELECTOR, ".className #elementId")`
- **XPath**
  - Uses XPath expressions to locate elements.
  - Example: `driver.find_element(By.XPATH, "//div[@id='elementId']/input")`

## Locating Web Elements

To interact with web elements using Selenium, you need to locate them first. Here's a basic example using XPath in Python:

```python
# Import necessary libraries
from selenium import webdriver
from selenium.webdriver.common.by import By

# Set up WebDriver
driver = webdriver.Chrome()

# Open a web page
driver.get("http://example.com")

# Locate an element using XPath
element = driver.find_element(By.XPATH, "//div[@id='exampleId']/input")

# Perform actions on the element
element.send_keys("Sample Text")

# Close the browser
driver.quit()
```