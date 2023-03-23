# AJAX, Routing

---

# AJAX 2, Custom hooks
1. Continue last exercise. Create a new branch 'custom-hooks' with git.
2. Study [custom hooks](https://reactjs.org/docs/hooks-custom.html) and [this article](https://medium.com/@cwlsn/how-to-fetch-data-with-react-hooks-in-a-minute-e0f9a15a44d6) about using hooks to load data.
3. Create `hooks` folder and add there a new file `ApiHooks.js`.
4. The idea is to make hooks for each path in the [API](https://media.mw.metropolia.fi/wbma/docs/): login, users, media, etc.
5. Create a custom hook `useMedia` to ApiHooks.js and move fetch related functionalities from MediaTable.jsx:
   ```javascript
   // TODO: add necessary imports
   const baseUrl = 'http://media.mw.metropolia.fi/wbma/';
   const useMedia = () => {
     // TODO: move mediaArray state here
     // TODO: move loadMedia function here
     // TODO: move useEffect here
     return {mediaArray};
   };

   export {useMedia};
   ```
6. Modify MediaTable.jsx:
   ```javascript
   ...
    import {useMedia} from '../hooks/ApiHooks';
   
    const MediaTable = () => {
      const {mediaArray} = useAllMedia();
   
      console.log(mediaArray);
   
      return (
        <table>
          <tbody>
            {
              mediaArray.map((file, index) => <MediaRow file={file} key={index}/>)
            }
          </tbody>
        </table>
      );
    };
     ...
     ```
7. The app should work the same as before
8. git add, commit & push to remote repository
9. Deploy project to your public_html

# Routing 

Study [React Router Tutorial](https://www.youtube.com/watch?v=UjHT_NKR_gU)

1. Continue last exercise. Create a new branch 'navigation' with git.
2. Install [react-router-dom](https://reactrouter.com/en/main/start/tutorial) with npm
3. Goal is to make a navigation between three 'pages'
    * main menu has two links: 'Home' and 'Profile'
    * Each media file has 'view' link next to it. Clicking that should take to 'Single' and then display the selected media file
4. Create new folder 'views' to folder 'src'
5. Create new component 'views/Layout.jsx
    * content for Layout.jsx:
    ```jsx
    import {Outlet} from 'react-router-dom';
    
    const Layout = () => {
      return (
        <div>
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
          <main>
            <Outlet />
          </main>
        </div>
      );
    };
    
    export default Layout;
    ```
1. Create 'Home.jsx', 'Single.jsx' and 'Profile.jsx' to 'views'
    * Home.jsx will be the component that should show first when the app starts
    * Content for Home.jsx (note: `<> is shorthand for <React.Fragment>`)
    ```jsx harmony
     const Home = () => {
      return (
          <>
            <h1>Home</h1>
          </>
      );
    };
    
    export default Home;
    ```
 
    * Move the following jsx from App.jsx to Home.jsx
    ```jsx harmony
      <MediaTable/>
    ```
    * In Home.jsx replace it with
    ```jsx harmony
      <Home/>
    ``` 
    * The app should at this point work the same as before
1. Content for Profile.jsx:
    ```javascript
     const Profile = () => {
      return (
          <>
            <h1>Profile</h1>
          </>
      );
    };
    
    export default Profile;
    ```
1. Content for Single.jsx:
   ```javascript
   const Single = () => {
     const file = {}; // TODO in the next task: single media from props.location.state
   
     return (
       <>
         <h1>{file.title}</h1>
         <img src={mediaUrl + file.filename} alt={file.title}/>
       </>
     );
   };
   
   // TODO in the next task: add propType for location
   
   export default Single;

   ```
1. Study the video above and create routing described in bullet 2.
   
## Show single file & local state
  
1. In MediaRow.jsx make the 'view' link to open 'Single' component and send file as a state.
   - [useLocation](https://reactrouter.com/docs/en/v6/api#uselocation)
    ```jsx harmony
    // when navigating to single view, you need to send location state to define which media to show
    <Link to={'/example'} state={{fileObject}} />
    ```
1. In Single.jsx receive state from location prop and save it variable 'file' to display the title in `<h1>` element and file in `<img>` element.
1. To make links work also on remote server after building, add environment variables and basename attribute to Route:
   - add to App.jsx:`
    ```jsx harmony
    <Router basename={import.meta.env.BASE_URL}>
    ```
   - Modify `scripts` in package.json:
    ```json
      "build": "vite build --base=/~username/foldername/",
    ```
1. git add, commit & push to remote repository
1. Deploy project to your public_html
1. If you get 'Not found' error when you open e.g. `http://users.metropolia.fi/~username/foldername/profile`. To fix this, add `.htaccess` to your server to the same folder where you have `index.html` of your app:
   ```text
   RewriteEngine On
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteRule ^ index.html [QSA,L]
   ``` 

---

