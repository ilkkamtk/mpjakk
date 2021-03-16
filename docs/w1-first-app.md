# WBMA, First App

---
# Exercise 1: Setup your toolchain and a new React project

Study [Learn React JS ](https://www.youtube.com/watch?v=DLX62G4lc44&feature=youtu.be) from 0:00 to 1:58:15
   - especially 'Mapping Components'

### Exercise

**a.**

Study: [Create React App](https://github.com/facebook/create-react-app)

1. If needed, install code editor (+ extensions), git, npm
1. Use the `create-react-app` cli tool to generate an app skeleton `npx create-react-app my-app`
1. Test that app works; run it and open in browser
   - `cd my-app`
   - `npm start`
1. Create a remote git repository and push your app there
   - If you want to make public repository you can use GitHub
   - If you want to make private reposistory (only for metropolia users) use gitlab.metropolia.fi
   - After creating the repository initialize git and set up remote:
   ```text
   #If you use GitHub:
   
   git init
   git add .
   git commit -m "first commit"
   git remote add origin https://copy.address.here.git
   git push -u origin master
   
   #If you use GitLab:
   
   git config --global user.name "username"
   git config --global user.email "your.email@metropolia.fi"
   
   git init
   git remote add origin git@gitlab.metropolia.fi:username/nameOfTheRepo.git
   git add .
   git commit -m "Initial commit"
   git push -u origin master
   ```
   
   

**b.**  
1. Install ESlint to your project `npm i -D eslint eslint-plugin-react`
1. Initialize ESlint: `npm eslint --init` or `node eslint --init` or `./node_modules/.bin/eslint --init` or `node node_modules\eslint\bin\eslint.js --init`
    * Choose:
        1. To check syntax, find problems, and enforce code style
        1. JavaScript modules (import/export)
        1. React
        1. N
        1. Browser
        1. Use a popular style guide
        1. Google (or AirBnb if you prefer that)
        1. JavaScript
        1. Y
1. Enable ESLint in your WebStrom project (google instructions for VSCode)
   - [Instructions](https://www.jetbrains.com/help/webstorm/eslint.html)
      - [Importing code style](https://www.jetbrains.com/help/webstorm/eslint.html#ws_js_linters_eslint_import_code_style_from_eslint) is the most interesting part
1. Modify .eslintrc.js:
   ```JavaScript
    module.exports = {
      'parser': 'babel-eslint',
      'env': {
        'browser': true,
        'es2021': true,
      },
      'extends': [
        'google',
        'eslint:recommended',
        'plugin:react/recommended',
      ],
      'globals': {
        'Atomics': 'readonly',
        'SharedArrayBuffer': 'readonly',
      },
      'parserOptions': {
        'ecmaFeatures': {
          'jsx': true,
        },
        'ecmaVersion': 2018,
        'sourceType': 'module',
      },
      'plugins': [
        'react',
      ],
      'rules': {
        'react/jsx-uses-react': 'error',
        'react/jsx-uses-vars': 'error',
        'no-console': 0,
      },
      'settings': {
        'react': {
          'createClass': 'createReactClass', // Regex for Component Factory to use,
                                             // default to "createReactClass"
          'pragma': 'React',  // Pragma to use, default to "React"
          'version': 'detect', // React version. "detect" automatically picks the version you have installed.
                               // You can also use `16.0`, `16.3`, etc, if you want to override the detected value.
                               // default to latest and warns if missing
                               // It will default to "detect" in the future
          'flowVersion': '0.53', // Flow version
        },
        'propWrapperFunctions': [
          // The names of any function used to wrap propTypes, e.g. `forbidExtraProps`. If this isn't set, any propTypes wrapped in a function will be skipped.
          'forbidExtraProps',
          {'property': 'freeze', 'object': 'Object'},
          {'property': 'myFavoriteWrapper'},
        ],
        'linkComponents': [
          // Components used as alternatives to <a> for linking, eg. <Link to={ url } />
          'Hyperlink',
          {'name': 'Link', 'linkAttribute': 'to'},
        ],
      },
    };
   ```

1. If you want to lint a certain file: `npm eslint src/App.js` or `./node_modules/.bin/eslint src/App.js`.
1. Right click somewhere over .eslint.rc, choose 'Apply ESlint Code Style Rules'. Then you can correct code automatically with ctr-alt-l

**c.**

1. Develop your app further. Add a `<table>` etc. (and also css)  to the app skeleton so that the layout is similar to this: 

    ![View 1](./images/app1.png)

1. You can use placekitten.com or similar site for the images
1. Example html:
    ```html
    <table>
       <tbody>
           <tr>
               <td>
                   <img src="http://placekitten.com/160/160" alt="Title" />
                </td>
               <td>
                   <h3>Title</h3>
                   <p>Lorem ipsum dolor sit amet...</p>
               </td>
               <td>
                   <a href="http://">View</a>
               </td>
           </tr>
           <tr> etc...</tr>
       </tbody>
    </table>
    ```

**d.**

1. Develop your app further. Make the table dynamically by using this array:
    ```javascript
    // add to App.js after imports
      
    const picArray = [
          {
            'title': 'Title 1',
            'description': 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis sodales enim eget leo condimentum vulputate. Sed lacinia consectetur fermentum. Vestibulum lobortis purus id nisi mattis posuere. Praesent sagittis justo quis nibh ullamcorper, eget elementum lorem consectetur. Pellentesque eu consequat justo, eu sodales eros.',
            'thumbnails': {
              w160: 'http://placekitten.com/160/161',
            },
            'filename': 'http://placekitten.com/2048/1920',
          },
          {
    
            'title': 'Title 2',
            'description': 'Donec dignissim tincidunt nisl, non scelerisque massa pharetra ut. Sed vel velit ante. Aenean quis viverra magna. Praesent eget cursus urna. Ut rhoncus interdum dolor non tincidunt. Sed vehicula consequat facilisis. Pellentesque pulvinar sem nisl, ac vestibulum erat rhoncus id. Vestibulum tincidunt sapien eu ipsum tincidunt pulvinar. ',
            'thumbnails': {
              w160: 'http://placekitten.com/160/162',
            },
            'filename': 'http://placekitten.com/2041/1922',
          },
          {
            'title': 'Title 3',
            'description': 'Phasellus imperdiet nunc tincidunt molestie vestibulum. Donec dictum suscipit nibh. Sed vel velit ante. Aenean quis viverra magna. Praesent eget cursus urna. Ut rhoncus interdum dolor non tincidunt. Sed vehicula consequat facilisis. Pellentesque pulvinar sem nisl, ac vestibulum erat rhoncus id. ',
            'thumbnails': {
              w160: 'http://placekitten.com/160/163',
            },
            'filename': 'http://placekitten.com/2039/1920',
          },
        ];

    ```

1. Create components for table and tr.
    * name them as MediaTable and MediaRow
    * Hierarchy:
    ```text
    App
       -MediaTable
           -MediaRow 
    ```
    * you can put each comoponent (MediaTable, MediaRow) to one file or you can make own file for each component 
    * Pass picArray as props from App to MediaTable.
       * ESlint wants you to use [PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)
    * Iterate picArray in MediaTable to create multiple MediaRow components
       * picArray does not have id`s so you can use array.map's index parameter indstead:
       ```jsx harmony
        array.map((item, index) => {
          return <MediaRow key={index} someProp={item} />
        });
        ``` 
    
1. Develop your app further. Open 'filename' image when `<a>` is clicked.
1. (Optional) Develop your app further. Add more CSS. For example open 'filename' image to your self made modal.
1. git add, commit & push to remote repository
    * git add .
    * git commit -m 'viesti'
    * git push
1. Deploy project to your public_html (see below for instructions)

---

## Deploy React Project

1. Add following to package.json (e.g after devDependencies):
    ```json
     "homepage": "."
    ```
1. Run `npm build` or `npm run build`
1. Set deployment settings in WebStorm:
    ![Build conf0](./images/build_conf0.png)
    ![Build conf1](./images/build_conf1.png)
    ![Build conf2](./images/build_conf2.png)
1. Move build folder to your public_html
1. Test your app: `http://users.metropolia.fi/~username/somefolder`
1. Modify README.md. Change the link in `Open [http://localhost:3000](http://localhost:3000) to view it in the browser.` to point to the above link.
1. Add, commit and push to git
   ```text
   git add .
   git commit -m 'First app'
   git push
   ```
1. Make sure the link works in Github/GitLab
1. Submit to Oma
