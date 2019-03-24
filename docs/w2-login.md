# Login, Register

## 2/2019

# Login

1. Install [React Develper Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) to Chrome
1. Create 'Login.js', to 'views'
    * This will be the login and register page
    * Make it to be a class component
    * Add two forms:
        * Login form with username and password fields and submit button
        * Register form with username, password, email and full name fields and submit button
        * Add local state to Login.js
        ```javascript
        state = {
            username: '',
            password: '',
            email: '',
            full_name: '',
          };
        ````
    * When login or register form is submitted, add values from corresponding form fields to local state 
    

1. In MediaApi.js create methods 'register', 'login' and 'checkIfUserExists' with corresponding functionalities
 - Login.js: call MediaApi.js's functions to login user and save user's token to App.js's state
    - when logged in, user is redirected to 'home'
    - if user has already logged in redirect to 'home' (autoredirect)
- 'register'-page: call media API to create new user 
    - login automatically after registering
    - check if username already exists before trying to register
- [Forms with ngModel](https://ionicframework.com/docs/v3/developer-resources/forms/)
- 'logout'-page: logout (clear localstorage, update loggedIn status in media provider)
    - Use a [lifecycle event](https://blog.ionicframework.com/navigating-lifecycle-events/) for automatic method calls
- Use [show]-attribute to show/hide login/logout buttons in tab-navigation according to user's login status


---

