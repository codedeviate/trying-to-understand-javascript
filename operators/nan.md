# NaN

```javascript
const x = parseInt('abc');
console.log(x); // NaN
console.log(isNaN(x)); // true
console.log(x === NaN); // false
```
The result from the first two console.logs shouldn't be any surprice. But the last console.log might be something you might not have anticipated.
NaN is an internal construction in javascript that is unique for every time you call it. So if you compare it to itself it is no longer the same.

If you have two variables that you with to compare and they both turn out to be strings then you might be in for a nasty treat.
```javascript
const x = 'abc';
const y = 'def';
if(parseInt(x) === parseInt(y)) {
    console.log('x and y have the same nuemeric value');
}
```
Even though x and y both seems to be equal to 0 they are not the same when compared since they both becomes NaN.