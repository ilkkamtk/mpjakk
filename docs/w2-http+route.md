class: center, middle

# AJAX, Routing

## 2/2019

---

# AJAX 2, Move reusable functions to a separate file

1. Continue last exercise. Create a new branch with git.
1. Create new folder 'utils' to 'src' folder
1. In the 'utils' folder create a new file 'MediaAPI.js'
1. In 'MediaAPI.js' make function getAllMedia and [export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) it.
    - getAllMedia should fetch all media files and their thumbnails from MediaAPI (just like last exercise)
    * example: 
    ```javascript
    ...
    const getAllMedia = () => {    
     return fetch(apiUrl).then(param => {
     ...then(someParam => {
           return Promise.all(someParam.map(item => {
             return fetch(...
             ...
       }
    }
    ...
    export {getAllMedia}
    ```
1. In App.js use getAllMedia in componentDidMount-hook to add images to state and display the data in table the same way as last exercise.
    - when using webStorm MediaAPI.js should be auto imported. If not, import it manually.

# Routing 

Study [React crash course](https://www.youtube.com/watch?v=sBws8MSXN7A) from 1:15:48  to 1:25:44

1. Create new component 'Nav.js' (to components folder)
    * content for Nav.js:
    ```javascript
    import React from 'react';
    
    const Nav = () => {
      return (
          <nav>
            <ul>
              <li>
                Home
              </li>
              <li>
                Profile
              </li>
            </ul>
          </nav>
      );
    };
    
    export default Nav;
    ```
1. Add Nav-component to App.js so that you can see it above Table component in browser
1. Create folder 'views' to folder 'src'
1. Create 'Front.js', 'Single.js' and 'Profile.js' to 'views'
    * Front.js will be the component that should show first when the app starts
    * Move the following jsx from App.js to Front.js
    ```jsx harmony
      <Table picArray={this.state.picArray}/>
    ```
    * Replace it with
    ```jsx harmony
      <Front picArray={this.state.picArray} />
    ``` 
    * In Front.js, make the moved code to use props instead of state.
    * The app should now work the same as before
1. Content for Profile.js (this is a [function component](https://reactjs.org/docs/components-and-props.html#function-and-class-components)):
    ```javascript
    import React from 'react';
    
    const Profile = (props) => {
      return (
          <div>
            <h1>Profile</h1>
          </div>
      );
    };
    
    export default Profile;
    ```
1. Content for Single.js (this is a [class component](https://reactjs.org/docs/components-and-props.html#function-and-class-components)):
   ```javascript
   import React, {Component} from 'react';
   import PropTypes from 'prop-types';
   
   class Single extends Component {
     mediaUrl = 'http://media.mw.metropolia.fi/wbma/uploads/';
     state = {
       file: {
         filename: 'b2db3cce51674aba84d9476a545c5cc4.jpg',
         title: 'Test',
       },
     };   
   
     render() {
       return (
           <React.Fragment>
             <h1>{this.state.file.title}</h1>
             <img src={this.mediaUrl + this.state.file.filename}
                  alt={this.state.file.title}/>
           </React.Fragment>
       );
     }   
   }
   
   Single.propTypes = {
     match: PropTypes.object,
   };
   
   export default Single;
   ```
1. 
    
1. In 'mediaAPI.js' make function getSingleMedia and [export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) it.
    - getSingleMedia should fetch one media file with thumbnails from MediaAPI (just like last exercise)
    * example: 
    ```javascript
    ...
    const getAllMedia = () => {    
     return fetch(apiUrl).then(param => {
     ...then(someParam => {
           return Promise.all(someParam.map(item => {
             return fetch(...
             ...
       }
    }
    ...
    export {getAllMedia}
    ```
1. In App.js use getAllMedia in componentDidMount-hook to add images to state and display the data in table the same as last exercise.
1. git add, commit & push to remote repository
1. Deploy project to your public_html 

---

