class: center, middle

# AJAX + state

---

Study [Understanding and handling API requests](https://www.youtube.com/watch?v=2N9iqkWfjC8&list=PLDIXF8nb0VG1v4S-smVy7GV0MHsJ3PJiL&index=7) and [Using Hooks](https://www.youtube.com/watch?v=rEFYriigJ5A&list=PLDIXF8nb0VG1v4S-smVy7GV0MHsJ3PJiL&index=9)

Study [State Hook](https://reactjs.org/docs/hooks-state.html), [What are effects](https://beta.reactjs.org/learn/synchronizing-with-effects) and [Effect Hook](https://reactjs.org/docs/hooks-effect.html)

# Fetching data with AJAX, Task A

1. Continue last exercise. Create a new branch `http-a` with git and checkout it (`git checkout -b http-a`).
2. Remove mediaArray from App.js. Also from `<MediaTable>` and MediaTable.js' props.
3. Save [test.json](./assets/test.json) into 'public' folder of your project.
4. In MediaTable.js, use [fetch](https://ilkkamtk.github.io/SSSF-course/Slides/JS%20recap/W1-2-JavaScript-cheat.html) to load test.json
    - Add the new code to MediaTable function:
    ```javascript
    let mediaArray = [];
     const getMedia = async () => {
       const response = await fetch('test.json');
       const json = await response.json();
       console.log(json);
     };
   
     getMedia();
    ```
5. Why is the resulted page in your browser empty?
6. Save the loaded data to state and try to get the image list back.
   - convert `let mediaArray...` to state with `useState` -hook
   - set the value of `mediaArray` state to `json` 
   - what do you see in the console?
7. Prevent infinite loop with [useEffect](https://www.robinwieruch.de/react-hooks-fetch-data).
8. Use [try/catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) to catch possible errors from promises.
9. Deploy project to your public_html 
10. git add, commit & push to remote repository

---

# Fetching data with AJAX, Task B

1. Continue last exercise. Create a new git branch `http-b` and use it.
2. Modify the app so that you fetch the data from the media API instead of test.json
    - [Documentation](https://media.mw.metropolia.fi/wbma/docs/)
    - base url: https://media.mw.metropolia.fi/wbma/
    - Media files location: http://media.mw.metropolia.fi/wbma/uploads/
3. Modify getMedia function to load the data from the '/media' endpoint of the API.
4. First log the data using ```console.log()```
    - Note that '/media' endpoint doesn't give you thumbnails. You need to do a nested request to '/media/:id' to get also thumbnails.
        - Study Promise.all [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) and [here](http://promise-nuggets.github.io/articles/14-map-in-parallel.html)
        - example: 
        ```javascript
        // 2nd fetch:
        Promise.all(array.map(async (item) => {
          const response =  await fetch(url + item.id);
          const json = await response.json();
          return json;
        }));
        ```
5. Save the data to state and then print the data to the table

### Submit
1. Run `npm build` or `npm run build`
2. Move build folder to your public_html
3. Test your app: `http://users.metropolia.fi/~username/somefolder`
4. Modify README.md. Change the link in `Open [X](X) to view it in the browser.` to point to the above link.
5. git add, commit & push to remote repository
