# Login, Register

# Login

1. Study [useState with forms](https://www.youtube.com/watch?v=R7T5GQLxRD4)
1. Study [Using React Hooks To Create Awesome Forms](https://medium.com/@geeky_writer_/using-react-hooks-to-create-awesome-forms-6f846a4ce57)
1. Install [React Develper Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) to Chrome
1. Continue last exercise. Create a new branch with git.
1. Create files:
    * 'Login.js' and 'Logout.js' to 'views' 
    * 'FormHooks.js' to 'hooks' 
    * 'LoginForm.js' and 'RegisterForm.js' to 'components'
1. Login.js will hold LoginForm and RegisterForm components
    * Add the usual imports, component function and export to Login, LoginForm and RegisterForm
    * Login.js:
    ```jsx harmony
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
    * Use 'Using React Hooks...' article as an example to handle form events. Instead of using 'CustomHooks.js' as filename, use 'FormHooks.js' and useForm as the function name instead of useSignUpForm
       * You need to do changes to useForm function:
        ```javascript
        // FormHooks.js:
      const useForm = (callback, initState) => {
        const [inputs, setInputs] = useState(initState);
        
        const handleSubmit = (event) => {
            if (event) {
              event.preventDefault();
            }
            callback();
          };
        ```
1. Then in LoginForm make this change:
   ```javascript
   // LoginForm.js:
   const doLogin = () => {
     console.log(inputs);
     // TODO: add login functionalities here
   };
   
   const {inputs, handleInputChange, handleSubmit} = useForm(doLogin, {
    username: '',
    password: '',
   });

   ```
    
1. In APiHooks.js create functions 'register', 'login' and 'checkUserAvailable' with corresponding functionalities. Log the results of API fetches to console at this point.
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
    * RegisterForm.js: set APiHooks.js's 'register' function as a callback to to 'useForm' and fill the registartion form in your browser. Check the log.
    * LoginForm.js: set APiHooks.js's 'login' function as a callback to to 'useForm' and fill the login form in your browser. Check the log.
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
    * since updating the DOM requires a state change, user data needs to be saved into a state instead of localStorage. But which state?
    * save user data with [ContextAPI](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react) instead of localStroage (token is always stored to localStorage). With Context API you can create a global state which can be accessed from all components.
    * create new folder 'contexts' to 'src'. Create 'MediaContext.js' to 'contexts':
    ```javascript
    import React, {useState} from 'react';
    import PropTypes from 'prop-types';
    
    const MediaContext = React.createContext();
    
    const MediaProvider = ({children}) => {
      const [user, setUser] = useState(null);
      return (
        <MediaContext.Provider value={[user, setUser]}>
          {children}
        </MediaContext.Provider>
      );
    };
    
    MediaProvider.propTypes = {
      children: PropTypes.node,
    };
    
    
    export {MediaContext, MediaProvider};

    ```
    * add <MediaProvider> to app.js:
    ```jsx harmony
    <Router basename={process.env.PUBLIC_URL}>
          <MediaProvider>
            <Nav/>
            <Switch>
              <Route path="/" exact component={Home}/>
              <Route path="/login" component={Login}/>
              <Route path="/profile" component={Profile}/>
              <Route path={'/logout'} component={Logout}/>
              <Route path="/single/:id" component={Single}/>
            </Switch>
          </MediaProvider>
        </Router>
    ```
   * save user data to context:
   ```javascript
   const [user, setUser] = useContext(MediaContext);
   setUser(userdataFromApi); 
   ```
1. Add and commit changes to git, push to Github/GItLab. Build and upload to users.metropolia.fi
