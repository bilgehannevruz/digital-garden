---
Created: 2024-03-01T21:52
URL: https://dev.to/codewithshahan/writing-clean-reusable-components-in-react-best-practices-2gka
---
[Cover image for Writing clean, reusable components in React (best practices)](https://media.dev.to/cdn-cgi/image/width=1000,height=420,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F1d0ipsf8vsu3jw2rxwzj.png)

[![](https://media.dev.to/cdn-cgi/image/width=1000,height=420,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F1d0ipsf8vsu3jw2rxwzj.png)](https://media.dev.to/cdn-cgi/image/width=1000,height=420,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F1d0ipsf8vsu3jw2rxwzj.png)

## 🔑 Key Concepts

What are reusable React components? You can think of them as building blocks.

They are independent pieces of code that can be reused throughout your website to save you time and effort.

They can be anything from simple buttons to complex forms.

**Why Use Reusable Components?**

As your website grows, you can easily add new features by combining existing components. This makes your code more scalable and adaptable.

You can use **your reusable piece of code in future projects** without writing it again from scratch.

## 🧩 How to Write Clean, Reusable React Components

Here are the _two most important_ things to keep in mind while writing clean reusable React components:

[Image of react reusable component](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fyuprsf67nntkgexmo92w.jpg)

[![](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fyuprsf67nntkgexmo92w.jpg)](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fyuprsf67nntkgexmo92w.jpg)

**1. 🩼Avoid Side Effects.** Don't put logic that interacts with external data (like making API calls) directly inside a reusable component. Instead, pass this logic as `props` to the component.

For example, if a button does more than just looking pretty, like fetching data from the internet, **it might not be reusable.**

I am not going to show you an example of this until you grasp the concept of passing props with best practices. Keep reading.

This is a reusable button component. But it lacks best practices. I will show you why in the example section.

```Plain
// This is a reusable button component (bad practice!)
const Button = () => {
  return (
    <button> Click Me </button>
  );
}
```

‍

**2. 🗃️ Use Props.** Props are arguments you pass to a component to customize its behavior and appearance. This allows you to use the same component for different purposes.

```Plain
// This is a button component that can change its color
const Button = ({ color }) => {
  return (
    <button style={{ backgroundColor: color }}> Click Here </button>
  );
}
```

This is still a bad practice because you have a fixed label called "Click Here". If you want to change the text on your button, let say - "Sign Up", then you would have to go back to the button component and make that change.

That means every time we want to use a different text, we'd have to go back and edit the code. In other words, it's no longer reusable.

**💪 Challenge:** So what's the solution?

You already have the answer. But if you don't, I am going to show you in the example section.

**🌴 Hint:** Think about how you might want to use the component in different situations and design it to be flexible and adaptable.

## 🍃Examples of Reusable React Components

Here are some common examples of reusable React components, along with some code examples to get you started:

**1. Buttons:** Basic buttons with different styles and functionalities.

```Plain
// Button component
import React from "react";

const Button = ({ color, label, onClick }) => {
  return (
    <button
      className={`padding-2 shadow-none hover:shadow background-light-${color} hover:background-dark-${color}`}
      onClick={onClick}
    >
      {label}
    </button>
  );
};

export default Button;

// Using the Button component
<Button color="blue" label="Click Here" onClick={() => console.log("Button clicked!")} />
```

As you can see, I did not write "Click Here" in the button component. I want to make my button reusable, and thus it doesn't know anything about custom styles or texts.

So, I passed them as props (e.g., color, label, onClick) to change them in the future without touching the original button components. Hope that makes it clear.

> **🪜Solution:** You need to pass EACH functionality as `props` in the reusable component - that's it.

**2. Navbars:** Navigation bars that provide consistent navigation across your website.

```Plain
// Navbar component
import React from "react";

const Navbar = ({ isLoggedIn }) => {
  return (
    <div className="navbar">
      <div className="navbar-container">
        <div className="navbar-logo">
          <img src={logo} alt="logo" />
        </div>
        <div className="navbar-links">
          <a href="/">Home</a>
          <a href="/about">About</a>
          <a href="/contact">Contact</a>
          {isLoggedIn ? (
            <a href="/profile">Profile</a>
          ) : (
            <a href="/login">Login</a>
          )}
        </div>
      </div>
    </div>
  );
};

export default Navbar;

// Using the Navbar component
<Navbar isLoggedIn={true} />
```

As you can see, I passed `<Navbar isLoggedIn={true} />`

This line utilizes the `Navbar` component and passes the `isLoggedIn` prop with a value of true, indicating the user is logged in. This will display the "Profile" link and hide the "Login" link.

Similar to the button component, the Navbar component is reusable and accepts props to customize its behavior. Perfect!

**3. Why API call in button component is a bad practice**

Now, you understand everything about reusable component in React.

Let's dig deeper by solving a complex problem.

Consider the scenario, where you have a button that does an API call. The code for the button component can be the following:

```Plain
import React from "react";
import doAPICall from "../api"

const SaveButton  = () => {
  return (
    <button
      onClick={() => {
        doAPICall();
      }}
    >
      Save
    </button>
  );
}

export default SaveButton
```

It is quite clear that you can’t reuse the above button in multiple places as this button component contains a side-effect (`doAPICall()`) inside it.

To make this component reusable, first, you will have to extract out the side-effect and pass that as a prop to the button component like the following:

```Plain
const App = () =>  {
  function doAPICall() {
    // Does an API call to save the current state of the app.
  }

  return (
    <div>
      <SaveButton onClick={doAPICall}/>
    </div>
  )
}
```

The button component will look like the following:

```Plain
const SaveButton  = ({
  onClick
}) => {
  return (
    <button
      onClick={onClick}
    >
      Save
    </button>
  );
}
```

As you can see, the above button can now be reused in all places where you want to save data on click of a button. The button can now be used like this in multiple places:

```Plain
const App = () =>  {
  function saveUser() {
    // Does an API call to save the user.
  }

  function saveProject() {
    // Does an API call to save the project.
  }

  return (
    <div>
      <SaveButton onClick={saveUser}/>
      <SaveButton onClick={saveProject}/>
    </div>
  )
}
```

You can also make the button component more reusable by using a prop to control the label like the following:

```Plain
const App = () =>  {
  function saveUser() {
    // Does an API call to save the user.
  }

  function saveProject() {
    // Does an API call to save the project.
  }

  return (
    <div>
      <SaveButton onClick={saveUser} label="Save user"  />
      <SaveButton onClick={saveProject} label="Save project" />
    </div>
  )
}
```

The button component will look like the following:

```Plain
const SaveButton  = ({
  onClick,
  label
}) => {
  return (
    <button
      onClick={onClick}
    >
      {label}
    </button>
  );
}

```

## 👏Conclusion

Congratulations! You've successfully learned how to build clean reusable React component with BEST practices.

Remember, **reusable components are the building blocks of robust React development**. By practicing reusable components, you can build cleaner, more efficient, and more maintainable React applications.

The more you practice, the better you'll become at identifying opportunities to use them in your projects!

**Read More:** [The Future of Frontend Development](https://dev.to/codewithshahan/the-future-of-frontend-development-1amd)

Thank you for taking the time to read this article. Keep learning and you can follow me on [𝕏](https://twitter.com/shahancd) for latest updates on programming and productivity.