
## Media Player

### Task: Create page for viewing single media files

1. Continue the previous exercise. Create a new git branch for these tasks.
1. Modify 'Single.js'. Features:
    - depending on file type use `<img>`, `<video>` or `<audio>` to show/play media file
        - <http://www.w3schools.com/tags/tag_video.asp>
        - <http://www.w3schools.com/tags/tag_audio.asp>
    - show also other data related to the media file:
        - title
        - description
        - user (to get username you need to request [User endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-User-GetUser) using media file's `user_id`)
        - optional: likes (request [Favourite endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-Favourite) on the media api)
            - add likes to image(s) with Postman or add 'like' button to Single.js
        - optional: show users who like the image

## Show user's files + update

1. Add new page 'MyFiles.js'
1. Add a button (for example to profile page) which opens MyFiles
1. Display a list of user's own files
    - very similar to Home
1. Add 'view', 'modify' and 'delete' buttons next to each file.
    - onClick example for delete:
    ```jsx harmony
     <button onClick={() => {
       deleteFile(file_id);
     }}>Delete</button>
    ```
    - important! not like this, because it's invoked immediately without click:
    ```jsx harmony
    <button onClick={ deleteFile(file_id) }>Delete</button>
    ```
1. Add corresponding functionality to the buttons
    - for 'view' use Single.js
    - delete does not need it's own page
    - modify is 90% same as UploadPage
        - make a copy of Upload.js and remove file chooser
        
### Extra. Study how to [protect routes](https://ui.dev/react-router-v5-protected-routes-authentication/)
### AJAX error handling
```javascript
const response = await fetch(url, options);
const json = await response.json();
if (json.error) {
   // if API response contains error message (use Postman to get further details)
   throw new Error(json.message + ': ' + json.error);
} else if (!response.ok) {
   // if API response does not contain error message, but there is some other error
   throw new Error('doFetch failed');
} else {
   // if all goes well
   return json;
}
```
