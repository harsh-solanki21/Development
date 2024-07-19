# Cookies vs Local Storage vs Session Storage

| Parameters         | Cookies          | Local Storage | Session Storage |
| ------------------ | ---------------- | ------------- | --------------- |
| Capacity           | 4kb              | 10mb          | 5mb             |
| Accessible from    | Any Window       | Any Window    | Same Tab        |
| Expires            | Manually         | Set Never     | On tab close    |
| Storage Location   | Browser & Server | Browser only  | Browser only    |
| Sent with requests | Yes              | No            | No              |

<br />

## Local Storage

- It persists until explicitly deleted. Changes made are saved and available for all current and future visits to the site.
- Use for long term use.
- Both key and value must be string.
- We can use the two JSON metods to store objects in localstorage:
  `JSON.stringify(object)` - converts object to JSON string
  `JSON.parse(string)` - converts string to object

<br />

- `getItem` - to get the data from the localStorage
- `setItem` - to set the data in the localStorage
- `removeItem` - to remove

```javascript
localStorage.setItem("name", "Harsh"); // set in key-value pair
localStorage.setItem("name", "Harsh21"); // updates the value
const data = localStorage.getItem("name"); // key to get data
localStorage.removeItem("name"); // key to remove data
localStorage.clear(); // to remove all the saved data
```

<br />

## Session Storage

- It exists only within the current browser tab. Another tab with same page will have a different storage.
- The data survives page refresh, but not closing/opsning tabs.
- Use when you need to store something that changes or something temporary.

<br />

- All the methods in session storage are same as local storage

```javascript
sessionStorage.setItem("key", "value");
sessionStorage.setItem("name", "Harsh Solanki"); // do setItem again to update data
let data = sessionStorage.getItem("key");
sessionStorage.removeItem("key");
sessionStorage.clear(); // to remove all the saved data
```

<br />

- Saving text between refreshes:
  The following example autosaves the contents of a text field and if browser is refreshed, restores the text field content so that no writing is lost.

```javascript
// Get the text field that we're going to track
let field = document.getElementById("field");

// See if we have an autosave value (this will only happen if the page is accidentally refreshed)
if (sessionStorage.getItem("autosave")) {
  // Restore the contents of the text field
  field.value = sessionStorage.getItem("autosave");
}

// Listen for changes in the text field
field.addeventListener("change", function () {
  // And save the results into the session storage object
  sessionStorage.setItem("autosave", field.value);
});
```

<br />

## Cookies

- Cookies can be used by web servers to identity and track users as they navigate different pages on a website, and to identify users returning to a website.

- An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to a user's web browser through request header . The browser may store the cookie and send it back to the same server with later requests.

```javascript
//  to set item
document.cookie = "name=harsh"; // to add cookie (won't replace the existing one)
document.cookie = "name=harsh21"; // to update the cookie as name key is already exists

// to set expiration date
document.cookie = "name=Harsh; expires=" + new Date(2022, 0, 1).toUTCString();
// new Date(yyyy, mm(0 based indexing), dd)
// new Date(2022, 0, 1) means Jan 1, 2022

// to set date to never expire
// just make year so far in the future like 9999

// to set other cookie
// make sure its a different name otherwise it will override the old value with the new one
document.cookie =
  "lastName=Solanki; expires=" + new Date(9999, 0, 1).toUTCString();
// cookie with last name and will never expire

// to see all the cookies
console.log(document.cookie);

// to encode and decode cookies (this way, the special characters are encoded)
// use of ; and = will affect the input. So use below methods in that case:
document.cookie = `${encodeUriComponent(key)}=${encodeUriComponent(value)}`;
decodeUriComponent("encoded key");

// Cookies have several options which can be provided after key=value to set call like this:
// This is a single cookie with multiple data
document.cookie =
  "user=harsh; path=/blog; expires=Tue, 21 May 2030 03:18:22 GMT";
```

<br />

- path option makes the cookie visible at `/blog`, `/blog/myblog`, etc. not on `/`
- expires sets the cookie expiration time.
