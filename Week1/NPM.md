# NPM
## Setup
1. In the root of the project, run:
```
npm init
```
**package.json** will be created.

2. In the **.gitignore** file, add the line:
```
node_modules
```
3. Install the dependencies, e.g.:
```
npm install --save mocha chai husky eslint
```
If there are already dependencies listed in **package.json**, simply run `npm install`.

---
## Testing
4. With Mocha and Chai installed for testing, create a folder named `spec` in the root of the project.

5. In **package.json**, add:
```
"scripts": {
  "test": "mocha ./spec/*.spec.js"
}
```
6. In the test files you create in `spec`, add this line at the top:
```javascript
const expect = require('chai').expect;
```
7. At the bottom of your script files, add this line at the bottom:
```javascript
module.exports = myFunction;
```
For example:
#### /myModule.js
```javascript
function myFunction () { ... }

module.exports = myFunction;
```
#### /spec/myModule.spec.js
```javascript
const expect = require('chai').expect;
const myFunction = require('../myModule');

describe('myFunction', function () {
  it('is a function', function () {
    expect(myFunction).to.be.a('function');
  });
});
```
8. In **package.json**, add a precommit hook:
```
"scripts": {
  "test": "mocha ./spec/*.spec.js",
  "precommit": "npm test"
}
```

---
## Linting
9. With ESLint installed for linting, create `.eslintrc` in the root of your project. Paste the following into it:
```
{
  "extends": ["eslint:recommended"],
  "env": {
    "node": true,
    "mocha": true,
    "es6": true
  },
    "parserOptions": {
    "ecmaVersion": 6,
    "sourceType": "module"
  },
  "rules": {
    "no-console": 0,
    "space-before-blocks": 1,
    "arrow-spacing": 1,
    "keyword-spacing": 1,
    "space-infix-ops": 1,
    "space-in-parens": 1,
    "spaced-comment": 1,
    "semi": 1,
    "quotes": ["error", "single"],
    "no-multiple-empty-lines": 1
  }
}
```
10. Add a linting script in **package.json**:
```
"scripts": {
  "test": "mocha ./spec/*.spec.js",
  "precommit": "npm test",
  "lint": "eslint --fix ./"
}
```
11. Create `.eslintignore` in the root of your project and paste `node_modules/*` into it.

12. Add posttest and lint scripts to **package.json**:
```
"scripts": {
    "test": "mocha ./spec/*.spec.js",
    "test.watch": "npm test -- --watch",
    "posttest": "npm run lint",
    "precommit": "npm test",
    "lint": "eslint --fix ./"
}
```
