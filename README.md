# xpath-locators-selenium-webdriver

Creating XPath Locators for Selenium WebDriver: A Practical Guide  
[source](https://www.udemy.com/course/xpath-locators-for-selenium/learn/lecture/22800907?start=0#overview)

## Introduction to XPath

### What You Need to Know

XPath (XML Path Language) is a query language for selecting nodes from an XML document. It's widely used in web scraping and automated testing to locate elements on a web page.

### Helpful Tips Before We Start

* Ensure you understand the structure of the web page's HTML.
* Use browser developer tools to inspect elements and test XPath expressions.
* Practice writing simple XPath expressions before moving on to complex queries.

### Page Elements

Web pages are structured using HTML tags, each representing different elements like divs, inputs, buttons, etc. Understanding these tags is crucial for creating effective XPath expressions.

 **Tools for Locating Page Elements:** 

* **Chrome Dev Tools** : A set of web developer tools built directly into the Google Chrome browser. It allows developers to inspect the HTML and CSS of a webpage, debug JavaScript, and analyze network performance.

* **Mozilla Xpath Finder** : An add-on for Mozilla Firefox that helps users construct and evaluate XPath expressions. It simplifies the process of finding the correct XPath for locating elements on a webpage.

* **Ranorex Selocity** : A free Chrome browser extension for generating and validating XPath and CSS selectors. It provides features to help users create robust selectors for web elements.

* **Selectors Hub** : A Chrome and Firefox extension for generating and editing XPath and CSS selectors. It provides a visual interface for building selectors and supports advanced features for more complex selections.

## Selenium Locators

Selenium provides various ways to locate elements on a web page. Here are the most commonly used locators:

* **ID** 
  + Locates an element by its unique ID attribute.
  + Example: `driver.find_element(By.ID, "elementId")`
* **NAME** 
  + Locates an element by its name attribute.
  + Example: `driver.find_element(By.NAME, "elementName")`
* **CLASS NAME** 
  + Locates elements by their class attribute.
  + Example: `driver.find_element(By.CLASS_NAME, "elementClass")`
* **LINK TEXT** 
  + Locates a link (anchor) element by its exact text.
  + Example: `driver.find_element(By.LINK_TEXT, "Click Here")`
* **PARTIAL LINK TEXT** 
  + Locates a link element by partial text.
  + Example: `driver.find_element(By.PARTIAL_LINK_TEXT, "Click")`
* **TAG NAME** 
  + Locates elements by their tag name.
  + Example: `driver.find_element(By.TAG_NAME, "div")`
* **CSS** 
  + Uses CSS selectors to locate elements.
  + Example: `driver.find_element(By.CSS_SELECTOR, ".className #elementId")`
* **XPath** 
  + Uses XPath expressions to locate elements.
  + Example: `driver.find_element(By.XPATH, "//div[@id='elementId']/input")`

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

## XPath Basics

Note: All the path examples below refer to this [Test Page](https://practicetestautomation.com/practice-test-exceptions/).

### XPath Terminology

* **Relationship of Nodes:** 
  + **Parents:** The immediate ancestor of a node.
  + **Children:** The immediate descendants of a node.
  + **Siblings:** Nodes that share the same parent.
  + **Ancestors:** Any node higher in the hierarchy.
  + **Descendants:** Any node lower in the hierarchy.

### Types of XPath

* **Absolute XPath (Avoid using this)** 
  + An absolute path starts from the root element and goes down to the target element.
  + Example: `/html/body/div/div/section/section/div/div/div/input`
* **Relative XPath (Always use this, most reliable)** 
  + A relative path starts from the current node and is more flexible.
  + Example: `//div[@id='row1']/input`

### Basic XPath Syntax

#### General Syntax

* **Structure:** `//tag[@attribute='value']`
* **Example:** `//div[@id='row1']/input`

#### Key Components

* **Relative XPath:** `//`
  + Selects nodes in the document from the current node that match the selection, regardless of their location.
* **Tag Element:** `div`
  + Selects all `<div>` elements.
* **Predicate:** `[@id='row1']`
  + Filters nodes with an `id` attribute equal to 'row1'.
* **Child Node:** `/input`
  + Selects the `<input>` child of the matched `<div>` element.

### `/` vs `//` vs `./` vs `.//` 

* **Single forward slash `/`** 
  + Represents an absolute path from the root node.
  + Selects a child node.
  + Example: `/html/body/div/div/section/section/div/div/div/input`
* **Double forward slash `//`** 
  + Represents a relative path.
  + Selects nodes anywhere in the document that match the selection.
  + Example: `//div[@id='rows']//input`
* **Dot-slash `./`** 
  + Represents a relative path starting at the current node.
* **Dot-double-slash `.//`** 
  + Selects nodes relative to the context node.
  + Example usage:

```python
rows = driver.find_elements(By.XPATH, "//div[@id='row2']/*[@id='save_btn']")
for row in rows:
    label = row.find_element(By.XPATH, ".//label").text
    print("Label text is:", label)
```

### Position and Index

When the best XPath expression still returns more than one element, you can use position and index to select a specific element.

#### Index Method

The index method selects a single element from a list of matched elements. Remember, XPath indexing starts at 1.

* **Example:** `//h5[2]`
  + Selects the second `<h5>` element.

* **Index After an Expression:** 
  + Use parentheses to group the expression and apply the index.
  + **Example:** `(//div[@class='row'])[2]`
    - Finds all `<div>` elements with the class `row` and selects the second one.
  + **Another Example:** `(//div[@class='row']/button)[6]`
    - Finds all `<button>` elements under all `<div>` elements with the class `row` and selects the sixth button.

#### Position Method

The position method allows the use of conditional operators to refine the selection.

* **Equal to:** `//h5[position()=2]`
  + Selects the second `<h5>` element.
* **Not Equal to:** `//h5[position()!=2]`
  + Selects all `<h5>` elements except the second one.
* **Less Than:** `//h5[position()<2]`
  + Selects all `<h5>` elements before the second one.
* **Less Than or Equal to:** `//h5[position()<=2]`
  + Selects the first and second `<h5>` elements.
* **Greater Than:** `//h5[position()>2]`
  + Selects all `<h5>` elements after the second one.
* **Greater Than or Equal to:** `//h5[position()>=2]`
  + Selects the second `<h5>` element and all subsequent ones.
* **Last:** `//h5[last()]`
  + Selects the last `<h5>` element.
* **One Element Before Last:** `//h5[last()-1]`
  + Selects the second-to-last `<h5>` element.

### More Useful XPath Functions

#### `text()` 

Used to select elements based on their text content.

* **General Syntax:** `//tag[text()='value']`
* **Example:** `//h5[text()='Create list of your favorite foods']`

#### `contains()` 

Useful when dealing with partially dynamic values.

* **General Syntax:** `//tag[contains(@attribute, 'partial value')]`
* **Example:** `//button[contains(@id, 'login')]`
* Can also be used with `text()`
  + **General Syntax:** `//tag[contains(text(), 'partial value')]`
  + **Example:** `//p[contains(text(), 'to add')]`

#### `starts-with()` 

Used to select elements whose attribute value starts with a specific string.

* **General Syntax:** `//tag[starts-with(@attribute, 'beginning')]`
* **Example:** `//input[starts-with(@class, 'input')]`
* Can also be used with `text()`
  + **General Syntax:** `//tag[starts-with(text(), 'beginning')]`
  + **Example:** `//p[starts-with(text(), 'Let’s learn')]`

#### `not()` 

Used to select elements that do not match the given criteria.

* **General Syntax:** `//tag[not(text()='value')]`
* **Example:** `//h5[not(text()='Create list of your favorite foods')]`
* Can also be combined with other functions.
  + **Example:** `//tag[not(contains(@attribute,'partial value'))]`
  + **Example:** `//tag[not(starts-with(text(),'beginning'))]`

## Advanced XPath

### XPath Operators

XPath provides various operators, including `+` , `-` , `*` , `div` , `=` , `!=` , `<` , `>` , `or` , and `and` . Among these, the `or` and `and` operators are particularly useful for creating flexible and robust XPath expressions. Sometimes different locators are needed for different browsers or mobile devices. For instance, you might need:

* `btn = By.XPATH("//div[@id='btn']")`
* `safariBtn = By.XPATH("//div[@id='btn']/div")`

In such cases, you can use the `or` and `and` operators to handle different scenarios effectively.

#### Example usage of `or` and `and` operators:

* `//button[@name='Add' or @name='Remove']`
* `//button[@name='Add' or @id='remove_btn']`
* `//button[@class and @name='Save']`
* `//button[@class='btn' and not(@style='display: none;')]`
* Using two sets of predicates: `//button[@class='btn'][not(@style='display: none;')]`

### XPath Wildcards

Wildcards in XPath are useful for creating expressions that match unknown XML nodes.

#### General Syntax:

* `//*[@*='value']`
  + The first `*` matches any element node.
  + The second `*` matches any attribute node.

#### Example:

* Match any attribute node: `//button[@*='btn']`

### XPath Axes

XPath axes are essential for navigating through complex XML documents, especially when elements do not have attributes, such as `<tr>` , `<td>` , `<ul>` , or `<li>` elements.

#### Types of XPath Axes:

* `ancestor`
* `descendant`
* `parent`
* `following-sibling`
* `preceding-sibling`

#### General Syntax:

* `axisname::nodetest[predicate]`

#### Examples:

* Find the parent `div` with no attributes: `//div[@id='row1']/parent::div`
* Replace `//section/ol[2]/li[2]` with: `//h5[contains(text(),'Test case 2')]/following-sibling::ol/li[2]`
* Find the heading based on text under the heading: `//li[text()='Verify text saved']/parent::ol/preceding-sibling::h5[1]`

[XPath Axes: Ancestor, Following Sibling, Preceding](https://www.scientecheasy.com/2019/08/xpath-axes.html/#google_vignette)

### Finding Elements Relative to Other Elements

You can locate parent or child elements using relative XPath expressions.

#### Examples:

* Find a `div` element relative to a child `input` element: `//div[./input]`
* Find the parent `div` of an `input` element: `//input/parent::div`
* Find an `input` element relative to a parent `div` with `id='row2'`: `//input[parent::div[@id='row2']]`
  + Simpler expression: `//div[@id='row2']/input`

### Selecting Several Paths

Sometimes, combining two XPath expressions into one is necessary, especially when you want to get a list of elements that have different locators.

#### Examples:

* `//div[@class='row'] | //input[@id='text']`
* Choose all `h2` and `h5` elements: `//h2 | //h5`
* Choose all buttons and input fields under `row1`: `//div[@id='row1']/button | //div[@id='row1']/input`
* Choose all headers and paragraphs: `//h2 | //h5 | //p`

### SVG Elements

Standard XPath formulas do not work with SVG elements due to different rules, but they can still be managed.

#### Examples:

* This won't work: `//rect[@y='11']`
* Use a wildcard for the tag name: `//*[@y='11']`
* Use the `name()` function to locate the element:
  + `//*[name()='rect' and @y='11']`
  + `//*[name()='symbol' and @id='icon-amazon']/*[name()='path']`

[SVG Explained](https://www.youtube.com/watch?v=emFMHH2Bfvo)

### Stopping Page Load

To inspect HTML elements that appear briefly, such as a ‘loading’ element, you can use Chrome DevTools to set breakpoints.

#### Example:

* Set an event listener breakpoint: 
  + Chrome DevTools → Sources → Event Listener Breakpoints → Mouse → Check 'click'
* Step through the debugger until the element appears.
* Click the ‘Select element in page’ button in the top left.
* Inspect the loading element on the screen.

## Pros and Cons of XPath

### XPath versus CSS

The debate between XPath and CSS as locator strategies is ongoing among developers, with each having its own proponents.

#### Preferences:

* **CSS:** Preferred by some for its ease of learning and speed.
* **XPath:** Favored by others for its power and flexibility in locating any element on a page.

#### Common Misconceptions:

* **Is XPath slow?** 
  + There is no noticeable difference in speed between XPath and CSS selectors. Locator strategy does not significantly impact test performance.
  + Test slowness is often due to poorly written tests: overly complex, too many steps, or not atomic.
  + For slow regression tests, consider optimizing test steps or running tests in parallel rather than focusing on the locator strategy.

* **Is XPath difficult to learn?** 
  + Not particularly. Once learned, XPath enables you to create your own locators without needing assistance from other developers.

#### Advantages of XPath:

* **Access Element Content:** 
  + CSS selectors cannot access the content of elements, whereas XPath can.
  + Example: `//h5[text()='Create']`
* **Traverse the DOM:** 
  + XPath can navigate up the DOM, which CSS cannot do.
  + Example: `//div[@id='row1']/parent::div`

#### Advantages of CSS:

* **Familiarity:** 
  + Most web developers are familiar with CSS, while not all know XPath.

[CSS vs. XPath](https://elementalselenium.com/tips/32-css-vs-xpath)
