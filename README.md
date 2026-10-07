# Automation_Tasks
# code
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Chrome()

# --------------------------------
# TC01 - Open Shopping Website
# --------------------------------

driver.get("https://www.saucedemo.com/")

wait = WebDriverWait(driver, 10)

driver.find_element(By.ID, "user-name").send_keys("standard_user")
driver.find_element(By.ID, "password").send_keys("secret_sauce")
driver.find_element(By.ID, "login-button").click()

print("Login completed")

time.sleep(2)


# --------------------------------
# Open Alert Demo Page
# --------------------------------

driver.get("https://www.selenium.dev/selenium/web/alerts.html")


# --------------------------------
# TC02 - Confirmation Alert Accept
# --------------------------------

element=driver.find_element(By.ID, "confirm")
element.click()

alert = wait.until(EC.alert_is_present())

print("\nTC02 - Confirmation Alert:")
print(alert.text)

time.sleep(2)

# Click OK
alert.accept()

print("TC02 - Alert accepted successfully")


# --------------------------------
# TC03 - Confirmation Alert Dismiss
# --------------------------------
driver.get("https://www.selenium.dev/selenium/web/alerts.html")

element=driver.find_element(By.ID, "confirm")
element.click()

alert = wait.until(EC.alert_is_present())

print("\nTC03 - Confirmation Alert:")
print(alert.text)

time.sleep(2)

# Click Cancel
alert.dismiss()

print("TC03 - Alert dismissed successfully")


# --------------------------------
# TC04 - Prompt Alert
# --------------------------------

driver.find_element(By.ID, "prompt").click()

alert = wait.until(EC.alert_is_present())

print("\nTC04 - Prompt Alert:")
print(alert.text)

time.sleep(2)

# Enter information
alert.send_keys("Sriram")

print("Information entered: Sriram")

time.sleep(2)

# Click OK
alert.accept()

print("TC04 - Customer information submitted successfully")


#-------------------
#task 5 mouse hover
#-----------
driver.get("https://www.selenium.dev/selenium/web/mouse_interaction.html")

wait = WebDriverWait(driver, 10)

# Find the hover element
hover_element = wait.until(
    EC.visibility_of_element_located((By.ID, "hover"))
)

# Create ActionChains object
actions = ActionChains(driver)

# Move mouse over the element
actions.move_to_element(hover_element).perform()

print("Mouse hover completed")

# Verify hover result
status = driver.find_element(By.ID, "move-status").text

print("Status:", status)

if status == "hovered":
    print("TC05 Passed - Mouse hover successful")
else:
    print("TC05 Failed")







#-----------------
#Task 6
#--------------
driver.get("https://www.selenium.dev/selenium/web/mouse_interaction.html")

wait = WebDriverWait(driver, 10)

# Find the clickable element
product = wait.until(
    EC.visibility_of_element_located((By.ID, "clickable"))
)
time.sleep(2)

# Create ActionChains object
actions = ActionChains(driver)

# Double click
actions.double_click(product).perform()

print("Product double-clicked successfully")

# Verify result
status = driver.find_element(By.ID, "click-status").text

print("Status:", status)

if status == "double-clicked":
    print("TC06 Passed - Double click completed successfully")
else:
    print("TC06 Failed")

#drag and drop
# task 7

driver.get("https://www.selenium.dev/selenium/web/mouse_interaction.html")

wait = WebDriverWait(driver, 10)

# Find draggable item
source = wait.until(
    EC.visibility_of_element_located((By.ID, "draggable"))
)

# Find drop area
target = wait.until(
    EC.visibility_of_element_located((By.ID, "droppable"))
)

# Create ActionChains object
actions = ActionChains(driver)

# Drag source and drop it into target
actions.drag_and_drop(source, target).perform()
print("TC07 - Drag and Drop:")
print("Item dragged and dropped successfully")
time.sleep(3)

#------------------

#task 8
#-------------


driver.get("https://automationexercise.com/")

wait = WebDriverWait(driver, 10)


# --------------------------------
# TC08 - Search Product
# --------------------------------

# Click Products
products_button = wait.until(
    EC.element_to_be_clickable(
        (By.XPATH, "//a[@href='/products']")
    )
)

products_button.click()

print("Products page opened")


# --------------------------------
# Find Search Box
# --------------------------------

search_box = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "search_product")
    )
)

print("Search box displayed")


# Enter product name
search_box.send_keys("Men Tshirt")

print("Product name entered")


# --------------------------------
# Click Search
# --------------------------------

search_button = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "submit_search")
    )
)

search_button.click()

print("Search button clicked")


# --------------------------------
# Explicit Wait for Results
# --------------------------------

searched_products = wait.until(
    EC.visibility_of_element_located(
        (By.XPATH, "//h2[contains(text(),'Searched Products')]")
    )
)

print("Search results loaded")


