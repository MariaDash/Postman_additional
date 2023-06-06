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
1) `pm.expect(pm.response.text()).to.equal("string")`  === ( not child objects, test a value (property, number, string), not useful for objects, arrays)
Note: `equal` is equivalent to `equals`
2) `pm.expect(pm.response.text()).to.deep.equal("string")`  (equivalent to `eql` and to `eqls`) === (can test full structure: child objects)
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
Note: not strict
2)
```
pm.test("assert", function () {
     assert(pm.response.text() === "string_you_want_to_search");
 })
```
Note:  strict
3)
```
pm.test("assert", function () {
     assert.deepEqual(pm.response.text(),"string_you_want_to_search");
 })
```
Note: not strict, use in child objects
4)
```
pm.test("assert", function () {
     assert.deepStrictEqual(pm.response.text(),"string_you_want_to_search");
 })
```
Note: strict, use in child objects
5)
```
pm.test("assert", function () {
     assert.equal(pm.response.text(),"string_you_want_to_search");
 })
```
Note: not strict, not use in child objects
6)
```
pm.test("assert", function () {
     assert.strictEqual(pm.response.text(),"string_you_want_to_search");
 })
```
Note: strict, not use in child objects
### 2. Tests for the body: JSON
#### 2.1. From Postman snippets
1)
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.value).to.eql(100);
});
```
or `to.eql("string")`
2)
```
pm.test("Body is correct", function () {
     pm.response.to.have.body("response_body_string");
 });
```
or
```
pm.test("Body is correct", function () {
     pm.response.to.have.body({response_body_object});
 });
```
3)
```
pm.test("Body matches string", function () {
     pm.expect(pm.response.text()).to.include("string_you_want_to_search");
 });
```
#### 2.2. From  Sandbox API reference  
1) `pm.response.to.have.jsonbody({jsonobject})` - test that response have a json body
2) `pm.response.to.not.have.jsonbody({jsonobject})` - test that response not have a json body
#### 2.3. From Chai.js
##### 1)`eql,deep.equal,equal`(see response.text)
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.).to.eql({
     key: "value";
     key:"value"});
});
```
##### 2) `include, deep.include`
include tests that a part of a string, object , array is equal to smth:
```
var jsonData = pm.response.json();
pm.test("Body matches string", function () {
     pm.expect(jsonData.value).to.include("string_you_want_to_search");
 });
```
 or search a part of object:
```
 var jsonData = pm.response.json();
pm.test("Body matches string", function () {
     pm.expect(jsonData.value).to.include({key="value"});
 });
```
deep.include tests the whole structure:
```
 var jsonData = pm.response.json();
pm.test("Body matches string", function () {
     pm.expect(jsonData.value).to.deep.include({key="value"});
 });
```
##### 3)`nested.include`: for child objects
```
{a:{b:['x','y']}}
pm.expect(jsonData.a.b[1]).to.include('y');
```
or
```
pm.expect(jsonData.to.nested.include({'a.b[1]':'y'})
```
##### 4) `property`  - we test === (strictly) that the target has a property with given key
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.value).to.have.property('a');
 })
```
or
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.value).to.have.property('a','value');
 })
```
##### 5) `deep.property`
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.value1.value2).to.have.deep.property('a','value');
 })
```
##### 6) `nested.property` ( for objects and arrays)
Add `.nested` earlier in the chain to enable dot- and bracket-notation when referencing nested properties.
```
expect({a: {b: ['x', 'y']}}).to.have.nested.property('a.b[1]');
expect({a: {b: ['x', 'y']}}).to.have.nested.property('a.b[1]', 'y');
```
also I can use `nested.deep.property`
##### 7) check value type with `.property`
.property changes the target of any assertions that follow in the chain to be the value of the property from the original target object.

`expect({a: 1}).to.have.property('a').that.is.a('number');`
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.value1.value2).to.have.deep.property('a','value').that.is.a.('number');
 })
```
##### 8) for comfortable reading add `.a`:
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.value).to.have.a.property('a','value');
 })
```
##### 9) `keys`.     `all.keys`
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.value).to.have.all.keys('value1','value2') 
 })
```
or `any.keys`
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.value).to.have.any.keys('value1','value2') 
 })
```
##### 10. Finding types of elements with Chai.js `.a` , `.instanceof`
1)`.a` for number, string, object, array
```
var jsonData = pm.response.json();
pm.test("Your test name", function () {     
     pm.expect(jsonData.value).to.be.a('string');
 })
```
or
```
var jsonData = pm.response.json();
pm.test("Your test name", function () {     
     pm.expect(jsonData.value).to.be.an('array');
 })
```
2) `that.includes`
```
var jsonData = pm.response.json();
pm.test("Your test name", function () {     
     pm.expect(jsonData.value).to.be.an('array').that.includes({json_object});
 })
```
or
```
var jsonData = pm.response.json();
pm.test("Your test name", function () {     
     pm.expect(jsonData.value).to.be.an('array').that.deep.includes({json_object});
 })
```
3) `expect({a: 1}).to.have.property('a').that.is.a('number');`
4) `instanceOf` for own created arrays, objects and own functions
Asserts that the target is an instance of the given constructor.
```
function Cat () { }

