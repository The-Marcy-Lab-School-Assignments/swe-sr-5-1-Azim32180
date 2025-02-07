# Technical Writing Assignment

For guidance on setting up and submitting this assignment, refer to the Marcy lab School Docs How-To guide for [Working with Short Response and Coding Assignments](https://marcylabschool.gitbook.io/marcy-lab-school-docs/fullstack-curriculum/how-tos/working-with-assignments#how-to-work-on-assignments).

## Prompt 1

Imagine you are teaching a friend about OOP. They mainly want to understand what is Encapsulation. Write a brief lesson on Encapsulation that includes the following:

- What is encapsulation?
- What major goal does this help to achieve in software engineering?
- Give an example (in code) of encapsulation.
- An explanation of how the code example demonstrates encapsulation

### Response 1

## Prompt 2

The following `friendsManager` object is an example of an interface that is **NOT** consistent and predictable:

```js
const friendsManager = {
  friends: [],
  addFriend(newFriend) {
    if (typeof newFriend !== "string") return;
    this.friends.push(newFriend);
  },
};

friendsManager.addFriend("daniel");
friendsManager.addFriend(true);
friendsManager.friends.push("emmaneul");
friendsManager.friends.push(42);
```

Explain how the code is not consistent or predictable, then provide an example in code that uses closure to make it more consistent and predictable.

### Response 2

`friendsManager` function has some issues that prevents it from being consistent and predictable. The `friends` array is publicly accessible, meaning anyone can change it using `friendsManager.friends.push("friend")`. Since the array is publicly exposed, the user can bypass `addFriend()` method and push any data type (including non-string, boolean, etc.) values to the array which leads to inconsistent behavior of the output. We want to set up the `friends` array so that it can be modified only using the `addFriend()` method and not bypass any restrictions we specify in our method. Also `friendsManager` is a plain object and not a class-based or factory-based structure that allows to create multiple instances.

Here is an example of the revised code above that is consistent with OOP guidelines and is more predictable:

```js
class FriendsManager {
  // creates a private array where we can store all the friends of the individual instances
  #friends = [];

  addFriend(newFriend) {
    if (typeof newFriend !== "string") {
      console.log("Only strings allowed bro...");
      return;
    }
    this.#friends.push(newFriend);
  }

  getFriends() {
    // returns a shallow copy of the array to prevent the direct mutation
    return [...this.#friends];
  }
}

// creates a new instance
const danny = new FriendsManager();

// adds a new friend
danny.addFriends("Josh");

// does not add new friend because of the validation
danny.addFriends(213);

// returns ["Josh"]
console.log(danny.getFriends());

// throws a syntax error because cannot access the `friends` array directly
console.log(danny.#friends);
```

## Prompt 3

With OOP in JavaScript, it's possible to use factory functions to achieve encapsulation and re-use them to make objects that look alike. However, factory functions have drawbacks and we often use classes instead.

How would you explain to a budding developer what the drawbacks of using factory functions are and why it is better to use classes instead?

### Response 3

## Prompt 4

Do some research on the history of when / how classes were introduced into JavaScript and share your findings. Your response should include:

- What version of JavaScript were classes introduced in and when did it come out?
- Why were classes introduced into JavaScript?

### Response 4

- `Classes` were introduced in ES6 version of JavaScript and it came out in June 2015. Along with classes this version came out with a few more syntax features.

  1.  Class syntax (`class`, `constructor`, `extends`, `super`)
  2.  Arrow functions (`=>`)
  3.  `let` and `const` for block-scoped variables
  4.  Template literals (backticks `Hello ${name}`)
  5.  Default parameters
  6.  Destructuring assignment
  7.  Promises
  8.  Modules (`import`/`export`)

- `Classes` were introduced to JavaScript to offer a more structured and intuitive approach to object-oriented programming (OOP), making the syntax cleaner, more readable, and developer-friendly.

Here is a code example before `classes` were introduced (using prototype & constructor functions):

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.greet = function () {
  console.log(`Hello, my name is ${this.name}.`);
};
```

This syntax works but it is not intuitive for developers coming from class based languages.

Here is a revised example using `Classes` in ES6:

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}.`);
  }
}
```

This is much cleaner syntax and resembles a traditional OOP languages.

`Classes` allow defining objects and dealing with inheritance much easier.
Here is an example of prototype-based inheritance before ES6:

```js
function Employee(name, age, jobTitle) {
  Person.call(this, name, age); // Call parent constructor
  this.jobTitle = jobTitle;
}

Employee.prototype = Object.create(Person.prototype);
Employee.prototype.constructor = Employee;

Employee.prototype.work = function () {
  console.log(`${this.name} is working as a ${this.jobTitle}.`);
};
```

Here is a better version using `Classes` with (`extends` & `super`)

```js
class Employee extends Person {
  constructor(name, age, jobTitle) {
    super(name, age); // Calls the parent class constructor
    this.jobTitle = jobTitle;
  }

  work() {
    console.log(`${this.name} is working as a ${this.jobTitle}.`);
  }
}
const emp1 = new Employee("Bob", 25, "Software Engineer");
emp1.greet(); // Inherited from Person class
emp1.work(); // Output: Bob is working as a Software Engineer.
```

This syntax is much easier to read and handle inheritance.

## Prompt 5

OOP can still be achieved in JavaScript without using the `class` keyword and instead using the "Constructor Functions" and the "Prototype Chain" (look them up!)

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.greet = function () {
  return `Hi, I'm ${this.name}, and I'm ${this.age} years old.`;
};

const alice = new Person("Alice", 30);
console.log(alice.greet());
```

Provide one point that advocates for the use of this syntax and then provide a counter-argument for the use of classes instead.

### Response 5
