# Some additional  Postman/Javascript tests scripts
## Tests  for the response from the server
### 1.Tests for the body: Text
#### 1.1. From Postman snippets
1) `to.have.body ===` test whole string
```pm.test("Body is correct", function () {
     pm.response.to.have.body("response_body_string");
 });
```
Note1: everytime break your test to test them.
Note2:`\n` - shielding line break
2) `to.include ==` test partially
```
 pm.test("Body matches string", function () {
     pm.expect(pm.response.text()).to.include("string_you_want_to_search");
 });
``` 
#### 1.2. From  Sandbox API reference  
1) `pm.response.to.have.body()` - test that response have a body
#### 1.3. From Chai.js
1) `pm.expect(pm.response.text()).to.equal("string")`  === ( not child objects)
2) `pm.expect(pm.response.text()).to.deep.equal("string")`  (equivalent to eql) === (with child objects)
3) `pm.expect(pm.response.text()).to.be.a("string")`   - this is a string, not number
4) `pm.expect(pm.response.text()).to.be.an("string")`  - this is a string, not number
5) `pm.expect(pm.response.text() == "string").to.be.true`  - boolean
6) `pm.expect(pm.response.text() === "string").to.be.true`   - strict boolean
7) `pm.expect(pm.response.text() == "string").to.be.ok`   - boolean
8) `pm.expect(pm.response.text() === "string").to.be.ok`   - strict boolean
9) `pm.expect(pm.response.text()).to.have.lengthOf(30)`   - test length
10) `pm.expect(pm.response.text()).to.have.lengthOf.above(20)`  - test that length is more than mentioned
11) `pm.expect(pm.response.text()).to.have.lengthOf.at.least(200)` - test that length is more or equal than mentioned
12) `pm.expect(pm.response.text()).to.have.lengthOf.at.most(200)` - test that length is less or equal than mentioned
13) `pm.expect(pm.response.text()).to.exist` - test that the text exists
14) `pm.expect(pm.response.text()).to.not.be.empty`  - test that the text is not empty
15) `pm.expect(pm.response.text()).to.match(/^string/)`  test matching with use of regexp
16) `pm.expect(pm.response.text()).to.have.string("string")` === test we have string
#### 1.4. From Node.js
1) `const assert = require("assert");`   - downloading assertion library

```
pm.test("assert", function () {
     assert.ok.(pm.response.text() == "string_you_want_to_search");
 });
```
2)
```
pm.test("assert", function () {
     assert(pm.response.text() === "string_you_want_to_search");
 })
```
3)
```
pm.test("assert", function () {
     assert.deepEqual(pm.response.text(),"string_you_want_to_search");
 })
```
4)
```
pm.test("assert", function () {
     assert.deepStrictEqual(pm.response.text(),"string_you_want_to_search");
 })
```
5)
```
pm.test("assert", function () {
     assert.equal(pm.response.text(),"string_you_want_to_search");
 })
```
6)
```
pm.test("assert", function () {
     assert.strictEqual(pm.response.text(),"string_you_want_to_search");
 })
```
### 2. Tests for the body: JSON
#### 2.1. From Postman snippets

