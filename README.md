# Assignment 6 - UI Testing with Playwright

## GitHub Repository
**Repository Link:** https://github.com/ALGeek01/SE333_Assignment_6.git

**Note:** The GitHub Actions workflow is configured to automatically run all tests when code is pushed. All tests must pass for successful submission.

## Overview
This project implements automated UI testing for the DePaul University Bookstore website using Playwright. The project demonstrates two different approaches to writing UI tests: traditional manual test coding and AI-assisted test generation.

## Project Structure
```
├── src/test/java/
│   ├── playwrightTraditional/     # Manually written tests
│   └── playwrightLLM/             # AI-assisted tests
├── .github/workflows/             # GitHub Actions configuration
├── pom.xml                        # Maven dependencies
└── videos/                        # Test execution recordings
```

## Setup Instructions

### Prerequisites
- Java 1.8 or higher
- Maven 3.8.5 or higher
- macOS or Windows 10

### Installation

1. Clone the repository and navigate to the project directory

2. Install project dependencies:
```bash
mvn clean install
```

3. Install Playwright browsers:
```bash
mvn exec:java -e -D exec.mainClass=com.microsoft.playwright.CLI -D exec.args="install --with-deps"
```

## Running Tests

Execute all tests:
```bash
mvn test
```

Run traditional tests only:
```bash
mvn test -Dtest=playwrightTraditional.DePaulBookstoreTest
```

Run AI-assisted tests only:
```bash
mvn test -Dtest=playwrightLLM.DePaulBookstoreAITest
```

## Test Scenarios

Both test suites cover the following purchase workflow:

1. Search for "earbuds" in the bookstore
2. Apply filters (JBL brand, Black color, Over $50 price)
3. Select the JBL Quantum True Wireless product
4. Verify product details and add to cart
5. Proceed through checkout as a guest
6. Enter contact and pickup information
7. Review payment details
8. Remove item from cart

## Reflection: Manual vs AI-Assisted Testing

### Traditional Manual Testing

Writing the traditional test suite required significant time and effort. Each test case was carefully constructed by hand, selecting appropriate locators, adding wait conditions, and writing explicit assertions. This approach took several hours to complete.

The main advantage of manual testing was having complete control over every aspect of the test. I could decide exactly which elements to target, how long to wait for dynamic content, and what assertions to make. When something didn't work, it was straightforward to debug because I understood every line of code.

However, the manual approach was quite tedious. Much of the code was repetitive - clicking buttons, filling forms, and waiting for pages to load followed similar patterns throughout. Writing over 400 lines of test code by hand felt inefficient, especially for straightforward user interactions.

Maintenance could be challenging with this approach. If the website structure changes, I would need to manually update locators throughout multiple test methods. The code is also verbose, making it harder to quickly understand the test flow at a glance.

### AI-Assisted Testing  

Using natural language prompts to generate tests was remarkably faster. Describing the test scenario in plain English and having working code generated in minutes was impressive. What took hours manually was accomplished in a fraction of the time.

The generated code was often cleaner and more modular than what I initially wrote. The AI structured tests with reusable helper methods, reducing duplication. This made the code easier to read and understand.

However, the AI approach had drawbacks. The generated code sometimes made assumptions about page structure that needed verification. Some locators were too specific and would break easily with minor UI changes. I also had to review the code carefully to ensure it actually tested what I intended.

There were also cases where the AI-generated tests lacked comprehensive error handling or missed edge cases that I would have considered when writing manually. The code worked for the happy path but needed manual refinement for robustness.

### Comparison

**Speed:** AI-assisted testing wins decisively here. Initial test creation was 5-10 times faster than manual coding.

**Accuracy:** Manual testing provided more confidence in correctness. Every assertion was intentional. AI-generated tests required careful review to verify they tested the right things.

**Maintenance:** This is more nuanced. AI can quickly regenerate tests when requirements change, but understanding what needs to change is harder with generated code. Manual tests are explicit about what they're testing, making updates more straightforward despite being more time-consuming.

**Code Quality:** AI-generated code was surprisingly clean and modular. However, manual code gave me more confidence in handling edge cases and errors appropriately.

### Practical Takeaway

Neither approach is strictly better. For this project, a hybrid approach would have been most effective - use AI to generate the initial test structure and boilerplate, then manually refine assertions, error handling, and edge cases.

AI-assisted testing is excellent for rapid prototyping and creating baseline test coverage quickly. Manual testing remains essential for complex scenarios, detailed assertions, and ensuring tests truly validate what matters.

Going forward, I would use AI generation as a starting point but always review and enhance the generated code. The time savings from AI are substantial, but human judgment is still necessary to ensure test quality and reliability.

## GitHub Actions

The project includes automated CI/CD through GitHub Actions. On every push, the workflow:
- Sets up the Java environment
- Installs Maven dependencies  
- Installs Playwright browsers
- Runs all test suites
- Uploads test videos and reports as artifacts

All tests must execute successfully and the project must compile without errors.

## Important Notes

- Tests interact with the live DePaul bookstore website
- Test execution videos are recorded automatically and saved in the `videos/` directory
- Browser cache is cleared between test runs to ensure consistent results
- Tests are configured to run in visible browser mode for demonstration purposes

## Compilation Requirement

**Critical:** The project must compile successfully. Compilation failure results in automatic assignment failure. Before submission, verify the project builds:

```bash
mvn clean compile
mvn test
```

Both commands must complete without errors.
