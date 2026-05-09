# 📞 Telemarketing Automation Test

![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Selenium](https://img.shields.io/badge/Selenium_4.0.0-43B02A?style=flat-square&logo=selenium&logoColor=white)
![TestNG](https://img.shields.io/badge/TestNG_7.6.0-FF7300?style=flat-square&logo=testng&logoColor=white)
![Cucumber](https://img.shields.io/badge/Cucumber_7.3.4-23D96C?style=flat-square&logo=cucumber&logoColor=white)
![Maven](https://img.shields.io/badge/Maven-C71A36?style=flat-square&logo=apachemaven&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green.svg)

End-to-end automation testing suite for a complex enterprise telemarketing system, covering SPV workflows including task creation, follow-up scheduling, agreement capture, and bulk data management.

---

## 📑 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Getting Started](#-getting-started)
- [Test Scenarios](#-test-scenarios)
- [Design Patterns](#-design-patterns)
- [Reports](#-reports)
- [CI/CD](#-cicd)
- [Author](#-author)

---

## ✨ Features

- **Comprehensive SPV Workflow Coverage** — Automates the full telemarketing supervisor lifecycle from login through task completion
- **Multi-Module Test Architecture** — Organized test classes spanning login, new tasks, follow-ups, agreements, finals, and bulk data operations
- **Agent-Specific Test Isolation** — Dedicated subdirectory for agent-level test scenarios separated from SPV tests
- **Page Object Model (POM)** — Large-scale page object implementation with granular page abstractions for complex UI forms
- **TestNG Suite Management** — XML-driven suite configuration for selective and parallel test execution
- **HTML Reporting** — Auto-generated HTML reports for each test module with detailed pass/fail breakdowns
- **Reusable Utility Layer** — Centralized utility class for common actions, waits, and data handling across all page objects

---

## 🛠 Tech Stack

| Technology | Version | Purpose |
|:-----------|:--------|:--------|
| Java | 11+ | Core programming language |
| Selenium WebDriver | 4.0.0 | Browser automation engine |
| TestNG | 7.6.0 | Test framework & suite orchestration |
| Cucumber | 7.3.4 | BDD layer for readable test definitions |
| Maven | 3.8+ | Build automation & dependency management |

---

## 📁 Project Structure

```
telemarketing-automation-test/
├── pom.xml
├── src/
│   ├── main/java/
│   │   └── pages/
│   │       ├── LoginPage.java
│   │       ├── MainPage.java
│   │       ├── TaskAgreePage.java            # 4.9 KB — agreement capture forms
│   │       ├── TaskDataAllPage.java          # 21.9 KB — bulk data grid operations
│   │       ├── TaskFinalPage.java
│   │       ├── TaskFollowUpPage.java         # 18.9 KB — follow-up scheduling & comms
│   │       ├── TaskNewPage.java              # 19.3 KB — new task creation workflows
│   │       └── Utility.java
│   └── test/java/
│       ├── tests/
│       │   ├── TLMKT_TestLogin.java          # 8.5 KB
│       │   ├── TLMKT_TestTaskNew.java        # 30 KB
│       │   ├── TLMKT_TestTaskFollowUp.java   # 30.5 KB
│       │   ├── TLMKT_TestTaskAgree.java      # 9.9 KB
│       │   ├── TLMKT_TestTaskFinal.java      # 4.5 KB
│       │   └── TLMKT_TestDataAll.java        # 37.8 KB
│       └── agent/
│           └── ...                           # Agent-specific test classes
├── TaskSPVsuite.xml
├── reports/
│   ├── TELEMARKET-SPV-Login.html
│   └── TELEMARKET-SPV-TaskFinal.html
└── README.md
```

---

## 📋 Prerequisites

- **Java JDK** 11 or higher
- **Apache Maven** 3.8+
- **Chrome / Firefox** browser installed
- **ChromeDriver / GeckoDriver** matching your browser version
- Access credentials to the telemarketing application environment

---

## 🚀 Getting Started

### Installation

```bash
# Clone the repository
git clone https://github.com/ridhotadjudin/telemarketing-automation-test.git
cd telemarketing-automation-test

# Install dependencies
mvn clean install -DskipTests
```

### Running Tests

```bash
# Run the full SPV test suite
mvn test -DsuiteXmlFile=TaskSPVsuite.xml

# Run a specific test class
mvn test -Dtest=TLMKT_TestTaskNew

# Run with a specific browser
mvn test -DsuiteXmlFile=TaskSPVsuite.xml -Dbrowser=chrome
```

---

## 🧪 Test Scenarios

| Scenario Name | Type | Description |
|:--------------|:-----|:------------|
| SPV Login | Functional | Validates supervisor login with valid/invalid credentials and session handling |
| New Task — Creation | Functional | Verifies creation of new telemarketing tasks with required field validations |
| New Task — Assignment | Functional | Tests task assignment to agents with correct role and priority propagation |
| New Task — Priority Setting | Functional | Ensures priority levels are correctly applied and reflected in task queues |
| Follow-Up — Scheduling | Functional | Validates scheduling of follow-up calls with date/time constraints |
| Follow-Up — Communication Log | Functional | Confirms communication history is recorded accurately per customer interaction |
| Agreement — Capture | Functional | Tests capturing customer agreement details including terms and conditions acceptance |
| Agreement — Document Attachment | Functional | Validates document upload and association with the correct agreement record |
| Task Final — Completion | End-to-End | Verifies full task lifecycle completion with status transitions and audit trail |
| Bulk Data — Management | Data-Driven | Tests bulk data operations including filtering, sorting, pagination, and export across large datasets |
| Bulk Data — Search & Filter | Data-Driven | Validates complex multi-criteria search and filter combinations on the data grid |
| Agent — Task Handling | Functional | Agent-specific tests for task pickup, processing, and status updates |

---

## 🏗 Design Patterns

### Page Object Model (POM)

Every page in the telemarketing application is represented by a dedicated Java class under `pages/`. Each page object encapsulates element locators and interaction methods, ensuring that UI changes require updates in only one place. The large page objects (`TaskDataAllPage` at 21.9 KB, `TaskNewPage` at 19.3 KB, `TaskFollowUpPage` at 18.9 KB) reflect the complexity of enterprise forms with dozens of fields, dropdowns, and conditional logic.

### Data-Driven Testing

Test data is externalized and injected via TestNG data providers and Cucumber examples, enabling the same test logic to execute across multiple input combinations without code duplication.

### Suite-Based Execution

The `TaskSPVsuite.xml` configuration groups tests by functional area, enabling selective execution of login, task, follow-up, or agreement modules independently or as a full regression suite.

### Utility Abstraction

The `Utility.java` class centralizes reusable operations such as explicit waits, screenshot capture, element visibility checks, and date formatting — reducing boilerplate across all page objects and test classes.

---

## 📊 Reports

HTML test reports are generated automatically after each test run:

| Report | Description |
|:-------|:------------|
| `TELEMARKET-SPV-Login.html` | Login module test results with pass/fail details |
| `TELEMARKET-SPV-TaskFinal.html` | Task finalization test results with execution timestamps |

Reports are located in the `reports/` directory and can be opened directly in any browser.

---

## ⚙️ CI/CD

This project is designed to integrate with CI/CD pipelines:

- **Maven Surefire Plugin** for test execution within build pipelines
- **TestNG XML suites** for selective module execution in different pipeline stages
- **HTML reports** generated as pipeline artifacts for post-build review
- Compatible with **Jenkins**, **GitHub Actions**, and **GitLab CI** runners

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Ridho Tadjudin**

- 🌐 Website: [ridhotadjudin.id](https://ridhotadjudin.id)
- 💻 GitHub: [@ridhotadjudin](https://github.com/ridhotadjudin)
