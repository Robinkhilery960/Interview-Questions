# Interview Questions
## What is express ?
## What are middleware functions and How to use them ?
Express is actually a series of middleware function calls 
middleware functions are those function which  have access of request object , response object , and next middleware function in request response cycle> If you are using a middleware function  and your middleware function is not ending the request response cycle then pou have to call `next ` to pass the control to the next middleware or to response. If you will not do that then your  request will be left hanging 
### Types of Middleware:
### 1. Application level middleware :

You can bind these application level middleware using `app.use()` and  `app.METHOD() `where METHOD function HTTP method of the request that middleware function handle   

`app.use(middlewareFunction)`- this middleware function will be executed every time the app receive a request because no mount path is provided here 


`app.use('/user/:id',middlewareFunction)`- here a middleware function is mounted on a specific path so the function will execute for any HTTP request on  /user/:id path. 


`app.get('/user/:id',middlewareFunction)`- here a middleware function will execute only when  you receive a get request on this path 


`app.use(path,middlewareFunction1,middlewareFunction2)` and 
`app.use(path,[middlewareFunction1,middlewareFunction2])`- here both the middleware function will be called for every request on this path (remember that you have to mention next in both the middlewareFunction1 and middlewareFunction2)

Route handlers enable you to define multiple routes for a path. The example below defines two routes for GET requests to the /user/:id path. The second route will not cause any problems, but it will never get called because the first route ends the request-response cycle.
````javascript
app.get('/user/:id', (req, res, next) => {
  console.log('ID:', req.params.id)
  next()
}, (req, res, next) => {
  res.send('User Info')
})

// handler for the /user/:id path, which prints the user ID
app.get('/user/:id', (req, res, next) => {
  res.send(req.params.id)
})
````
To skip the rest of the middleware functions from a router middleware stack, call next('route') to pass control to the next route. NOTE: next('route') will work only in middleware functions that were loaded by using the app.METHOD() or router.METHOD() functions.
````javascript
app.get('/user/:id', (req, res, next) => {
  // if the user ID is 0, skip to the next route
  if (req.params.id === '0') next('route')
  // otherwise pass the control to the next middleware function in this stack
  else next()
}, (req, res, next) => {
  // send a regular response
  res.send('regular')
})

// handler for the /user/:id path, which sends a special response
app.get('/user/:id', (req, res, next) => {
  res.send('special')
})
````
### 2. Router-level middleware :
Router middleware works in the same way the application router works but they are bind to the instance of `express.Router()` that is router object.
You can load them using router.use() or router.METHOD().
You have to mount the router in your app like `app.use("/",router)` or `app.use(router)` .
### 3. Error-handling middleware:
error-handling middleware always takes four arguments. You must provide four arguments to identify it as an error-handling middleware function. Even if you don’t need to use the next object, you must specify it to maintain the signature. Otherwise, the next object will be interpreted as regular middleware and will fail to handle errors.
````javascript
app.use((err, req, res, next) => {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
````
### 4. Built-in middleware:
Express has the following built-in middleware functions:

express.static serves static assets such as HTML files, images, and so on.
express.json parses incoming requests with JSON payloads.  
express.urlencoded parses incoming requests with URL-encoded payloads. 

### 5. Third-party middleware:
You can use third party middleware to enhance express functionality  

##  How to use template engine with express? 
### What are Template Engines  ? 
Template engine that are mostly used for server side application. Template engine helps you to load static template file into your application.
At run time 2 things happen :
1. Your variable get replaced by actual value 
2. Your template code is converted into a HTML code 
### How to render the template files in express js :

Generator have created an  app for you and  some of the application setting properties are  already set with default values  so  you have to change them - 
1. views property- this is actually a directory where the template files are located so its default value is  `process.cwd() + '/views'` you can change it if you want  or you can keep it as it is.
2. view engine-  this is the template engine you want to use and its default is not defined you can set this property like this `app.set("view engine","ejs") `

 now install using npm install your view engine name 

` res.render(view, object,callback)`-  a method used to render a view and send that html string to client 
parameter-

1. `view-` is a string that is a path of view file to render - this path could absolute ot relative to view setting- if view does not contain file extension - then view engine setting determines the file extension and if path does contain the file extension then express will load the module for that specific template engine  via require and render it using loaded modules __express function ,so actually render method call this loaded modules' __express function that is actually rendering it 
2. `an object` - whose properties will behave as local variable to that view 
3. `callback function `  
Note- view argument perform file system operation like reading a file from your disk and evaluating node.js modules  so for security reasons should not contain input from  the end user 

````javascript
app.get('/', (req, res) => {
  res.render('index', { title: 'Hey', message: 'Hello there!' })
})
````

### Developing template engines for Express:
You can even develope your own view engine if you want using `express.engine()`
[See Here](https://expressjs.com/en/advanced/developing-template-engines.html) 

## express.Router(options):
The top-level express object has a Router() method that creates a new router object. 
Parameter:an object whose property defines behavior of this router object :

1. caseSensitive:/Foo and /foo will be treated same by the router - by default disabled

2.  mergeParams: persevere parents req.params value -m by default false
3. strict - /foo and /foo/ are treated as same by the router 

you can add middleware and HTTP methods routes to router object just like an application 

`router object`-
you can think of this a s an  mini application that is able to perform middler and routing functions 

router is itself behave as an middleware so you can use it as argument to the app.use()   or argument to the other routers use method 

````javascript
// created a router object 
const router=express.Router() 
````

`router.use(middlewareFunction) `or `router.use("/",callbackFunction)`- this middleware function will be executed every time the app receive a request because no mount path is provided here 

`router.use('/user/:id',middlewareFunction)`- here a middleware function is mounted on a specific path so the function will execute for any HTTP request on  /user/:id path. 


`router.get('/user/:id',middlewareFunction)`- here a middleware function will execute only when  you receive a get request on this path 


`router.use(path,middlewareFunction1,middlewareFunction2)` and 
`router.use(path,[middlewareFunction1,middlewareFunction2])`- here both the middleware function will be called for every request on this path (remember that you have to mention next in both the middlewareFunction1 and middlewareFunction2)

### Methods:
1. `router.all()`: this method is same like router.METHOD() except that it matches to all the HTTP  methods
2. [`router.METHOD`](https://expressjs.com/en/4x/api.html#router.METHOD)
3. [`router.param()`](https://expressjs.com/en/4x/api.html#router.param)
4. [`router.router()`](https://expressjs.com/en/4x/api.html#router.route)
5. [`router.use`](https://expressjs.com/en/4x/api.html#router.use)
