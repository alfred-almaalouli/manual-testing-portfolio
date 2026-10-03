# Test Summary Report – Sauce Demo

**Test period:** 03.10.2026 · **Tester:** Alfred Al Maalouli · **Environment:** https://www.saucedemo.com, Chromium-based desktop browser

## Result for `standard_user` (release candidate)

| Area | Executed | Passed | Failed | Not run |
|------|----------|--------|--------|---------|
| Login | 7 | 7 | 0 | 2 (TC-L06, TC-L09) |
| Products | 4 | 4 | 0 | 2 (TC-P05, TC-P06) |
| Cart | 4 | 3 | 1 (TC-C06 → BUG-06) | 2 (TC-C02, TC-C04) |
| Checkout | 6 | 6 | 0 | 1 (TC-K07) |
| **Total** | **21** | **20** | **1** | **7** |

The main flows (login, products, cart, checkout, totals) are also covered by 24 automated regression tests: [saucedemo-playwright-tests](https://github.com/alfred-almaalouli/saucedemo-playwright-tests).

## Exploratory sessions

| Charter | Findings |
|---------|----------|
| EX-01 problem_user | BUG-01, BUG-03, BUG-04, BUG-07, BUG-08, BUG-10 |
| EX-02 unusual checkout input | BUG-11 |
| EX-03 error_user | BUG-02, BUG-04, BUG-07, BUG-09 |
| EX-04 navigation between users | BUG-05 |

## Defects

11 defects reported: **2 critical, 3 high, 5 medium, 1 low** – details in [bug-reports.md](bug-reports.md).

## Assessment

- `standard_user`: the main purchase flow works. Before release, **BUG-05** (cart visible to the next user) and **BUG-06** (empty order) should be fixed.
- `problem_user` and `error_user`: not releasable – a customer cannot complete a purchase (BUG-01, BUG-02).
- Recommendation: fix the critical and high defects, then re-test and run the automated regression suite.
