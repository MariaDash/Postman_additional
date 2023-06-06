# Some additional  Postman/Javascript tests scripts
## Tests  for the response from the server
### 1.Tests for the body:Text
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
1) pm.expect(pm.response.text()).to.equal("string")
2) pm.expect(pm.response.text()).to.deep.equal("string")
3) pm.expect(pm.response.text()).to.be.a("string")
4) pm.expect(pm.response.text()).to.be.an("string")
5) pm.expect(pm.response.text() == "string").to.be.true
6) pm.expect(pm.response.text() === "string").to.be.true
7) pm.expect(pm.response.text() == "string").to.be.ok
8) pm.expect(pm.response.text() === "string").to.be.ok
9) pm.expect(pm.response.text()).to.have.lengthOf(30)
10) pm.expect(pm.response.text()).to.have.lengthOf.above(20)
11) pm.expect(pm.response.text()).to.have.lengthOf.at.least(200)
12) pm.expect(pm.response.text()).to.exist
13) pm.expect(pm.response.text()).to.not.be.empty
14) pm.expect(pm.response.text()).to.match(/^string/)
15) pm.expect(pm.response.text()).to.have.string("string")
