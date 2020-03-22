# Login, Register

# Login

1. Study [useState with forms](https://www.youtube.com/watch?v=R7T5GQLxRD4)
1. Study [Using React Hooks To Create Awesome Forms](https://medium.com/@geeky_writer_/using-react-hooks-to-create-awesome-forms-6f846a4ce57)
1. Install [React Develper Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) to Chrome
1. Continue last exercise. Create a new branch with git.
1. Create files:
    * 'Login.js' and 'Logout.js' to 'views' 
    * 'LoginHooks.js' and 'RegisterHooks.js' to 'hooks' 
    * 'LoginForm.js' and 'RegisterForm.js' to 'components'
1. Login.js will hold LoginForm and RegisterForm components
    * Add the usual imports, component function and export to Login, LoginForm and RegisterForm
    * Login.js:
    ```jsx harmony
    import React from 'react';
    import LoginForm from '../components/LoginForm';
    import RegisterForm from '../components/RegisterForm';
    
    const Login = () => {
      return (
        <>
          <LoginForm/>
          <RegisterForm/>
        </>
      );
    };
    
    export default Login;
   ```
1. Change routing so that Login is the root ("/") instead of Home. Add also a new route for Home.
1. Add form to RegisterForm.js with username, password, email and full_name fields and submit button
    * Use 'Using React Hooks...' article as an example to handle form events. Instead of using 'CustomHooks.js' as filename, use 'RegisterHooks.js'
       * You need to do one change to useSignUpForm function:
        ```javascript
        // RegisterHooks.js:
        const [inputs, setInputs] = useState({
            username: '',
            password: '',
            email: '',
            full_name: '',
          });
        
        const handleSubmit = (event) => {
            if (event) {
              event.preventDefault();
            }
            callback(inputs);
          };
        ```
1. Do the same with LoginForm.
   * Instead of using 'CustomHooks.js' as filename for hooks, use 'LoginHooks.js'
   * Rename 'useSignUpForm' function in 'LoginHooks.js' to 'useLoginForm'
   * Make this change:
   ```javascript
   // LoginHooks.js:
   const [inputs, setInputs] = useState({
       username: '',
       password: '',
     });
   
   const handleSubmit = (event) => {
       if (event) {
         event.preventDefault();
       }
       callback(inputs);
     };
   ```
    
1. In APiHooks.js create functions 'register', 'login' and 'checkUserExists' with corresponding functionalities. Log the results of API fetches to console at this point.
    * Example 'register' function:
    ```javascript
    const register = async (inputs) => {
      const fetchOptions = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(inputs),
      };
      const response = await fetch(baseUrl + 'users', fetchOptions);
      const json = await response.json();
      console.log(json);
    };
    ```
    * RegisterForm.js: set APiHooks.js's 'register' function as a callback to to 'useSignupForm' and fill the registartion form in your browser. Check the log.
    * LoginForm.js: set APiHooks.js's 'login' function as a callback to to 'useLoginForm' and fill the login form in your browser. Check the log.
1. Add the final functionalities:
    * when logging in, save user data to [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage). Also [redirect](https://tylermcginnis.com/react-router-programmatically-navigate/) to 'Home'
    * display user's info (username, fullname and email) in Profile.js
    * if user has already logged in, redirect to 'Home' (autoredirect)
        * for this, save token to [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) when logging in. Then when the app starts, use [/users/user](http://media.mw.metropolia.fi/wbma/docs/#api-User-GetCurrentUser) endpoint to check if the token is valid
    * when registering  
        * login automatically after succesful registration
        * check if username already exists before trying to register
    * Logout.js: logout (clear localstorage, redirect to Home)
1. Study [conditional rendering](https://reactjs.org/docs/conditional-rendering.html)
    * when user is logged in, show Profile and Logout links in Nav. When user is logged out, hide Profile and Logout and show Login.

1. Extra: Save user data with [ContextAPI](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react) instead of localStroage (token is always stored to localStorage)

---

