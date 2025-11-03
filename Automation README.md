# EnrichMinion QA Assignment

This repository contains manual and automated QA artifacts for the [Enrich Minion](https://enrichminion.vercel.app/enrichment/phone-finder) application. It includes UI and API test cases, a bug report, and Playwright-based automation scripts.

---

##  Folder Structure

automation/
├── pages/
│   ├── RegisterPage.js          # Page Object for registration
│   └── LoginPage.js             # Page Object for login
├── tests/
│   ├── register.test.js         # Test script for registration flow
│   └── login.test.js            # Test script for login flow
├── playwright.config.js         # Playwright configuration file
├── package.json                 # Project dependencies and scripts
├── .gitignore                   # Files/folders to exclude from Git
└── README.md                    # Instructions for automation setup
Absolutely, Mounika! Here's a clean summary of just the **`automation/` folder structure** and **how to run your Playwright tests**:

---

##  `automation/` Folder Structure

```
automation/
├── pages/
│   ├── RegisterPage.js          # Page Object for registration
│   └── LoginPage.js             # Page Object for login
├── tests/
│   ├── register.test.js         # Test script for registration flow
│   └── login.test.js            # Test script for login flow
├── playwright.config.js         # Playwright configuration file
├── package.json                 # Project dependencies and scripts
├── .gitignore                   # Files/folders to exclude from Git
└── README.md                    # Instructions for automation setup
```

---

##  How to Run the Automation

### 1. **Install Dependencies**

```bash
npm install
```

### 2. **Run All Tests**

```bash
npx playwright test
```

### 3. **Run a Specific Test**

```bash
npx playwright test tests/login.test.js
```

### 4. **View HTML Report**

```bash
npx playwright show-report
```
Attaching the code in zip file 
