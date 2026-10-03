# Bug Reports – Sauce Demo

Found during test execution on **03.10.2026**. Environment for all reports: https://www.saucedemo.com, Chromium-based browser (desktop), password `secret_sauce`.

**Severity** = impact on the user. **Priority** = how soon it should be fixed.

| ID | Title | User | Severity | Priority |
|----|-------|------|----------|----------|
| BUG-01 | Last name cannot be entered – typing overwrites the first name, checkout blocked | problem_user | Critical | High |
| BUG-02 | *Finish* does not complete the order | error_user | Critical | High |
| BUG-03 | Product name opens the detail page of a different product | problem_user | High | High |
| BUG-04 | *Add to cart* does nothing for 3 of 6 products | problem_user, error_user | High | High |
| BUG-05 | Cart of the previous user is shown to the next user | standard_user | High | Medium |
| BUG-06 | Order with an empty cart can be completed ($0.00) | standard_user | Medium | Medium |
| BUG-07 | *Remove* does not remove products from the cart | problem_user, error_user | Medium | High |
| BUG-08 | Sorting has no effect | problem_user | Medium | Medium |
| BUG-09 | Last name cannot be entered, but checkout continues without it | error_user | Medium | Medium |
| BUG-10 | All products show the same placeholder image | problem_user | Medium | Medium |
| BUG-11 | Checkout accepts names with only spaces and a postal code with letters | standard_user | Low | Low |

---

## BUG-01 – Last name cannot be entered, checkout blocked

**User:** problem_user · **Severity:** Critical · **Priority:** High

**Steps to reproduce**
1. Log in as `problem_user`
2. Add any product to the cart, open the cart, click *Checkout*
3. Type "Alfred" in *First Name*
4. Type "Tester" in *Last Name*
5. Type "45143" in *Postal Code* and click *Continue*

**Expected result:** First Name = "Alfred", Last Name = "Tester", the overview page opens.

**Actual result:** The text typed in *Last Name* appears in *First Name* (First Name = "Tester"), *Last Name* stays empty. After *Continue* the error "Error: Last Name is required" is shown. The order cannot be completed.

**Note:** works correctly for `standard_user` (control test).

---

## BUG-02 – *Finish* does not complete the order

**User:** error_user · **Severity:** Critical · **Priority:** High

**Steps to reproduce**
1. Log in as `error_user`
2. Add *Sauce Labs Backpack* to the cart and go to checkout
3. Fill in the form, click *Continue*
4. On the overview page click *Finish*

**Expected result:** "Thank you for your order!" page.

**Actual result:** Nothing happens, the user stays on the overview page. Browser console: `Uncaught TypeError: ... is not a function` in the click handler of the button.

---

## BUG-03 – Product name opens a different product

**User:** problem_user · **Severity:** High · **Priority:** High

**Steps to reproduce**
1. Log in as `problem_user`
2. Click the product name *Sauce Labs Backpack*

**Expected result:** Detail page of *Sauce Labs Backpack*.

**Actual result:** Detail page of *Sauce Labs Fleece Jacket* is opened (`inventory-item.html?id=5`). The customer may buy the wrong product.

---

## BUG-04 – *Add to cart* does nothing for 3 of 6 products

**User:** problem_user (same behaviour for error_user) · **Severity:** High · **Priority:** High

**Steps to reproduce**
1. Log in as `problem_user`
2. Click *Add to cart* on every product, from top to bottom

**Expected result:** Cart badge counts up to 6.

**Actual result:** The badge only counts *Backpack*, *Bike Light* and *Onesie* (badge = 3). Clicks on *Bolt T-Shirt*, *Fleece Jacket* and *Test.allTheThings() T-Shirt (Red)* have no effect.

---

## BUG-05 – Cart of the previous user is shown to the next user

**User:** standard_user · **Severity:** High · **Priority:** Medium

**Steps to reproduce**
1. Log in as `problem_user`, add 3 products to the cart
2. Log out via the menu
3. Log in as `standard_user` on the same browser
4. Open the cart

**Expected result:** Cart of `standard_user` is empty – every user only sees their own cart.

**Actual result:** The cart shows the 3 products of the previous user (badge = 3).

**Impact:** On a shared computer one customer can see (and order) what another customer selected – a privacy problem. The cart seems to be stored per browser, not per user.

---

## BUG-06 – Order with an empty cart can be completed

**User:** standard_user · **Severity:** Medium · **Priority:** Medium

**Steps to reproduce**
1. Log in as `standard_user`, make sure the cart is empty
2. Open the cart and click *Checkout*
3. Fill in the form, click *Continue*, then *Finish*

**Expected result:** *Checkout* is disabled for an empty cart, or a message "Your cart is empty" is shown.

**Actual result:** Overview shows "Total: $0.00" and the order is confirmed with "Thank you for your order!".

---

## BUG-07 – *Remove* does not remove products

**User:** problem_user (same for error_user) · **Severity:** Medium · **Priority:** High

**Steps to reproduce**
1. Log in as `error_user`
2. Add *Backpack*, *Bike Light* and *Onesie* (badge = 3)
3. Click *Remove* on each of them on the product list

**Expected result:** Badge goes 2 → 1 → disappears.

**Actual result:** Badge stays at 3. For `problem_user` the same happens with *Remove* on *Sauce Labs Backpack*.

---

## BUG-08 – Sorting has no effect

**User:** problem_user · **Severity:** Medium · **Priority:** Medium

**Steps to reproduce**
1. Log in as `problem_user`
2. Select "Name (Z to A)" in the sort dropdown

**Expected result:** *Test.allTheThings() T-Shirt (Red)* is first, list is sorted Z → A.

**Actual result:** The order does not change and the dropdown jumps back to "Name (A to Z)". Works for `standard_user`.

---

## BUG-09 – Last name cannot be entered, but checkout continues without it

**User:** error_user · **Severity:** Medium · **Priority:** Medium

**Steps to reproduce**
1. Log in as `error_user`, add a product, start checkout
2. Type "Alfred", "Tester", "45143" in the three fields
3. Click *Continue*

**Expected result:** All three fields are filled; if one is empty, a "required" error is shown.

**Actual result:** *Last Name* stays empty (console: `Uncaught TypeError: Cannot read properties of undefined (reading 'value')`), but the overview page opens anyway – the required-field check is skipped.

---

## BUG-10 – All products show the same image

**User:** problem_user · **Severity:** Medium · **Priority:** Medium

**Steps to reproduce**
1. Log in as `problem_user`
2. Look at the product images

**Expected result:** Each product shows its own picture (6 different images, as for `standard_user`).

**Actual result:** All 6 products show the same placeholder image (`sl-404...jpg`, a dog photo).

---

## BUG-11 – Checkout accepts invalid customer data

**User:** standard_user · **Severity:** Low · **Priority:** Low

**Steps to reproduce**
1. Log in as `standard_user`, add a product, start checkout
2. Enter three spaces as *First Name* and *Last Name*, "abc" as *Postal Code*
3. Click *Continue*

**Expected result:** Error messages – names must contain letters, the postal code must have a valid format.

**Actual result:** The overview page opens; the data is accepted.
