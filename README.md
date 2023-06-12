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
3) 
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
~~pm.expect(pm.response.json().task).to.include("99");~~ 

pm.expect(pm.response.json().task).to.be.oneOf([200,201,202]);
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
```
### 6. Tests for the body : JSON (Node.js)
1)
```
jsonData = pm.response.json();
const assert = require('assert');
pm.test('Test assert.ok', funcion ()  {
    assert.ok(jsonData.message == 'Registration completed!'); });
```
Note:  not strict
2)
```
pm.test("assert", function () {
     assert.(jsonData.message === 'Registration completed!'); });
 })
```
Note:  strict
3)
```
pm.test("assert", function () {
     assert.deepEqual(jsonData.message,'Registration completed!');
 })
```
Note: not strict, use in child objects
4)
```
pm.test("assert", function () {
     assert.deepStrictEqual(jsonData.message,'Registration completed!');
 })
```
Note: strict, use in child objects
5)
```
pm.test("assert", function () {
     assert.equal(jsonData.message,'Registration completed!');
 })
```
Note: not strict, not use in child objects
6)
```
pm.test("assert", function () {
     assert.strictEqual(jsonData.message,'Registration completed!');
 })
```
Note: strict, not use in child objects.
or
```
pm.test("assert", function () {
     assert.strictEqual(jsonData.message,{
     message:'Registration completed'
     }
     )});
```
### 7. Tests for the body: XML (Postman)
```
var jsonData = xml2Json(responseBody);
pm.test("Your test name", function () {
     pm.expect(jsonData).to.include({
     key: 'value1';
     key2:'value2';});
 })
```
### 8. Test on headers (Postman)
1)
```
 pm.test("Content-Type is present", function () {
     pm.response.to.have.header("Content-Type");
 });
 ```
 or
 ```
 pm.test("Content-Type is present", function () {
     pm.response.to.have.header("Content-Type". 'application/json');
 });
 ```
 2)
 ```
 pm.test("Body matches string", function () {
     pm.expect(pm.response.headers).to.include("string_you_want_to_search");
 });
 ```
3)
 ```
 console.log(pm.response.headers.contentSize());
```
 4)
 ```
  pm.test("Body matches string", function () {
     pm.expect(pm.response.headers.count()).to.eql(9);
 });

 ```

5) high priority
```
 pm.test("Body matches string", function () {
     pm.expect(pm.response.headers.get("Cache-Control")).to.include('no-cache');
 });

```
6)
```
 pm.test("Body matches string", function () {
     pm.expect(pm.response.headers.has("Content-Type88")).to.be.true;
 });
 ```
 or
 ```
  pm.test("Body matches string", function () {
     pm.expect(pm.response.headers.has("Content-Type88", 'application/json')).to.be.true;
 });
 ```
 7)
 ```
 pm.test("Body matches string", function () {
     pm.expect(pm.response.headers.idx(7).key).to.eql("Cache-Control");
 });
 ```
 7)
 ```
 pm.test("Body matches string", function () {
     pm.expect(pm.response.headers.indexOf('Cache-Control')).to.eql(7);
 });
```
 ### 9. Test on Cookies (Postman)
1)
```
 pm.test("Body matches string", function () {
     pm.expect(pm.cookies.has(cookieName:String)).to.be.true;
 });
 ```
2)
```
pm.test("Body matches string", function () {
     pm.expect(pm.cookies.count()).to.eql(9);
 });
```
3) high priority
```
 pm.test("Body matches string", function () {
     pm.expect(pm.cookies.get(cookieName:String)).to.eql('string');
 });
```
4)
```
pm.test("Body matches string", function () {
     pm.expect(pm.cookies.has(cookieName:String, 'value')).to.be.true;
 });
 ```
5)
```
pm.test("Body matches string", function () {
     pm.expect(pm.cookies.idx(0).value).to.eql('string')
 });
```
6)
```
pm.test("Body matches string", function () {
     pm.expect(pm.cookies.idexOf(cookieName:String)).to.eql(0)
 });
