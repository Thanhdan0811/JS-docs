# Set
- Store (nested) data of any kind and length.
- Iterable, also some special set methods available.
- Order is not guaranteed, duplicates are Not allowed, no Index-based access.


```
const ids = new Set([1,2,3]);
console.log(ids[0]); //=> undefined.
console.log(ids.has(1)); // => true.

ids.add(2); // => still have three elements, 'cause duplicate.

ids.entries(); // => return iterable, can use with for loop or foor of.
ids.entries(); => return [[1,1], [2,2], [3,3]] 

ids.delete(1); // => delete it, if not found show no errors.


```

# Map 
- Store (nested) data of any kind and length and key values are allowed.
- Iterable, also some special map methods available.
- Order is guaranteed, duplicates are Not allowed, key-based access.


```
const person1 = {name: 'Max'};
const person2 = {name: 'Manual'};

const personData = new Map([[person1, [{date:'yesterday', price: 10}]]]);

console.log(personData);
console.log(personData.get(person1));

```
