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
* To ensure that a current user exists before checking its attributes:
```
if(currentUser && campground.author.id.equals(currentUser._id)
```
Since comments are a nested route, we need to define the id differently, ie
```
campgrounds/:id/comments/:comment_id/edit
```

