class: center, middle

# AJAX + state

---

Study [Understanding and handling API requests](https://www.youtube.com/watch?v=2N9iqkWfjC8&list=PLDIXF8nb0VG1v4S-smVy7GV0MHsJ3PJiL&index=7) and [Using Hooks](https://www.youtube.com/watch?v=rEFYriigJ5A&list=PLDIXF8nb0VG1v4S-smVy7GV0MHsJ3PJiL&index=9)

Study [State Hook](https://reactjs.org/docs/hooks-state.html), [Effect Hook](https://reactjs.org/docs/hooks-effect.html) and this article

# Fetching data with AJAX, Task A

1. Continue last exercise. Create a new branch `http-a` with git and checkout it (`git checkout -b http-a`).
1. Remove picArray from App.js. Also from `<MediaTable>` and MediaTable.js' props.
1. Save [test.json](./assets/test.json) into 'public' folder of your project.
1. In MediaTable.js, use [fetch](https://ilkkamtk.github.io/SSSF-course/Slides/JS%20recap/W1-2-JavaScript-cheat.html) to load test.json
    - Add the new code to MediaTable function:
    ```javascript
    let picArray = [];
     const getMedia = async () => {
       const response = await fetch('test.json');
       const json = await response.json();
       console.log(json);
     };
   
     getMedia();
    ```
1. Why is the resulted page in your browser empty?
1. Save the loaded data to state and try to get the image list back.
   - convert `let picArray...` to state with `useState` -hook
   - set the value of `picArray` state to `json` 
   - what do you see in the console?
1. Prevent infinite loop with [useEffect](https://www.robinwieruch.de/react-hooks-fetch-data).
1. git add, commit & push to remote repository
1. Deploy project to your public_html 

---

# Fetching data with AJAX, Task B

1. Continue last exercise. Create a new git branch `http-b` and use it.
1. Modify the app so that you fetch the data from the media API instead of test.json
    - [Documentation](https://media-new.mw.metropolia.fi/wbma/docs/)
    - base url: https://media-new.mw.metropolia.fi/wbma/
    - Media files location: http://media-new.mw.metropolia.fi/wbma/uploads/
1. First log the data using ```console.log()```
    - Note that '/media' endpoint doesn't give you thumbnails. You need to do a nested request to '/media/:id' to get also thumbnails.
        - Study Promise.all [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) and [here](http://promise-nuggets.github.io/articles/14-map-in-parallel.html)
        - example: 
        ```javascript
        // 2nd fetch:
        Promise.all(array.map(item => {
            return fetch(url + item.id).
                then(response => {
                  return response.json();
                });
          })).then(items => {
            console.log(items);
            // save items to state
          });
        ```
1. Save the data to state and then print the data to the table
1. git add, commit & push to remote repository
1. Deploy project to your public_html 