expect(new Cat()).to.be.an.instanceof(Cat);
expect([1, 2]).to.be.an.instanceof(Array);
```
object literal:
```
var cat ={
     name:"Kitty",
     year:1,
     sleep: function(){
          //sleeping code
     }
}
```
about constructor:
```
function Cat (name, year){
    this.name=name;
    this.year=year;
    this.sleep=function(){
    //sleeping code
    }
}
var kitty - new Cat('Kitty',1);
```
`.instanceOf` check that `kitty` was made from constructor `Cat`

Example of usage:
```
function Animal() {}
function Rabbit() {}
Rabbit prototype = Object.create(Animal.prototype);
var rabbit = new Rabbit();
alert(rabbit instanceOf Rabbit);
alert(rabbit instanceOf Animal);
alert(rabbit instanceOf Object);
```
### 3. Tests for arrays
#### 3.1. Chai.js
##### 1) 
```
var jsonData = pm.response.json();
pm.test("Your test name", function () {     
     pm.expect(jsonData.value).to.be.an('array')
     })
```
extended:
```
var jsonData = pm.response.json();
pm.test("Your test name", function () {     
     pm.expect(jsonData.value).to.be.an('array').that.is.empty;
     pm.expect(jsonData.value).to.be.an('array').that.is.not.empty;
     pm.expect([1,2,3]).to.be.an('array').that.includes(2);
     });
```
##### 2) `expect([1, 2]).to.be.an.instanceof(Array);`
##### 3) `keys`.    
`all.keys`
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.value).to.have.all.keys('value1','value2') 
 })
```
or `any.keys`
```
pm.test("Your test name", function () {
     var jsonData = pm.response.json();
     pm.expect(jsonData.value).to.have.any.keys('value1','value2') 
 })
```
##### 4) `.members` only for arrays (any order but strictly ===)
```
pm.test("Your test name", function () {
     pm.expect([1, 2, 3]).to.have.members([2, 1, 3]);
 })
```
or `ordered.members`( testing the order strictly ===):
```
pm.test("Your test name", function () {
     pm.expect([1, 2, 3]).to.have.ordered.members([1,2,3]);
 })
```
or `include.members`( testing that member is included not strictly ==)
```
pm.test("Your test name", function () {
     pm.expect([1, 2, 3]).to.include.members([1,2]);
 })
```
or `include.deep.members` (not strictly ==, in child objects too)
```
pm.test("Your test name", function () {
     pm.expect([1, 2, 3]).to.include.deep.members([1,2]);
 })
```
##### 5) `.lengthOf`
```
pm.test("Your test name", function () {
     pm.expect([1, 2, 3]).to.have.lengthOf(3);
 })
```
or
```
// Recommended
expect([1, 2, 3]).to.have.lengthOf(3);

// Not recommended
expect([1, 2, 3]).to.have.lengthOf.above(2);
//more than
expect([1, 2, 3]).to.have.lengthOf.below(4);
//less than
expect([1, 2, 3]).to.have.lengthOf.at.least(3);
//more or equal
expect([1, 2, 3]).to.have.lengthOf.at.most(3);
//less or equal
expect([1, 2, 3]).to.have.lengthOf.within(2,4);
//the target is a number or a date greater than or equal to the given number or date start, and less than or equal to the given number or date finish respectively
```
##### 6) `null, empty, exist`
```
pm.expect(jsonData.companys).to.not.be.null;
pm.expect(jsonData.companys).to.not.be.empty;
pm.expect(jsonData.companys).to.exist;
```
##### 7) `eql`
```
pm.test("test order", function () {
     pm.expect(jsonData.company[0].id_company).to.eql(99);
     pm.expect(jsonData.company[0].name).to.eql('Cathalina');
     pm.expect(jsonData.company[1].id_company).to.eql(86);
     pm.expect(jsonData.company[1].name).to.eql('Angelina');
 });
```
### 4. Tests for the body : string in JSON (Chai.js)
```
pm.expect(pm.response.json()).to.be.a("string");
pm.expect(pm.response.json()).to.equal("error");
pm.expect(pm.response.json()).to.include("rr");
pm.expect(pm.response.json().name).to.have.lengthOf(33);
pm.expect(pm.response.json().name).to.have.lengthOf.above(33);
pm.expect(pm.response.json().message === 'Success!').to.be.ok;
pm.expect(pm.response.json().message === 'Success!').to.be.true;
pm.expect(pm.response.json().name).to.not.be.null;
pm.expect(pm.response.json().name).to.not.be.empty;
pm.expect(pm.response.json().name).to.exist;
```
### 5. Tests for the body : number in JSON (Chai.js)
```
pm.expect(pm.response.json().task).to.be.a("number");
pm.expect(pm.response.json().task).to.equal("100");
~~pm.expect(pm.response.json().task).to.include("99");~~ pm.expect(pm.response.json().task).to.be.oneOf([200,201,202]);
pm.expect(pm.response.json().task).to.be.below(99);
pm.expect(pm.response.json().task).to.be.above(99);
num=jsonData.task;
pm.expect(num===33).to.be.ok;
pm.expect(num===33).to.be.true;
pm.expect(num=='33').to.be.ok;
pm.expect(num=='33').to.be.true;
pm.expect(num).to.not.be.null;
pm.expect(num).to.not.be.empty;
pm.expect(num).to.not.be.undefined;
pm.expect(num).to.not.be.NaN;
pm.expect(num).to.exist;
