# Test action
This simple action for execution of `npm` tests with color output.

## Input
### `test-name`
**Required** - The name of the test from `package.json`.

## Example usege
```yml
---
name: Test

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout the repo
        uses: actions/checkout@v4
  
      - name: Use Node.js 20.x
        uses: actions/setup-node@v4
        with:
          node-version: 20.x
          cache: "npm"
        
      - name: Install dependencies
        run: npm install
  
      - name: Install Playwright browsers
        run: npx playwright install
  
      - name: Start the application
        run: npm start &
  
      - name: Execute UI tests
        uses: tonytech83/execute-test@v1.1
        with:
          test-name: test:ui
```
