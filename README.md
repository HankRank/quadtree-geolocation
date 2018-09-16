# Quadtree for geolocation

Quadtree is a tree data structure that has 4 "children", often called nodes, each of these nodes have 4 more nodes within and so on, until the specified granularity is achieved.



For optimization purpouse, the children are only created when necessary, for example, in the image below we can see the representation of the quadtree.

![Quadtree depth](https://poppicture-57876.firebaseapp.com/quadtree/quadtree-depth.png)

![Quadtree gif](https://poppicture-57876.firebaseapp.com/quadtree/quadtree-mouse.gif)

This structure is beautiful in so many ways, there's a lot of usages that can really improve applications. The most common usages are:

* Optimization of rendering on games 
* Dynamic lighthing effect on games
* Geolocation
* Image compression
* A.I. Path finding

For this example, we'll use the quadtree for optimizing Geolocation. Imagine that we have an app that shows the user other users around them, or pictures around them.

The traditional way would be comparing the distance between User A and B. Using latitude and longitude of both points, we could calculate the distance in degrees and then convert it to KMs or Miles. So far so good.

![Distance between User A and B](https://poppicture-57876.firebaseapp.com/quadtree/step1.png)

As we know, the formula to calculate the distance between two points is:

![Distance between points formula](https://poppicture-57876.firebaseapp.com/quadtree/dbtpformula.png)

The problem starts here, SQRT functions are CPU expensive, imagine that our backend would need to do this for each request against all users on the database. 


![Distance between User A and others](https://poppicture-57876.firebaseapp.com/quadtree/step2.png)


We could even add some filters to help, maybe compare only the same country, or city. Even so, it's not sustainable.
Fortunately, we can represent our planet in a 2D map, using latitude and longitude.


![World map in 2D latitude and longitude](http://cse.ssl.berkeley.edu/segwayEd/lessons/search_ice_snow/worldmapL.gif)


Longitude -180 to 180
Latitude -90 to 90

Great! Now we know that we can create a quadtree to represent the whole world. First we need to define the size of the deepest node/child, let's say the deepest node will have 100km * 100km. Then we'll add 1 million points of interest. To be able to show the insertion, i had to slow down the gif. 

![World Quadtree insertion gif](https://poppicture-57876.firebaseapp.com/quadtree/world-quadtree.gif)

Now, we are going to use the mouse pointer as the center of our search, the area is going to be 100km, therefore, any point of interest within 100km of the mouse pointer will be selected.

![World Quadtree insertion gif](https://poppicture-57876.firebaseapp.com/quadtree/world-quadtree-search.gif)

Using the example above, it does not take even a millisecond to get the search results. Running the same example with 10 million points we got the same results.

![World Quadtree insertion gif](https://poppicture-57876.firebaseapp.com/quadtree/world-quadtree-10kk-search.gif)

There's no limitation to the depth of a quadtree, we could set the size of the last node to 1km * 1km if we wanted to, that would save a lot of process power and time.
