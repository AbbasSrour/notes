## Cookie Creation
### Client 
Cookies can be created using on the client side using `document.cookie`.
```ts
document.cookie =["key=data"]
````
### Server
Cookies can be created on the backend site using the set-cookie header
```ts
app.get("/", (req,res)=>{
	res.setHeader("set-cookie", ["key=value; ..."]);
})
```

## Cookie Properties
Cookies are sent with every http request, but to only the domains that the cookie is assigned to.
### Cookie Scope
#### Domain
Cookies can be configured to be assigned to multiple domains, thus sent with every http request to the assigned domains.
#### Path
Cookies can also be configured to only be sent to a specific path in the domain.

### Cookie Age And Expiration
Cookies can have a time limit for existing and will expire after a certain age limit specified in the cookie body.
```js
document.cookie="key=data; max-age=<x>min"
```  

### Same Site
When going from one site to another through a link on the first the cookies from the first site will go to the server of the second one. Setting the `same-site` header in the cookie to _strict_, the cookie will only be sent from the same site. Using the *lax* value will allow the cookie to be sent from the first one to the second.
```ts
document.cookie="key=data; same-site=strict"
```

## Cookie types
### Session Cookie
A session cookie is a cookie that doesn't have a max age or expiry, when the browser is deleted the cookie is essentially deleted.
### Permanent Cookie
A permanent cookie is a cookie that has a max age or expiry header, where if the browser is closed the cookie is not deleted.
### HttpOnly Cookie
HttpOnly cookies are cookies that  can only be set by the browser and the browser can't read them for security concerns.
### Secure Cookies
Secure cookies are cookies that can only be sent through an https connection.
### Third Party Cookies
Third-party cookies are named as such because **they come from a website other than the one a user is currently on** -- a third party in other words.
### Zombie Cookies
Zombie cookies are cookies that even if they are deleted they will be recreated with the same value. What happens is that the backend server will save some information like *etags* that came with the http request that the server response created the cookie for and if the cookie gets deleted on the client side the backend will recreate the same cookie using the information it collected about the user and linked to him/her from the initial http request. 

## Cookie Security
### Cookie Stealing 
Cookie stealing is done through a malicious js script that reads the file or files in the client file system that store the cookies, and sends them back to the server.
### Cross Site Request Forgery
When going from one site to another through a link on the first the cookies from the first site will go to the server of the second one
