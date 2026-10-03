# Test Summary Report: SauceDemo E-commerce Web Application

| | |
|---|---|
| **Project** | SauceDemo |
| **Application under test** | https://www.saucedemo.com |
| **Tested by** | [Hisaan Sakhawat] |
| **Execution date** | [3/10/26] |
| **Environment** | Google Chrome [version], [OS] |
| **Related documents** | `test-plan.md`, `SauceDemo_Test_Cases.xlsx`, GitHub Issues |

---

## 1. Overview

52 test cases were executed manually across login, inventory, product details, checkout, logout, and the `problem_user` and `visual_user` accounts. **27 passed and 25 failed (pass rate: 51.9%).** The 25 failures map to **14 distinct defects**.

The core flow works correctly for `standard_user` (login, sorting, cart, total calculation, checkout with valid data, logout). The main weaknesses are **missing input validation on the checkout form** and **multiple functional and visual defects for `problem_user` and `visual_user`**, including one that blocks checkout entirely.

## 2. Execution Summary

| Metric | Count |
|---|---|
| Total test cases | 52 |
| Passed | 27 |
| Failed | 25 |
| Blocked / Not run | 0 |
| Pass rate | 51.9% |
| Distinct defects | 14 |

### By module

| Module | Total | Passed | Failed |
|---|---|---|---|
| Login | 10 | 10 | 0 |
| Inventory | 8 | 8 | 0 |
| Product Details | 1 | 1 | 0 |
| Checkout | 18 | 7 | 11 |
| Logout | 1 | 1 | 0 |
| Problem User | 10 | 0 | 10 |
| Visual User | 4 | 0 | 4 |
| **Total** | **52** | **27** | **25** |

### By account

| Account | Total | Passed | Failed |
|---|---|---|---|
| `standard_user` | 37 | 26 | 11 |
| `problem_user` | 11 | 1 | 10 |
| `visual_user` | 4 | 0 | 4 |

## 3. Defect Summary

Severity and priority below are proposed. Update the IDs to match your GitHub Issue numbers.

| Bug ID | Summary | Account | Severity | Priority | Failed test case(s) |
|---|---|---|---|---|---|
| BUG-01 | Checkout can be started with an empty cart | standard_user | Medium | Medium | TC-CHECKOUT-001 |
| BUG-02 | Name fields accept digits and special characters | standard_user | Low | Low | TC-CHECKOUT-008, 009, 014, 015 |
| BUG-03 | ZIP field accepts letters and special characters | standard_user | Medium | Medium | TC-CHECKOUT-010, 016 |
| BUG-04 | No maximum length on First Name, Last Name and ZIP | standard_user | Low | Low | TC-CHECKOUT-011, 012, 013 |
| BUG-05 | Spaces in checkout fields are not trimmed | standard_user | Low | Low | TC-CHECKOUT-017 (spaces) |
| BUG-06 | Wrong product images shown (same dog image repeated) | problem_user | Medium | Medium | TC-PROB-002 |
| BUG-07 | Product detail page shows a different product than the one clicked | problem_user | High | High | TC-PROB-003 |
| BUG-08 | Add to cart / Remove buttons do not respond for some products | problem_user | High | High | TC-PROB-004, 005 |
| BUG-09 | Sort dropdown has no effect (all four options) | problem_user | Medium | Medium | TC-PROB-006, 007, 008, 009 |
| BUG-10 | Last Name field does not accept input, so checkout cannot proceed | problem_user | Critical | High | TC-PROB-010, 011 |
| BUG-11 | Product images do not match products | visual_user | Medium | Medium | TC-VIS-001 |
| BUG-12 | Cart icon is not placed in the header | visual_user | Low | Low | TC-VIS-002 |
| BUG-13 | Checkout button is placed at the top instead of below the cart items | visual_user | Low | Low | TC-VIS-003 |
| BUG-14 | Menu button is slightly tilted | visual_user | Low | Low | TC-VIS-004 |

### Defects by severity

| Severity | Count |
|---|---|
| Critical | 1 |
| High | 2 |
| Medium | 5 |
| Low | 6 |
| **Total** | **14** |

## 4. Key Findings

1. **Checkout validation is the biggest gap for the standard account.** Every invalid-input test on First Name, Last Name and ZIP (digits, letters, symbols, very long values) was accepted, and spaces were not trimmed. In a real store this would allow bad data into orders.
2. **An empty cart can proceed to checkout.** This lets a user reach the payment steps with nothing to buy.
3. **`problem_user` cannot complete a purchase.** The Last Name field rejects input, buttons are unresponsive, and the detail page shows the wrong product. These are the most severe defects found.
4. **`visual_user` shows layout and image issues** that affect trust and usability but do not block any flow.
5. **No defects were found** in login handling, sorting and cart for `standard_user`, the checkout total calculation, or logout.

## 5. Test Coverage and Limitations

- Not covered in this cycle: `locked_out_user`, `error_user`, `performance_glitch_user`, security testing, cross-browser and mobile testing, cart persistence across pages, and reset app state.
- Expected results are based on common e-commerce practice because no requirements document exists. Some behaviors may be intentional on a demo site.
- All testing was done manually in a single browser.

## 6. Risks

- Without checkout validation, invalid customer data could reach order processing.
- Accounts that hit the `problem_user` defects would be unable to buy, meaning direct revenue loss.
- Untested areas (security, other browsers, mobile) may hide further defects.

## 7. Conclusion and Recommendation

**The application is not ready for release.** The `standard_user` journey works, but the checkout validation gaps (BUG-02 to BUG-05), the empty-cart checkout (BUG-01) and the blocking and high-severity defects for `problem_user` (BUG-07, BUG-08, BUG-10) should be fixed and retested before release.

**Recommended next steps:** fix BUG-10, BUG-07 and BUG-08 first, add validation to the checkout form, then run a regression pass on all failed test cases and extend coverage to the untested accounts and browsers.

## 8. Sign-off

| Role | Name | Date |
|---|---|---|
| Tester | [Hisaan Sakhawat] | [3/10/26] |
