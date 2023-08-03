# Must know spread and rest operator tricks in JS

### Spread operator:

#### 1. Pass an array as arguments of function:

```jsx
let arr = [3, 5, 1];

Math.max(...arr); // 5
```

Or several arrays:

```jsx
let arr1 = [1, -2, 3, 4];
let arr2 = [8, 3, -8, 1];

Math.max(...arr1, ...arr2); // 8
```
&nbsp;
#### 2. Merge arrays:

```jsx
const array1 = [1, 2, 3];
const array2 = [4, 5, 6];
const mergedArray = [...array1, ...array2]; // [1, 2, 3, 4, 5, 6]
```

And merge objects:

```jsx
const object1 = { a: 1, b: 2 };
const object2 = { c: 3, d: 4 };
const mergedObject = { ...object1, ...object2 }; // { a: 1, b: 2, c: 3, d: 4 }
```

Object properties can be updated while merging:

```jsx
const originalPerson = { name: 'Alice', age: 30 };
const updatedPerson = { ...originalPerson, age: 31 }; 
console.log(updatedPerson); // {name: 'Alice', age: 31}
```
&nbsp;
#### 3. Add new elements in existing array:

```jsx
const originalArray = [1, 2, 3];
const newArray = [...originalArray, 4, 5]; // [1, 2, 3, 4, 5]
```
&nbsp;
#### 4. Сlone array and objects:

```jsx
const originalArray = [1, 2, 3];
const copyArray = [...originalArray];

const originalObject = { a: 1, b: 2 };
const copyObject = { ...originalObject };
```
&nbsp;
#### 5. Convert a string to an array

```jsx
let str = "Hello";
console.log( [...str] ); // H,e,l,l,o
```

Another example - spread operator in the middle:

```jsx
let chars = ['a', ...'bcd', 'e'];
console.log(chars); // ["a", "b", "c", "d", "e"]
```
&nbsp;
#### 6. Create an array from Set:

```jsx
const set = new Set([1, 2, 3]);
const arrayFromSet = [...set];
```

With Set and spread operator you can remove duplicates from an array:

```jsx
const arr = [1,1,1,2];
const uniqueArr = [...new Set(arr)];   
console.log(uniqueArr);  //[1,2]
```
&nbsp;
### Rest parameters:

Rest parameters allow you to represent an indefinite number of arguments as an array.

Here are the main differences of spread and rest:

- The spread operator (`...`) unpacks the elements of an iterable object.
- The rest parameter (`...`) packs the elements into an array.
  
&nbsp;
#### 1. Gather all function arguments into an array:

```jsx
function printArgs(...args) {
  console.log(args);
}

printArgs('hello', 'world'); // ['hello', 'world']
```

Can be combined with regular params:

```jsx
function printInfo(name, age, ...details) {
  console.log(name, age, details);
}
```
&nbsp;
#### 2. Destructing:

```jsx
const { name, ...restInfo } = { name: 'Alice', surname: 'Johnson', age: 30 };
console.log(name); // { name: 'Alice' }
console.log(restInfo); // { surname: 'Johnson', age: 30 }
```

And destructing arrays:

```jsx
const [ num0, ...others ] = [ 1, 2, 3, 4, 5, 6 ]

console.log(num0) // 1
console.log(others) // [2, 3, 4, 5, 6]
```
&nbsp;
#### 3. Excluding properties:

```jsx
function noName({ name, ...rest }) {
  return rest;
}
let person = { name: 'Alice', surname: 'Johnson', age: 30 };
noName(person); // {surname: 'Johnson', age: 30}
```

Or you can dynamically exclude property:

```jsx
const removeProperty = prop => ({ [prop]: _, ...rest }) => rest

const removeName = removeProperty('name');
const removeId = removeProperty('id');

const user = { id: 1, name: 'John', surname: 'Show' };
removeName(user); //=> { id: 100, surname: 'Show' }
removeId(user); //=> { name: 'John', surname: 'Show' }
```
&nbsp;
#### 4. Organize properties:

```jsx
const user = {
  password: 'Password!',
  name: 'John',
  id: 11
}

const organize = object => ({ id: undefined, ...object })
```
&nbsp;
#### 5. Add conditional properties:

```jsx
const user = { name: 'John', id: 11 };
const password = 'Password!'
const userWithPassword = {
  ...user,
  ...(password && { password })
}

userWithPassword //=> { name: 'John', id: 11, password: 'Password!' }
```

