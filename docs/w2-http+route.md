class: center, middle

# AJAX, Routing

## 2/2019

---

# HTTP 2

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
1. In App.js use getAllMedia in componentDidMount-hook to add images to state and display the data in table the same as last exercise.

# Routing

1. Create folder 'views' to folder 'src'
1. Create 'Front.js' to 'views'
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

---

