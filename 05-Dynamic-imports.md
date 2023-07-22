# The import() expression
- The import(module) expression loads the module and returns a promise that resolves into a module object that contains all its exports.
- It can be called from any place in the code.
```
let modulePath = prompt("Which module to load?");

import(modulePath)
  .then(obj => <module object>)
  .catch(err => <loading error, e.g. if no such module>)
```

- Or from file :
```
// 📁 say.js
export function hi() {
  alert(`Hello`);
}

export function bye() {
  alert(`Bye`);
}

let {hi, bye} = await import('./say.js');

hi();
bye();

//////////////////////////////////////////
// 📁 say.js
export default function() {
  alert("Module loaded (export default)!");
}

//
let obj = await import('./say.js');
let say = obj.default;
// or, in one line: let {default: say} = await import('./say.js');

say();

```

- _NOTE_ : Although import() looks like a function call, it’s a special syntax that just happens to use parentheses (similar to super()).
- So we can’t copy import to a variable or use call/apply with it. It’s not a function.
