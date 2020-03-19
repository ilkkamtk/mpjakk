# AJAX, Routing

---

# AJAX 2, Custom hooks

1. Continue last exercise. Create a new branch with git.
1. Study [custom hooks](https://reactjs.org/docs/hooks-custom.html) and [this article](https://medium.com/@cwlsn/how-to-fetch-data-with-react-hooks-in-a-minute-e0f9a15a44d6) about using hooks to load data.
1. Create new folder 'hooks' to 'src' folder
1. In the 'hooks' folder create a new file 'MediaHooks.js'
1. In 'MediaHooks.js' make function useAllMedia and [export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) it.
    - use 'hooks.js' in the article above as an example
       - rename useFetch(url) to useAllMedia
       - fetchUrl should behave like loadMedia function from previous task
       - you can remove the loading state. Instead of `return [data, loading]` you can just `return data`; 
    - useAllMedia should fetch all media files and their thumbnails from MediaAPI (just like last exercise)
    - modify MediaTable.js to use 'useAllMedia' function:
    ```javascript
    ...
   import {useAllMedia} from '../hooks/ApiHooks';
   
   const MediaTable = () => {
     const picArray = useAllMedia();
   
     console.log(picArray);
   
     return (
       <table>
         <tbody>
           {
             picArray.map((file, index) => <MediaRow file={file} key={index}/>)
           }
         </tbody>
       </table>
     );
   };
    ...
    ```

# Routing 

Study [React Router Tutorial](https://www.youtube.com/watch?v=Law7wfdg_ls)

1. Install [react-router-dom](https://reacttraining.com/react-router/web/guides/quick-start) with npm
1. Goal is to make a navigation between three 'pages'
    * main menu has two links: 'Home' and 'Profile'
    * Each media file has 'view' link next to it. Clicking that should take to 'Single' and then display the selected media file
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
1. Add Nav-component to App.js so that you can see it above MediaTable component in browser
1. Create new folder 'views' to folder 'src'
1. Create 'Home.js', 'Single.js' and 'Profile.js' to 'views'
    * Home.js will be the component that should show first when the app starts
    * Content for Home.js (note: `<> is shorthand for <React.Fragment>`)
    ```jsx harmony
    import React from 'react';
    
    const Home = (props) => {
      return (
          <>
            <h1>Home</h1>
          </>
      );
    };
    
    export default Home;
    ```
 
    * Move the following jsx from App.js to Home.js
    ```jsx harmony
      <MediaTable/>
    ```
    * Replace it with
    ```jsx harmony
      <Home/>
    ``` 
    * The app should at this point work the same as before
1. Content for Profile.js:
    ```javascript
    import React from 'react';
    
    const Profile = (props) => {
      return (
          <>
            <h1>Profile</h1>
          </>
      );
    };
    
    export default Profile;
    ```
1. Content for Single.js:
   ```javascript
   import React from 'react';
   
   const mediaUrl = 'http://media.mw.metropolia.fi/wbma/uploads/';
        
   
   const Single = () => {
     const file = {}; // TODO: fetch single media based on id from path parameter
   
     return (
       <React.Fragment>
         <h1>{file.title}</h1>
         <img src={mediaUrl + file.filename} alt={file.title}/>
       </React.Fragment>
     );
   };
   
   // TODO: add propTypes
   
   export default Single;

   ```
1. Study the video above and create routing described in bullet 2.
    ```jsx harmony
    // when navigating to single view, you need to send id parameter to define which media to show
    <Route path="/example/:id" component={Example} />
    ```
   
## Show single file & local state
  
1. In 'ApiHooks.js' make function useSingleMedia and [export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) it.
    - useSingleMedia should fetch one media file from MediaAPI based on id
    * example: 
    ```javascript
    ...
    const useSingleMedia = (id) => {
      const [data, setData] = useState([]);
      // TODO: fetch data from api
    
     // TODO: useEffect
    
      return data;
    };
    ...
    ```
1. In MediaRow.js make the 'view' link to open 'Single' component and send file_id as a parameter.

1. Study [react-router-dom url parameters](https://tylermcginnis.com/react-router-url-parameters/) to get file_id to Single.js
1. In Single.js receive the file_id parameter and save the result of useSingleMedia to variable 'file' to display the title in `<h1>` element and file in `<img>` element.
1. To make links work also on remote server after building, add environment variables and basename attribute to Route:
   - add `.env` to project root. Content: `PUBLIC_URL='/~username/foldername'`
   - add `.env.dvelopment` to project root. Content: `PUBLIC_URL='/'`
   - add to App.js:
    ```jsx harmony
    <Router basename={process.env.PUBLIC_URL}>
    ```
1. git add, commit & push to remote repository
1. Deploy project to your public_html 

---

