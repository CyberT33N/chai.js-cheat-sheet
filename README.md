# Chai.js Cheat Sheet (https://www.npmjs.com/package/chai)
Chai.js Cheat Sheet with the most needed stuff ..








<br><br>

# Install
```bash
npm i -D chai
```

- Import the library in your code, and then pick one of the styles you'd like to use - either assert, expect or should:
```bash
var chai = require('chai');  
var assert = chai.assert;    // Using Assert style
var expect = chai.expect;    // Using Expect style
var should = chai.should();  // Using Should style
```




<br><br>




<br><br>

# Expect (https://www.chaijs.com/api/bdd/)

<br><br>

## .exist
```javascript
expect(project.entities).to.exist
expect(project.entities).to.not.exist
```
<br><br>

## .include
```javascript
expect('foobar').to.include('foo');
```

<br><br>

## Check if array is included in array
```javascript
expect(['a', 'b', 'c']).to.include.members('a', 'c');
```

<br><br>



## deep.include
```javascript
// Target array deeply (but not strictly) includes `{a: 1}`
expect([{a: 1}]).to.deep.include({a: 1});
expect([{a: 1}]).to.not.include({a: 1});

// Target object deeply (but not strictly) includes `x: {a: 1}`
expect({x: {a: 1}}).to.deep.include({x: {a: 1}});
expect({x: {a: 1}}).to.not.include({x: {a: 1}});
```

<br><br>

## .equal
```javascript
const foo = 'bar';
expect(foo).to.equal('bar');
```

<br><br>

#### .eql
- eql. Eql is based on the deep-eql project. It works by looking at the content of the expressions being compared.
```javascript
expect([1, 2, 3]).to.equal([1, 2, 3]); // fails
expect([1, 2, 3]).to.eql([1, 2, 3]); // passes
```

<br><br>

#### deep equal
- Because objects use different instances you must use deep equal in order to compare the content of two objects
```javascript
const obj = {a: true, b: true};
const compare = obj === obj;
console.log(compare); // false

expect(obj).to.deep.equal(obj)
```

<br><br>

#### deep equal any order (https://www.npmjs.com/package/deep-equal-in-any-order)
```javascript
const deepEqualInAnyOrder = require('deep-equal-in-any-order');
const chai = require('chai');

chai.use(deepEqualInAnyOrder);

const { expect } = chai;

expect([1, 2]).to.deep.equalInAnyOrder([2, 1]);
expect([1, 2]).to.not.deep.equalInAnyOrder([2, 1, 3]);
expect({ foo: [1, 2], bar: [4, 89, 22] }).to.deep.equalInAnyOrder({ foo: [2, 1], bar: [4, 22, 89] });
expect({ foo: ['foo-1', 'foo-2', [1, 2], null ] }).to.deep.equalInAnyOrder({ foo: [null, [1, 2], 'foo-1', 'foo-2'] });
expect({ foo: [1, 2], bar: { baz: ['a', 'b', { lorem: [5, 6] }] } }).to.deep.equalInAnyOrder({ foo: [2, 1], bar: { baz: ['b', 'a', { lorem: [6, 5] }] } });
```



<br><br>

## .contain
```javascript
expect('My name is Jeff').to.contain('My name is')
```

























































































<br><br>
_________________________________________________________
_________________________________________________________
<br><br>

## Type

<br><br>

```javascript
expect([]).to.be.an('array')
expect('blaa').to.be.an('string')
```































<br><br>
_________________________________________________________
_________________________________________________________
<br><br>

## Object

<br><br>

## check if object includes all properties inside of array
```javascript
const obj = {
  "useNewUrlParser": "true",
  "useUnifiedTopology": "true",
  "connectTimeoutMS": "10000",
  "socketTimeoutMS": "45000"
};

expect(obj).to.include.all.keys("useNewUrlParser", "socketTimeoutMS");
```



<br><br>

## check if object includes specific keys
```javascript
var obj= {
  user: "user",
  title: "title",
  content: "content",
  message: "message"
};

const headers = ['user', 'title']
expect(obj).include.keys(headers)
```









































<br><br>
_________________________________________________________
_________________________________________________________
<br><br>

## promises
```javascript
const chai = require('chai');
chai.use(require('chai-as-promised'));
chai.should();

it('reject expected', () => {
  return expect(new Promise((res,rej) => {rej()})).to.be.rejected
})
it('reject unexpected', () => {
  return expect(new Promise((res,rej) => {rej()})).to.be.fulfilled
})
```





































































<br><br>
_________________________________________________________
_________________________________________________________
<br><br>

## regex
```javascript
expect('foobar').to.match(/^foo/);
```













































<br><br>
_________________________________________________________
_________________________________________________________
<br><br>


## throw (https://www.chaijs.com/api/bdd/#method_throw)
- does not work with async functions. Check below for working example
```javascript
var badFn = function () { throw new TypeError('Illegal salmon!'); };
expect(badFn).to.throw(TypeError);

// example with executing funtion
expect(() => validateModels(models)).to.throw('bla bla')
```

<br><br>


## not throw (https://www.chaijs.com/api/bdd/#method_throw)
- does not work with async functions. Check below for working example
```javascript
var goodFn = function () {};

expect(goodFn).to.not.throw(); // Recommended
expect(goodFn).to.not.throw(ReferenceError, 'x'); // Not recommended

// example with executing funtion
expect(() => validateModels(models)).to.not.throw();
```

<br><br>


## await (https://www.chaijs.com/plugins/chai-as-promised/)
```javascript
const chai = require('chai')
const expect = chai.expect
chai.use(require('chai-as-promised'))

// Always succeeds
async function wins() {
  return 'Winner'
}

// Always fails with an error
async function fails() {
  throw new Error('Contrived Error')
}

it('wins() returns Winner', async () => {
  expect(await wins()).to.equal('Winner')
})

it('fails() throws Error', async () => {
  // rejectedWith has same logic like includes
  await expect(fails()).to.be.rejectedWith(Error)
  // await expect(fails()).to.rejected
})

// you can also use

```
















































<br><br>
_________________________________________________________
_________________________________________________________
<br><br>


## instanceof (https://www.chaijs.com/api/bdd/#method_instanceof)
```javascript
function Cat () { }

expect(new Cat()).to.be.an.instanceof(Cat);
expect([1, 2]).to.be.an.instanceof(Array);
```

