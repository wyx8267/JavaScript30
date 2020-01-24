# 14 Must Know Dev Tool Tricks

## 调试技巧

```javascript
    // Regular
        console.log('hello')
    // Interpolated
        console.log('Hello I am a %s string!', 'JS')

    // Styled
        console.log('%c I am a great text', 'font-size: 40px;background: blue; text-shadow: 10px 10px 0 #ace;')
    // warning!
        console.warn('OH NOOOOO')
    // Error :|
        console.error('OH NOOOOO')
    // Info
        console.info('OH NOOOOO')
    // Testing
        const p = document.querySelector('p');
        console.assert(p.classList.contains('ouch'), 'Wrong!!!')
    // clearing
        console.clear()
    // Viewing DOM Elements
        console.log(p)
        console.dir(p)
    // Grouping together
        dogs.forEach(dog=>{
            console.group(`${dog.name}`)
            console.log(`This is ${dog.name}`)
            console.log(`${dog.name} is ${dog.age * 7} years old.`)
            console.groupEnd(`${dog.name}`)
            })
    // counting
        console.count('Res')
        console.count('Res')
        console.count('Dogee')
        console.count('Dogee')
        console.count('Res')
        console.count('Res')
        console.count('Res')
        console.count('Dogee')
        console.count('Res')
    // timing
        console.time('fetching data')
        fetch('https://api.github.com/users/wyx8267')
            .then(data=>data.json())
            .then(data=>{
                console.timeEnd('fetching data')
                console.log(data)
            })

        console.table(dogs)
```