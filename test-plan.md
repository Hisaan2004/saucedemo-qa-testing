# Test Plan: SauceDemo E-commerce Web Application

| | |
|---|---|
| **Project** | SauceDemo QA (personal portfolio project) |
| **Application under test** | https://www.saucedemo.com |
| **Prepared by** | [Your Name] |
| **Version / Date** | 1.0 / [date of execution] |
| **Test type** | Manual, functional and UI testing |

---

## 1. Objective

Verify that the core customer journey on SauceDemo (login, browsing and sorting products, managing the cart, checkout, logout) works as expected, that the checkout form handles invalid input correctly, and that the application behaves correctly for the built-in test accounts (`standard_user`, `problem_user`, `visual_user`). Defects found are documented with severity and priority.

## 2. Scope

### In scope
| Module | What is covered |
|---|---|
| Login | Valid and invalid credentials, empty fields, spaces, case sensitivity |
| Inventory | Sorting (name A-Z / Z-A, price low-high / high-low), add/remove from cart, multiple items, product detail page |
| Cart and Checkout | Empty-cart checkout, single and multiple product checkout, total calculation, field validation (empty, numeric, alphabetic, special characters, length, spaces), order confirmation |
| Logout | Logout from the side menu |
| User-specific behavior | `problem_user` (functional defects) and `visual_user` (layout and image defects) |

### Out of scope (this cycle)
- Performance testing (`performance_glitch_user`)
- `locked_out_user` and `error_user` accounts
- Security testing (SQL injection, XSS, session handling)
- Cross-browser and mobile testing
- Automation (planned as a separate project)

## 3. Test Approach

| Approach | How it is applied |
|---|---|
| Functional testing | Each feature is checked against its expected behavior |
| Negative testing | Invalid, empty and malformed input on login and checkout forms |
| Boundary value analysis | Very long values in name and ZIP fields |
| Equivalence partitioning | Input grouped into valid / invalid classes (letters, digits, special characters, spaces) |
| UI / visual testing | Element placement, images and alignment for `visual_user` |
| Exploratory testing | Initial walkthrough of the app before writing test cases |

Test cases are written in a spreadsheet (`SauceDemo_Test_Cases.xlsx`) with the columns: Test Case ID, Module, Title, Preconditions, Steps, Test Data, Expected Result, Actual Result, Status.

## 4. Test Environment

| Item | Detail |
|---|---|
| Application URL | https://www.saucedemo.com |
| Browser | Google Chrome [version] |
| Operating system | [Windows / macOS / Linux, version] |
| Tools | Google Sheets / Excel (test cases), GitHub Issues (defects), Chrome DevTools, screenshot tool |

## 5. Test Data

| Account | Username | Password | Purpose |
|---|---|---|---|
| Standard | `standard_user` | `secret_sauce` | Baseline behavior |
| Problem | `problem_user` | `secret_sauce` | Functional defects (images, buttons, sorting, forms) |
| Visual | `visual_user` | `secret_sauce` | Layout and image defects |

Checkout test data includes valid values (e.g. First Name: Smith, Last Name: Charles, ZIP: 54000) and invalid values (digits in names, letters or symbols in ZIP, 20+ character strings, spaces).

## 6. Entry and Exit Criteria

**Entry criteria**
- Application is reachable and the login page loads
- Test accounts and credentials are available
- Test cases are written and reviewed

**Exit criteria**
- All planned test cases are executed
- All failures are logged as defects with steps to reproduce and evidence
- A test summary report is produced

## 7. Defect Management

Defects are logged in GitHub Issues with: title, steps to reproduce, expected vs actual result, environment, severity, priority and a screenshot.

| Severity | Definition |
|---|---|
| Critical | Blocks a core flow (e.g. user cannot complete a purchase) |
| High | Major feature broken, workaround difficult |
| Medium | Feature partly broken or incorrect data/validation, workaround exists |
| Low | Cosmetic or minor UI issue |

Priority (High / Medium / Low) reflects how soon the fix is needed from a business point of view.

## 8. Deliverables

- Test Plan (this document)
- Test Cases (`SauceDemo_Test_Cases.xlsx`)
- Defect reports (GitHub Issues)
- Test Summary Report (`test-summary-report.md`)

## 9. Assumptions and Risks

- There is no requirements document for SauceDemo, so expected results are based on common e-commerce behavior and standard form-validation practice.
- SauceDemo is a demo site, so some behaviors (e.g. lax checkout validation) may be intentional. They are still reported because they would be defects in a real product.
- Results are from one browser and one OS, so findings may differ elsewhere.
- Coverage is limited to the modules listed in scope.
