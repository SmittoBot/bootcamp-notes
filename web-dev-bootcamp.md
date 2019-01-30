## Web Development Bootcamp

### YelpCamp: Update and Destroy
* When sending a put request, need to append to URL and send as a post request:
```
action=".../edit?_method=PUT" method="POST"
```
* Mongoose has built-in functions for updating objects:
```
Campground.findByIdAndUpdate(req.params.id, req.body.campground, function(err, updatedCampground){
```
* When sending a delete request, append method to url:
```
action="/campgrounds/<%= campground._id %>?_method=DELETE
```
* Authentication: finding out if someone is who they say they are
* Authorization: figuring out what a known person is allowed to do
* When checking that a user own a campground, comaparing `foundCampground.euthor.id` and `req.user._id`, look identical but first is mongoose object while second is a string
* Instead need to use:
```
foundCampground.author.id.equals(req.user._id)
```
* To send a user back to their previous page:
```
res.redirect("back");
```
* To ensure that a current user exists before checking its attributes, or displaying a button only that user can see:
```
if(currentUser && campground.author.id.equals(currentUser._id)
```
* Since comments are a nested route, we need to define the id differently, ie
```
campgrounds/:id/comments/:comment_id/edit
```
* For form inputs, can use input with type submit instead of a button, such as:
```
<input type="submit" class="btn btn-xs btn-danger" value="Delete">
```
* Put middleware in between your route and req/res function when using express router:
```
router.put("/:comment_id", checkCommentOwnership, function(req, res){
```
* Refactor middleware and move shared methods into a single file, such as `middleware/index.js`
```
var middlewareObj = {};
middlewareObj.checkCampgroundOwnership = function(){...
module.exports = middlewareObj;
```
* Then require the middleware functions in other files with
```
var middleware = require("../middleware");
```
* If you require a directory, it will automatically require the contents of the `index.js` file in the directory

### YelpCamp: UI Improvements
* Flash messages: send a message to a user once, delete if refreshing or closed
* When searching for library tutorials and APIs, make sure to list version to get relevant links
* Use `connect-flash` package for flash messages:
```
flash = require("connect-flash");
app.use(flash());
```
* To send a flash message:
```
req.flash("error", "Please Login First!");
```
* To refer to the flash message from anywhere in the app:
```
res.locals.error = req.flash("error");
res.locals.success = req.flash("success");
```
* Bootstrap component for alerts provides styling and colors for success/info/alert/error
* In header file:
```
<% if(error && error.length > 0){ %>
  <div class="alert alert-danger" role="alert"><%= error %></div>
<% end %>
<% if(success && success.length > 0){ %>
  <div class="alert alert-success" role="alert"><%= success %></div>
<% end %>
```
* To flash the generated error message from a request:
```
req.flash("error", err.message);
```
* nodemon: alternative to running node app.js, listens for any file changes on server, and automatically restarts server when changes are saved:
```
nodemon app.js
```
* For centering vertically on page, can use view height, set to <50 so content isn't pushed down too far:
```
padding-top: 40vh;
```
* To add value form inputs:
```
<input class="form-control" type="number" name="campground[price]" value="<%= campground.price %>" min="0.01" step="0.01">
```
