# Mind boggling puzzles

## Not equal to itself
Is there a way to have something that is not equal to itself?
```javascript
if(x !== x) {
    console.log('Could you ever end up here?');
}
```
If this is true then you'll have to have something that seemingly breaks the laws of physics, or in this case a language construct.

There is one thing in javascript that if unique for every call to itself and that is NaN, or not a number, which is an internal construct in the language that is meant to return a different reference everytime it's called.
```javascript
const x = NaN;
if(x !== x) {
    console.log('Could you ever end up here?');
}
```