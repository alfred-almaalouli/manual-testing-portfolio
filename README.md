# Manual Testing Portfolio – Sauce Demo

Manual test documentation for the [Sauce Demo](https://www.saucedemo.com) web shop, written the way it is done in a real project: test plan, test cases, executed tests, bug reports and a summary report. The test design follows the ISTQB Foundation Level syllabus.

| Document | Content |
|----------|---------|
| [Test plan](test-plan.md) | scope, approach, test techniques, environment, entry/exit criteria, risks |
| [Test cases](test-cases.md) | 28 test cases (login, products, cart, checkout) + 4 exploratory charters |
| [Bug reports](bug-reports.md) | 11 reproducible defects with steps, expected/actual result, severity and priority |
| [Test summary](test-summary.md) | results, defect overview and release recommendation |

## Highlights

- **Critical defects found:** a customer cannot complete a purchase as `problem_user` (last name field writes into the first name field) and as `error_user` (*Finish* button fails with a JavaScript error).
- **Privacy issue:** after logout, the next user on the same browser sees the previous user's cart.
- **Missing validation:** an order with an empty cart ($0.00) can be completed; names with only spaces are accepted.
- Every bug was reproduced and checked against `standard_user` as a control test.

## Test techniques used

Equivalence partitioning · boundary values · decision table · state transition · use-case testing · exploratory testing with charters

## Related projects

- Automated UI tests for the same shop: [saucedemo-playwright-tests](https://github.com/alfred-almaalouli/saucedemo-playwright-tests) (Python, Playwright)
- [selenium-ui-tests-java](https://github.com/alfred-almaalouli/selenium-ui-tests-java) (Java, Selenium)
- [rest-api-tests-java](https://github.com/alfred-almaalouli/rest-api-tests-java) (Java, REST Assured)

## Author

Alfred Al Maalouli – [GitHub](https://github.com/alfred-almaalouli)
