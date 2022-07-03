## Avoid Prop Drilling with React Context

In this blog post, let us understand what prop drilling is all about and how it can be avoided using React Context. 
Before proceeding, let us understand few basics.
### what exactly props are?🤔 
Props are short for properties and they are used to pass data between React components. 
When you work on a react application there is always a need to share data between components. The data passed in the form of <b>Props</b>.

In the below example, the Greeting component accepts 2 props to customize the greet message. 🙇

```
function Greeting({ greet, to }) {
  return <h1>{greet}, {to}!</h1>;
}
// Greeting Component
<Greeting greet="Welcome" to="User" />

// Final Output
<h1>Welcome, User!</h1>

``` 
But what if a Greeting component is several levels below the root component?  Prop data is being sent at almost every level due to requirements at the Greeting level. This is what leads to <b>Prop Drilling</b>💫

For Example, consider the below diagram

![Props_drilling.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631528349843/nHrm3ELEIx.png)

Consider Component App with user login details, it has to be passed down as a prop to the D component, E, and finally to the F component. This is what we call Prop Drilling or Threading. 🤯
> It would be nice to send data directly to the component instead of drilling at each component level. 
And this is where <b>Context comes into the picture.</b>

<hr style="margin:0,padding:0">
### Its React Context Time🌻

Wow, are these so overwhelming? Ok, just spare a few minutes I will try to explain the context as easily as possible.

React context allows us to pass down and use data in whatever component we need in our React app no matter how deep the component is without using props in short it resolves prop drilling. It is mainly used when we are dealing with user credentials or location-specific data.

### How to use Context.

React context can be used in 4 simple ways.

- Creating Context
- Providing the Context
- Wrap the context provider around your component tree.
- Consuming/Use the Context

#### 1: Creating Context 🦸 

```
const UserContext = React.createContext(defaultValue);
``` 
React comes with in-built function createContext(default) creates the context where defaultValue is optional

#### 2: Providing the context 🧠
```
const UserProvider = ({children}) => {
                      return (
                              <UserContext.Provider value={value}>
                               {children}
                              </UserContext.Provider>
                                 );
                       };
export {UserProvider,UserContext};
``` 
Context object Which we created in step 1 comes with a Provider React component that is used to provide context to the children components. It accepts a value prop that allow the user to change context values.

> !Important - All the child components that consume the context need to be wrapped inside the provider component.

#### 3: Wrap the context provider around your component tree 🎁 

We need to wrap our component with a context provider. Generally, we wrap our entire app component with a context provider in the index.js file.
 
```
import { UserProvider } from "./context";
ReactDOM.render(
    <UserProvider>
      <App />
    </UserProvider>,
  document.getElementById("root")
);
``` 
#### 4: Consume the context 🛍️

The cool thing about Context is that you really don't need to pass anything down to lower-level components with props as long as a provider for that context is positioned higher up the component tree. To consume the context we directly go to the component where we want to use it. And we use useContext hook to specify which context we want to use from UserContext

```
import { UserContext } from "./context";
const value = React.useContext(UserContext);
``` 

### Summary

1. Props allow us to pass data between React components.<br>
2. Prop drilling also termed threading is the code pattern you create when you need to get data from one component into another by passing props multiple times through other components.<br>
3. Context provides a way to pass data through the component tree without having to pass props down manually at every level.

And we are done, if you encounter any issues, you can check out the code sandbox link:
<a href="https://codesandbox.io/s/usecontext-06c7f?file=/src/context.js">useContext Demo</a>🔥<br>


If you enjoyed this article or found it helpful let us stay connected. You can find me on Twitter <a href="https://twitter.com/DeRaowl">Rahul Reddy</a>