JShare - Share your Node.js server side variables with your client side Javascript. 
===============


Usage:
------

First, you need to add the JShare middleware to your Express app **make sure to add it before the call to app.router**:

**app.js**

    var jshare = require('jshare');
    app.configure(function(){
	    app.use(jshare());
	    app.use(app.router);
	});

Next, you need to make a call out to the JShare helper method in your layout file:

**layout.jade** (or whatever other view engine you're using)

    !!!
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/style.css')
        !{includeJShare()}
      body!= body

And finally, in your routes file, you can now attach any variables to the Response:

**index.js**
    
    exports.index = function(req, res){
      res.jshare.person = {firstName : "Alex"};
      res.render('index', { title: 'Express' })
    };

Now, in your client-side javascript, all of your variables that you set on the server side, will be available to you:

**clientJS.js**

    alert(jshare.person.firstName);

Options:
------

When calling the `includeJShare()` function from within your layout, you can optionally pass in a `namespace` parameter. What that does is it prefaces the client side Javascript variables with your custom namespace as opposed to 'JShare':

**layout.jade**
   
    !{includeJShare('foo')}

**clientJS.js**

    alert(foo.person.name);