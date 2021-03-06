imageflow-prototype
===================

A working responsive prototype of the new WordPress Image Flow - no integration with WordPress data.

[You can find the front end of the prototype here](http://flow.teamadesign.net/).

We'll be exploring the following scenarios:

1. [User Adds New Image To Post](http://flow.teamadesign.net/scenario1/) (edited) (ARIS) (not done)

2. [User Adds Existing Image to Post ](http://flow.teamadesign.net/scenario2/)(ARIS, ROY) (not done)

3. User Edits Existing Image and Adds It To Post

4. User Creates A Gallery

5. User Inserts Multiple Pieces Into Post

6. User Edits Image that is already inserted

<h2>How Does This Work?</h2>
The prototype is largely based on HTML/CSS/javascript, and is meant to be simple to work with. To facilitate some of the complex transitions and interactive bits we are using AngularJS to power the modal interaction.

If you want to participate, choose a scenario that is not claimed (no name behind it) and add your name to the scenario. If you'd rather work on something that is already claimed, get in touch with those folks in the Slack channel.

<h3>Basics</h3>
Clone the Angular branch down to your local machine. You'll see that there are a number of Scenario Folders. If there is a scenario that is similar to your choice and has had work finished, duplicate that folder and name it correctly. If none are similar, duplicate the 'Scenario1' folder.

Inside the folder you will see an index.html file, and a number of other pages. The index file is the main WordPress admin area and post editor that the prototype is launched from. You should not need to edit this file. The other pages are views that are presented in the modal. The first is the media-grid for choosing an image, open it up and you will see that it is largely straightforward HTML. You'll notice that at the top and bottom are <code>ng-include</code> tags. These are used to include a header and footer for the modal. You can see these files in the assets/js/templates folder. These are, again, straight-forward HTML files that are simply broken out to make things easier when we repeat functionality across the prototype. If you need to create a new header or footer, add them to the templates file and change the path in your view.

<h3>Angular.js</h3>
If you are unfamiliar with Angular you can simply make flat HTML views without the fancy javascript stuff. Once that is done, let the group know on Slack, submit a pull request and we will hammer out the interactions and provide feedback.

If you are familiar with Angular, or javascript take a look in the assets/js/app-base.js file. This is the heart of the prototype. At the most basic, you can see the routes starting around line 7. These allow Angular to load the correct content as we move through the prototype.

`
$routeProvider.when( '/mediaGrid', {  
	templateUrl: '01-media-grid.html',  
	controller: 'mediaGridCtrl',  
});
`

The first variable '/mediaGrid' is the path that the app will call. Your href would point to '#/mediaGrid' in this case. The second variable is the name of the file for that view, and the final variable is the name of the controller for that view. Immediately following the routes, are the controllers. These are exactly what they sound like: the controls for the related view. This is where you can write Angular code, or standard javascript, to effect your view. I strongly encourage you to look over the mediaGrid controller as it will give a good indication of how Angular works.  
  
There is a [w3schools](http://www.w3schools.com/angular/angular_directives.asp) with some of the basic AngularJS directives and functionality we will be using. 

<h4>ng-repeat</h4>
In each template loaded into the modal that has a grid of images, you will see  

`ng-repeat="image in images track by $index"`  

as an HTML attribute on the `grid-wrap` div. This is similar to a PHP (foreach/while) loop. We are looping through an `images` array and each individual object is defined as `image`. While we are looping we have access to anything defined in that object, but in our use case all we have is `image.src` which is the source path for the image.  
  
<h4>ng-click</h4>
This is similar to the onclick="" html attribute of days gone by. This runs a function in the Angular Controller that we define. For example the HTML template has something with `ng-click="imageSelect( $index, $event )"`and the controller has `$scope.imageSelect = function( index, event) {...}` defined. You don't always need to pass `$index` and `$event` into the function, however in this use case we needed it for additional logic.
  
<h4>Further reading</h4>
[Roy](http://www.roysivan.com/lets-build-wordpress-app-together-part-iii/#.VJMcSYrF_IA) is also blogging about his build of an open source AngularJS app built with WP. It has some AngularJS tutorials and overview concepts. You can find his blog entries related to the project at [ttp://www.roysivan.com/category/wordpress/building-an-app-with-wordpress/](http://www.roysivan.com/category/wordpress/building-an-app-with-wordpress/)


<h3>Images</h3>
All images that are used in the prototype are in the img folder in the root, and are delivered to the app via data.json in the assets/js folder.