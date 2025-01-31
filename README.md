# Cross Domain Cookie/LocalStorage Sharing using JavaScript

This will help to cross domain sharing resources like login cookies data or local storage data between two subdomain or domain.

![pub-sub-pattern](https://user-images.githubusercontent.com/3996105/96174333-cd371a80-0f46-11eb-83b6-b6d1731e430f.png)
## Installation
Not required
  
## Usage

Just fork code or copy reference code block and use in your html or Javascript files.

Consider we have two domain example.com and example2.com.

**Step1** : Add postCrossDomainMessage function in landing page like index.html
www.example.com/index.html 
```
function postCrossDomainMessage(msg) {
  var win = document.getElementById('ifr').contentWindow;
  win.postMessage(msg, "https://example.com/");
}
var postMsg = {"login": "user"}; // this is just example
postCrossDomainMessage(postMsg);
```
**Step2**: Add iframe tag in landing page where everywhere reflected. For Angular/React you can add it in index.html

```
<iframe style="display:none;" src="http://example.com/getlocalstorage.html" id="ifr"></iframe>
```
**Step3**: On recipient domain www.example2.com create getlocalstorage.html file and put this code 👇🏻 in file getlocalstorage.html

```
var PERMITTED_DOMAIN = "http://example.com";
/**
 * Receiving message from other domain
 */
window.addEventListener('message', function(event) {
    if (event.origin === PERMITTED_DOMAIN) {
        //var msg = JSON.parse(event.data);
        // var msgKey = Object.keys(msg)[0];
        if (event.data) {
            localStorage.setItem("localstorage", event.data);
        } else {
            localStorage.removeItem("localstorage");
        }
    }

}); 
```

## Examples 
- Cookie/localstorage sharing in angular apps (https://github.com/aviboy2006/cookie-or-localstorage-sharing-in-angular-apps) 

## Session delivered so far 
[![https://www.youtube.com/watch?v=4zfDyGD1Brk](https://www.avinashdalvi.com/assets/img/jsfriend-session-banner.png)](https://www.youtube.com/watch?v=4zfDyGD1Brk)
[![https://www.youtube.com/watch?v=5pJd0apGHTk](https://user-images.githubusercontent.com/3996105/138595946-60ae09ab-a00a-4bbf-ae8a-c91db9c98436.jpeg)](https://www.youtube.com/watch?v=5pJd0apGHTk)



## Reference Blog
https://www.internetkatta.com/share-cookies-or-local-storage-data-between-cross-domain

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](https://choosealicense.com/licenses/mit/)
