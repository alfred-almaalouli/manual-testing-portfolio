# Test Cases – Sauce Demo

Priority: **H** = high, **M** = medium, **L** = low. All tests start on https://www.saucedemo.com in a new browser session. Password for all accounts: `secret_sauce`.

## Login

| ID | Title | Steps | Expected result | Prio |
|----|-------|-------|-----------------|------|
| TC-L01 | Valid login | 1. Enter `standard_user` / `secret_sauce` 2. Click *Login* | Products page with title "Products" is shown | H |
| TC-L02 | Wrong password | 1. Enter `standard_user` / `wrong` 2. Click *Login* | Error "Username and password do not match any user in this service"; user stays on login page | H |
| TC-L03 | Empty username | 1. Leave username empty, enter password 2. Click *Login* | Error "Username is required" | M |
| TC-L04 | Empty password | 1. Enter username, leave password empty 2. Click *Login* | Error "Password is required" | M |
| TC-L05 | Locked user | 1. Log in as `locked_out_user` | Error "Sorry, this user has been locked out." | H |
| TC-L06 | Error message can be closed | 1. Produce any login error 2. Click the X on the message | Message disappears, red field markers are removed | L |
| TC-L07 | Logout | 1. Log in 2. Open menu 3. Click *Logout* | Login page is shown | H |
| TC-L08 | Protected page | 1. Without login open `/inventory.html` | Error "You can only access '/inventory.html' when you are logged in." | H |
| TC-L09 | Back button after logout | 1. Log in, log out 2. Press browser *Back* | Products page is not accessible | M |

## Products

| ID | Title | Steps | Expected result | Prio |
|----|-------|-------|-----------------|------|
| TC-P01 | Product list | 1. Log in | 6 products with name, description, price, image and *Add to cart* | H |
| TC-P02 | Product images | 1. Log in 2. Compare images with product names | Every product shows its own matching image | M |
| TC-P03 | Sort A–Z / Z–A | 1. Select "Name (Z to A)" 2. Select "Name (A to Z)" | List is sorted accordingly | M |
| TC-P04 | Sort by price | 1. Select "Price (low to high)" 2. Select "Price (high to low)" | List is sorted by price | M |
| TC-P05 | Product detail | 1. Click a product name | Detail page of **the same** product with the same price | H |
| TC-P06 | Back to products | 1. Open detail page 2. Click *Back to products* | Products page | L |

## Cart

| ID | Title | Steps | Expected result | Prio |
|----|-------|-------|-----------------|------|
| TC-C01 | Add one product | 1. Click *Add to cart* on one product | Badge shows 1, button changes to *Remove* | H |
| TC-C02 | Add all products | 1. Add all 6 products | Badge shows 6 | M |
| TC-C03 | Remove from list | 1. Add 2 products 2. Click *Remove* on one | Badge shows 1 | H |
| TC-C04 | Remove in cart | 1. Add product 2. Open cart 3. Click *Remove* | Product disappears, badge disappears | M |
| TC-C05 | Cart after reload | 1. Add product 2. Reload page | Product is still in the cart | L |
| TC-C06 | Empty cart checkout | 1. Open empty cart 2. Click *Checkout* | Checkout should not be possible with an empty cart | M |

## Checkout

| ID | Title | Steps | Expected result | Prio |
|----|-------|-------|-----------------|------|
| TC-K01 | Complete order | 1. Add product 2. Checkout 3. Enter first name, last name, postal code 4. *Continue* 5. *Finish* | "Thank you for your order!" | H |
| TC-K02 | Missing first name | 1. Leave first name empty, fill the rest 2. *Continue* | "Error: First Name is required" | M |
| TC-K03 | Missing last name | 1. Leave last name empty 2. *Continue* | "Error: Last Name is required" | M |
| TC-K04 | Missing postal code | 1. Leave postal code empty 2. *Continue* | "Error: Postal Code is required" | M |
| TC-K05 | Totals | 1. Add Backpack, Bike Light, Onesie 2. Go to overview | Item total $47.97, tax $3.84, total $51.81 | H |
| TC-K06 | Cancel checkout | 1. Start checkout 2. Click *Cancel* | Back to cart, products still in cart | L |
| TC-K07 | Cart empty after order | 1. Complete order 2. Click *Back Home* | Cart badge is gone | M |

## Exploratory test charters

| ID | Charter | Time box |
|----|---------|----------|
| EX-01 | Explore the shop as `problem_user` to find differences to `standard_user` | 30 min |
| EX-02 | Explore the checkout with unusual input (very long names, special characters, spaces only, letters in postal code) | 20 min |
| EX-03 | Explore the shop as `error_user` and `visual_user` and look for functional and visual defects | 30 min |
| EX-04 | Explore navigation: browser back/forward, direct URLs, reload on every page | 20 min |
