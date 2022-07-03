## Execution Context in JavaScript

Hello Readers 👋

Let us learn how JavaScript works internally and how important the execution context is. Before proceeding, it is important to remember the following,

> Everything in JavaScript happens inside an Execution context

## So What is Execution Context? 

Execution context is a big container where the whole JavaScript program is executed.

*Execution context consists of 2 components,*

- Memory component: It is the place where all the variables and functions are stored as a key-value pair. It is also known as a <code>variable environment.</code>

- Code component: It is the place where code is executed one line at a time. It is also known as the <code>thread of execution.</code>

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626181203035/aZTaJgNkh.png)

> JavaScript is a "**synchronous single-thread**" language.

What does it really mean 🤔?

For a better understanding of the above statement, let's split it in two.
- Single-thread - JavaScript executes one line at a time.
- Synchronous  - JavaScript moves to the next line once the current line has finished executing.

## What happens when we execute a JavaScript program. 

When we execute the JS program global execution context is created. JavaScript isn't possible without execution context.

Let's understand it more clearly with an example.

```
var a = 5;
var b = 6;
function add(num1, num2) {
  return num1 + num2;
}
console.log(add(a, b));
console.log(add(1, 2));
``` 
*The creation of execution context takes place in two phases.*
- <h3>Memory Creation Phase:</h3> In this phase, JS will allocate memory to all the variables and functions. During the process of memory allocation to the variables, it stores a special value <code>***undefined***</code> as a placeholder. 
And in the case of a function, the entire function definition is copied.

![Global Execution.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626496580823/ZGAguZY02.png)

As shown in the above image, before executing JavaScript code, a global Execution Context is created. Variable a,b are assigned with placeholder <code>**Undefined**</code> and in case of add function, the entire code is copied.

- <h3>Code Execution Phase:</h3>
     In this phase, JS traverses the entire program line by line and replaces variables with their actual value. 

![brandbird (1).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626497205639/fsujTp05F.png)

As shown in the image above, variables a and b are stored with their real value as part of the global execution context. But here's something interesting. What happens when functions are involved?

Hola, a brand new execution context is created for the functions(Function Execution Context) 😀

![1 (2).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626498109877/86Z8h6SeS.png)

Function execution context will go through two execution phases. Again the memory is allocated to all variables with a special placeholder, the code is run line by line, and the actual value is assigned to the variables.
When the execution has ended, the function execution context is deleted.

This is how JavaScript works internally. But have you ever wondered how execution context is managed in JS?

<h3>What is Call Stack?</h3>

Let's look into the MDN definition.

> A call stack is a mechanism for an interpreter to keep track of its place in a script that calls multiple functions — what function is currently being run and what functions are called from within that function, etc.

Seems complicated? let's understand in an easy way.

As we discussed earlier before JS code is invoked an execution context is created, in the case of functions, the function execution context is created. Now let us assume we have 10000 lines of code with multiple nested functions. In this situation, it is difficult to keep track of currently executing functions.
 It is the place where <code>Call Stack</code> play an important role.

> Call Stack works on a LIFO basis.

Whenever a global execution context is created it is pushed to the top of the stack. And whenever a function is called, a function execution context is created and it is pushed to the top of the stack.

### **Example for Call Stack**

Let us consider the code which we defined at the beginning of the blog and let us see how the call stack works here.

Step-1: Before JS code is invoked, a Global execution context is created and it is pushed to the top of the stack.

Step-2: Now JS enters into code execution face and calls the add(a,b) function.

Step-3: Once the Execution of add(a,b) function is completed, it is popped out of the stack.

Step-4: Now add(1,2) function is invoked and a function execution context is created and it is pushed to the top of the stack.

Step-5: Once the Execution of add(1,2) function is completed, it is popped out of the stack.

Step 6: At last global execution context is popped out of call stack.

Overview of Call Stack creation,

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626502533447/gMiokeIOL.png)

### Conclusion

In Short, Whenever JS code is invoked a global execution context is created and a new execution context is created whenever the function is invoked.

Thank you for reading, if it was helpful feel free to share and ask questions in the comment sections below. Please check out my Twitter - <a href="https://twitter.com/DeRaowl">Rahul</a> and GitHub account <a href="https://github.com/DeRaowl">DeRaowl</a>

### Reference


- <a href="https://www.youtube.com/watch?v=ZvbzSrg0afE&t=5s">Akshay Saini</a>
- <a href="https://developer.mozilla.org/en-US/docs/Glossary/Call_stack">MDN</a>