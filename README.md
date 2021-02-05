# Chai.js Cheat Sheet
Chai.js Cheat Sheet with the most needed stuff ..



<br><br>

# Expect

<br><br>

## equal
```javascript
const foo = 'bar';
expect(foo).to.equal('bar');
```

<br><br>

#### eql
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
