The order of executing code isn't always completly clear. You might think that you've got it but there might be something else that tricks your mind.

In this example we throw an exception in a function that we will try to catch in a try-catch statement. But will that really happen?
```javascript
async function rejects() {
    throw new Error('Ouch')
}

async function main() {
    try {
        return rejects()
    } catch(e) {
        console.log('rejects failed')
    }
}

main().catch(e => {
    console.log('Main failed', e)
})
```
If you run this code you might be surprised to find that it will output "Main failed Error: Ouch". Why???

Well the reason might become obvious when you take into consideration that the function rejects will return a Promise which is what will be returned from the main function.

There are a few ways to alter this code to make it work like you might have intended.
```javascript
function rejects() {
    throw new Error('Ouch')
}

async function main() {
    try {
        return rejects()
    } catch(e) {
        console.log('rejects failed')
    }
}

main().catch(e => {
    console.log('Main failed', e)
})
```
If you remove async from the rejects function it will no longer return a Promise and the try-catch in the main function will catch the exception.

You can also handle it by placing an await on the call to rejects
```javascript
async function rejects() {
    throw new Error('Ouch')
}

async function main() {
    try {
        return await rejects()
    } catch(e) {
        console.log('rejects failed')
    }
}

main().catch(e => {
    console.log('Main failed', e)
})
```
Now the await will handle the Promise returned and throw the exception to be catched in the try-catch.

A more complete version might be to catch it from the reject call.
```javascript
async function rejects() {
    throw new Error('Ouch')
}

async function main() {
    try {
        return rejects().catch(e => {
            console.log('rejects failed but caught with catch', e)
        })
    } catch(e) {
        console.log('rejects failed')
    }
}

main().catch(e => {
    console.log('Main failed', e)
})
```
