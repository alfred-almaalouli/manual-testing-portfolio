# Test Plan – Sauce Demo Web Shop

| | |
|---|---|
| **Application** | Sauce Demo (Swag Labs) – https://www.saucedemo.com |
| **Version / date** | public demo, October 2026 |
| **Author** | Alfred Al Maalouli |
| **Test level** | System test (black box) |

## 1. Objective

Check that a customer can log in, find products, manage the cart and complete an order, and find defects before release. The demo provides special user accounts that simulate faulty versions of the shop; these are used to find and report real defects.

## 2. Scope

**In scope**

- Login and logout
- Product list: names, prices, images, sorting
- Product detail page
- Shopping cart: add, remove, cart badge
- Checkout: customer information, overview, totals, order confirmation
- Error messages and form validation

**Out of scope**

- Payment providers and real orders (the demo has no backend)
- Performance and load testing (only obvious slowness is reported)
- Security testing beyond basic access control
- Mobile apps

## 3. Test approach

| Technique | Where it is used |
|-----------|------------------|
| Equivalence partitioning | valid / invalid / locked user accounts, valid and empty form fields |
| Boundary values | cart with 0, 1 and 6 products |
| Decision table | required fields in the checkout form |
| State transition | cart state across pages and after reload |
| Use-case / end-to-end | complete order from login to confirmation |
| Exploratory testing | time-boxed sessions with charters (see test-cases.md) |

Regression tests for the main flows are automated in a separate project: [saucedemo-playwright-tests](https://github.com/alfred-almaalouli/saucedemo-playwright-tests).

## 4. Test environment

- Browser: Google Chrome (latest), desktop 1366×768
- Test accounts: `standard_user`, `locked_out_user`, `problem_user`, `performance_glitch_user`, `error_user`, `visual_user` (password `secret_sauce`)

## 5. Entry and exit criteria

**Entry:** application reachable, test accounts work, test cases reviewed.

**Exit:**

- all high-priority test cases executed
- no open defects with severity *Critical* or *High* for `standard_user`
- all defects documented in the bug report format

## 6. Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Demo site changes without notice | test cases outdated | check selectors and texts before each run |
| No real backend | totals and orders cannot be checked in a database | check calculations on the overview page |
| Cart is stored in the browser | results depend on browser state | start each test in a clean session |

## 7. Deliverables

- [Test cases](test-cases.md)
- [Bug reports](bug-reports.md)
- [Test summary report](test-summary.md)