```
## 2.Reserved symbols:
```
Code	Result
\b	Backspace
\f	Form Feed
\n	New Line
\r	Carriage Return
\t	Horizontal Tabulator
\v	Vertical Tabulator
```
## 3. Methods for Strings
var  x= 'Mariia'
### 1) `length`:
var txt = 'Very long string'
var ln = txt.length

pm.test("length 5", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.type.length).to.eql(5);
});

### 2)`indexOf` cannot use regexp
```
var txt = 'I want to go to the sea, to the sea I want to go'
txt.indexOf('sea')
console: number
```
if there is no match , then console: - 1
`lastIndexOf`
`txt.lastIndexOf('sea')`
`txt.lastIndexOf('sea', 15)` -incluse start position for search

### 4. `search` cannot use start position argument but can use regexp
`txt.search('sea')`

### 5. `slice` 
```
var fruits = 'apple, mango, peach';
fruits.slice(8,13) 
```
here start position is included and stop position is not included
`fruits.slice(-13,-8)` reversed slice
always use console
`fruits.slice (8)`
`fruits.slice(-13)`
from start position to the end
### 6. `substring ` dont use negative numbers as arguments
```
var fruits = 'apple, mango, peach';
fruits.substring(8,13)
```
and ` substr`
```
var fruits = 'apple, mango, peach';
fruits.substr(8,5)
```
Here second argument is not stop position, it is length
`fruits.substr(-13,5)`
`fruits.substr(-13,-5)` - not working
### 7. changing part of a string  by `replace`
`Replace` changing only one match
```
txt = "Hello, Anonimus!";
txt2 = txt.replace('Anonimus", "Kate")
console.log(txt2)
```
or case insensitive
```
txt = "Hello, Anonimus! Anonimus, right?";
txt2 = txt.replace('/ANONIMUS/i", "Kate")
console.log(txt2)
```
or for two words:
```
txt = "Hello, Anonimus Anonim!";
txt2 = txt.replace('/ANONIMUS ANONIM/i", "Kate")
console.log(txt2)
```
or global(all replacement)
```
txt = "Hello, Anonimus! Anonimus, right?";
txt2 = txt.replace('/Anonimus/g", "Kate")
console.log(txt2)
```
### 8. Changing registr in the string
```
var text1 = "Hello World!";
ver text2 = text1.toUpperCase();
console.log(text2);
HELLO WORLD!
```
or
```
var text1 = "Hello World!";
ver text2 = text1.toLowerCase();
console.log(text2);
hello world!
```
### 9. 'glueing` two strings 
with `+`
```
txt1 = "Sea";
txt2 = "wind";
txt3 = txt1 + ""+ txt2
Sea wind
```
with `concat()`
```
txt1 = "Sea";
txt2 = "wind";
txt3 = txt1.concat(""+ txt2);
Sea wind
```
### 10. Deleting redundant spaces in the string (in the start of the string and in the end)
```
txt = "  Sea wind  ";
console.log(txt1.trim());
Sea wind
```
### 11. Dividing to parts
```
fruits = "Apple, pineapple, coconut";
fruits.split(",");
```
`split()` is transforming string to a array ==>

`["Apple"," pineapple"," coconut"]` then we need to trim it from extra spaces
or we can do split another way( include there extra spaces):
`fruits.split(", ");`
example:
```
cat = "Kitty";
console.log(cat.split("");
["K", "i", "t", "t", "y"]
```
## 4. Methods for Numbers
### 1) `toString`
```
x= 123;
y = x.toString();
console.log(x);
console.log("x===y " +  Boolean(x===y));
```
this `y` you can compare to another string by ===.
### 2) convert string to number( global js-methods)
The `Number()` method
The `parseInt()` method
The `parseFloat()` method

#### 2)1). returnings of function `Number()`

```
console.log(Number(true));     // returns 1
console.log(Number(false));    // returns 0
console.log(Number("10"));     // returns 10
console.log(Number(" 10"));     // returns 10
console.log(Number("10 "));     // returns 10
console.log(Number(" 10 "));     // returns 10
console.log(Number("10.33"));     // returns 10.33
console.log(Number("10,33"));    // returns NaN
console.log(Number("10 33"));    // returns NaN
console.log(Number("John"));    // returns NaN
console.log(Number(new Date("2017-09-30")));  
//1506729600000 ( method will count ms started from 01.01.1970)
```
#### 2)2) `parseInt("10.33");
```
//10
console.log(parseInt(true));    // returns NaN
console.log(parseInt(false));    // returns NaN
```
#### 2)3) `parseFloat("10.33")`
```
//10.33
console.log(parseFloat(true));    // returns NaN
console.log(parseFloat(false));    // returns NaN
```
## 5. Methods for arrays in JS
```
var nums = new Array(1,2,3);
var nums = [1,2,3]; //literal syntaxis
```
### length:
```
fruits = ["apple, "banana', "orange","pear", "plum", "pineapple"];
fruits.length; // 6
pineapple = fruits[fruits.length -1];
console.log("Last element of array: " + pineapple);
```
### adding elements to array
`push` to the end of array
```
fruits = ["banana", "orange"];
fruits.push("pear");
// ["banana", "orange", "pear"]
```
and
```
fruits = ["banana", "orange"];
x = fruits.push("pear");
// x = 3
```
`x[x.length]` to the end of array
```
fruits = ["banana", "orange"];
fruits[fruits.length] = "pear";
// ["banana", "orange", "pear"]
```
`unshift()` to the beginning of the array
```
fruits = ["banana", "orange"];
fruits.unshift("pear");
// ["pear", "banana", "orange"]
```
`splice` adding and deleting elements in any part of array (defining start position(2) and number of deleting objects(0))
```
fruits = ["apple", "banana", "pear"];
fruits.splice(2,0,"lemon", "orange");
// ["apple", "banana", "pear", "lemon", "orange"]
```
Note: we cannot create a new variable with this? `splice` will rewrite the array.
if we want to delete one element ("pear") and add other elements:
```
fruits = ["apple", "banana", "pear", "mango"];
fruits.splice(2,1,"lemon", "orange");
// ["apple", "banana", "lemon", "orange", "mango"]
```
### editing elements in array
```
fruits = ["apple", "banana", "pear", "mango"];
fruits[0] = "kiwi";
// ["kiwi", "banana", "pear", "mango"];
```
### deleting element from array
`pop()` deleting the last element of array
```
fruits = ["apple", "banana", "pear"];
fruits.pop();
// ["apple", "banana"]
x = fruits.pop();
// x = "pear"
```
`shift()` deleteng the first element
```
fruits = ["apple", "banana", "pear"];
fruits.shift();
// ["banana", "pear"]
x = fruits.shift();
// x = "apple"
```
`delete` deleting element in the middle it delets the element but left undefined instead
```
fruits = ["apple", "banana", "pear"];
delete fruits[1];
// ["apple", undefined, "pear"]
```
`splice` defining start pisition and how many elements to delete
```
fruits = ["apple", "banana", "pear"];
fruits.splice(0,1);
// ["banana", "pear"]
```
we can delete as many elements as we want
```
fruits = ["apple", "banana", "pear"];
fruits.splice(0,2);
// ["pear"]
```
### transform array into a string ( separeter is comma)
`toString()`
```
fruits = ["apple", "banana", "pear"];
y = fruits.toString();
// apple,banana,pear
```
`join()` we define separeter
```
fruits = ["apple", "banana", "pear"];
y = fruits.join(", ");
// apple, banana, pear
```
or
```
fruits = ["apple", "banana", "pear"];
y = fruits.join(" * ");
// apple * banana * pear
```
### Union of arrays
```
fruits1 = ["apple", "banana"];
fruits2 = ["pear", "kiwi"];
fruits = fruits1.concat(fruits2);
//["apple", "banana","pear", "kiwi"];
```
or
```
fruits1 = ["apple", "banana"];
fruits2 = ["pear", "kiwi"];
fruits3 = ["mango", "orange"];
fruits = fruits1.concat(fruits2, fruits3);
//["apple", "banana","pear", "kiwi", "mango", "orange"];
```
or
```
fruits1 = ["apple", "banana"];
fruits = fruits1.concat(["pear", "kiwi"]);
//["apple", "banana","pear", "kiwi"];
```
### copy a part of array (1 element included, last element not included)
```
fruits = ["apple", "orange","lemon", "kiwi"];
citrus = fruits.slice(1,3);
// ["orange","lemon"]
```
or
```
fruits = ["apple", "orange","lemon", "kiwi"];
citrus = fruits.slice(1);
// ["orange","lemon", "kiwi"];
```
### sorting the array
`sort`
```
fruits = ["apple", "orange","lemon", "kiwi"];
fruits.sort();
// ["apple", "kiwi","lemon","orange"];
```
or 
```
fruits = ["apple", "orange","lemon", "kiwi"];
fruits.sort();
fruits.reverse();
// ["orange", "lemon", "kiwi", "apple"];
```

## 6. Methods for dates
```
 var jsonData = pm.response.json();
data_for_test = new Date(jsonData.fields.)
date_result = new Date(2023, 5,8);
date_test_1 = date_result.toDateString();
date_test_2 = date_for_test.toDateString();
pm.test("Your test name", function () {
   
    pm.expect(date_test_1).to.eql(date_test_2);
});
```
also use
`getFullYear()`
`getMonth()`
## 7. Mathematic functions in JS
### Math.random

`x = Math.random();`
`x = Math.random()*11;` will output random NOT integer number from 0 to 10
`x = Math.floor(Math.random() * 11);` will output random integer number from 0 to 10 ( it will not round but it will cut the float part)
### Math.min
```
Math.min(0, 150, 30, 20, -8, -200);
// returns -200
```
### Math.max
```
Math.max(0, 150, 30, 20, -8, -200);
// returns 150
```
### example of complicated test


