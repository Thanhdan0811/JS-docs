# Export before declarations.
- We can label any declaration as exported by placing _export_ before it, be it a variable, function, or a class.
```
// export an array
export let months = ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

// export a constant
export const MODULES_BECAME_STANDARD_YEAR = 2015;

// export a class
export class User {
  constructor(name) {
    this.name = name;
  }
}
```
- _NOTE_ : No semicolons after export class/function

# Export apart fron declarations
```
function sayHi(user) {
  alert(`Hello, ${user}!`);
}

function sayBye(user) {
  alert(`Bye, ${user}!`);
}

export {sayHi, sayBye}; // a list
```
- Technically, we could put export above functions as well.

# Import *
- Usually , we put a list of what to import in curly braces _import {...}_
```
// 📁 main.js
import {sayHi, sayBye} from './say.js';

sayHi('John'); // Hello, John!
sayBye('John'); // Bye, John!
```

- We can import everything as an object using _import * as <obj>_
```
// 📁 main.js
import * as say from './say.js';

say.sayHi('John');
say.sayBye('John');
```


# Import "as"
- We can also use _as_ to import under different names.
```
// 📁 main.js
import {sayHi as hi, sayBye as bye} from './say.js';

hi('John'); // Hello, John!
bye('John'); // Bye, John!
```

# Export "as"
- The similar syntax exists for _export_
```
// 📁 say.js
...
export {sayHi as hi, sayBye as bye};

// 📁 main.js
import * as say from './say.js';

say.hi('John'); // Hello, John!
say.bye('John'); // Bye, John!
```


# Export default
```
// 📁 user.js
export default class User { // just add "default"
  constructor(name) {
    this.name = name;
  }
}

// 📁 main.js
import User from './user.js'; // not {User}, just User

new User('John');
```
- As there may be at most one default export per file, the exported entity _may have no name_.

```
export default class { // no class name
  constructor() { ... }
}

export default function(user) { // no function name
  alert(`Hello, ${user}!`);
}

// export a single value, without making a variable
export default ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
```


# Re-export
-“Re-export” syntax export ... from ... allows to import things and immediately export them (possibly under another name), like this:
```
export {sayHi} from './say.js'; // re-export sayHi

export {default as User} from './user.js'; // re-export default
```


# Re-exporting the default export

```
// 📁 user.js
export default class User {
  // ...
}


/// If we’d like to re-export both named and default exports, then two statements are needed:
export * from './user.js'; // to re-export named exports
export {default} from './user.js'; // to re-export the default export

```