# --------------------------------
# Verify product
# --------------------------------

product = wait.until(
    EC.visibility_of_element_located(
        (By.XPATH, "//div[@class='productinfo text-center']//p[text()='Blue Top']")
    )
)

print("Product displayed:", product.text)

print("TC08 Passed - Product displayed successfully")
#----------
#testcase 9
#-----------


driver.get("https://www.saucedemo.com/")

wait = WebDriverWait(driver, 10)


# --------------------------------
# Login
# --------------------------------

driver.find_element(By.ID, "user-name").send_keys("standard_user")
driver.find_element(By.ID, "password").send_keys("secret_sauce")
driver.find_element(By.ID, "login-button").click()

print("Login completed")


# --------------------------------
# Add Product
# --------------------------------

add_product = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "add-to-cart-sauce-labs-backpack")
    )
)

add_product.click()

print("Product added to cart")


# --------------------------------
# Open Cart
# --------------------------------

cart = wait.until(
    EC.element_to_be_clickable(
        (By.CLASS_NAME, "shopping_cart_link")
    )
)

cart.click()

print("Cart opened")


# --------------------------------
# Checkout
# --------------------------------

checkout = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "checkout")
    )
)

checkout.click()

print("Checkout started")


# --------------------------------
# Enter Customer Information
# --------------------------------

wait.until(
    EC.visibility_of_element_located(
        (By.ID, "first-name")
    )
).send_keys("Sriram")

driver.find_element(By.ID, "last-name").send_keys("E")
driver.find_element(By.ID, "postal-code").send_keys("600001")

print("Customer information entered")


# --------------------------------
# Continue
# --------------------------------

continue_button = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "continue")
    )
)

continue_button.click()

print("Checkout overview opened")


# --------------------------------
# TC09 - Clickable Wait
# --------------------------------

place_order = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "finish")
    )
)

print("Place Order button is clickable")


# Click Place Order
place_order.click()

print("Order submitted successfully")


# --------------------------------
# Verify Order
# --------------------------------

confirmation = wait.until(
    EC.visibility_of_element_located(
        (By.CLASS_NAME, "complete-header")
    )
)

print("Confirmation:", confirmation.text)

print("TC09 Passed - Order submitted successfully")

# =========================
# TC10 - Alert Wait
# =========================

driver.get("https://www.saucedemo.com/")

wait = WebDriverWait(driver, 10)

# Login
driver.find_element(By.ID, "user-name").send_keys("standard_user")
driver.find_element(By.ID, "password").send_keys("secret_sauce")
driver.find_element(By.ID, "login-button").click()

print("\nTC10 - Login completed")

# Add product
add_product = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "add-to-cart-sauce-labs-backpack")
    )
)
add_product.click()

print("TC10 - Product added to cart")

# Open cart
cart = wait.until(
    EC.element_to_be_clickable(
        (By.CLASS_NAME, "shopping_cart_link")
    )
)
cart.click()

print("TC10 - Cart opened")

# Click checkout
checkout = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "checkout")
    )
)
checkout.click()

print("TC10 - Checkout started")

# Enter customer information
first_name = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "first-name")
    )
)
first_name.send_keys("Sriram")

driver.find_element(By.ID, "last-name").send_keys("E")
driver.find_element(By.ID, "postal-code").send_keys("600001")

print("TC10 - Customer information entered")

# Continue
continue_button = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "continue")
    )
)
continue_button.click()

print("TC10 - Checkout overview opened")

# Wait for Finish button
place_order = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "finish")
    )
)

print("TC10 - Finish button is clickable")

# Add JavaScript alert to Finish button
driver.execute_script("""
    arguments[0].addEventListener('click', function() {
        alert('Order placed successfully!');
    });
""", place_order)

# Click Finish
place_order.click()

# Wait for confirmation alert
alert = wait.until(
    EC.alert_is_present()
)

print("TC10 - Confirmation Alert:")
print(alert.text)

# Accept alert
alert.accept()

print("TC10 Passed - Confirmation alert handled successfully")


input("\nPress Enter to close browser...")

driver.quit()
```

#output
<img width="1251" height="956" alt="image" src="https://github.com/user-attachments/assets/017a3fab-6b8c-4467-a9dd-bfbc9f202f6c" />
<img width="1257" height="927" alt="image" src="https://github.com/user-attachments/assets/34577382-0114-49cf-bf38-01ef3e41de70" />
<img width="1247" height="916" alt="image" src="https://github.com/user-attachments/assets/fdf8af75-e4f7-4c40-a294-7ca2fa2ff5c6" />
<img width="1273" height="921" alt="image" src="https://github.com/user-attachments/assets/29815034-ad8d-4117-83f1-be5d50ced07b" />
<img width="1272" height="971" alt="image" src="https://github.com/user-attachments/assets/563729fc-ce11-4ca4-818d-9bd1cd8f3344" />





