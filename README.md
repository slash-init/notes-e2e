# Notes App E2E Tests

E2E tests for the notes app using Playwright. Tests login, note creation, and importance toggling.

## Setup

```bash
npm install
npx playwright install
```

## What I Learned

- Used Playwright for browser automation
- Reset database before each test with `/api/testing/reset` endpoint
- Created helper functions (`loginWith`, `createNote`) to avoid repeating code
- Used `waitFor()` to handle async operations - prevents flaky tests
- Tests run sequentially (`workers: 1`) to avoid database conflicts

## Running Tests

```bash
# All tests
npm test

# With browser visible
npm test -- --headed

# Debug mode (step through)
npm test -- --debug

# Specific test
npm test -- -g "login"

# View report
npm run test:report
```

## Important Notes

- Backend must be running on `localhost:3001` with `NODE_ENV=test`
- Frontend must be running on `localhost:5173`
- Database gets reset before each test via the `/api/testing/reset` endpoint
- Helper functions in `tests/helper.js` use CommonJS (`module.exports`), not ES6 exports
- 401 errors in console during login failure tests are expected - that's what we're testing

## Test Structure

```
tests/
├── helper.js         # loginWith, createNote helpers
└── note_app.spec.js  # actual test specs
```

## Config

- Timeout: 3 seconds per test
- Runs on Chromium, Firefox, and WebKit
- Base URL: `http://localhost:5173`
- Retries on CI: 2, Local: 0
