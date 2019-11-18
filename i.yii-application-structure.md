Yii-Application-Structure-Overview


Yii application are organized according to the ***model-view-controller(MVC)*** architectural pattern.

`Models` represent data, business logic and rules;

`Views` are output representation of models;

and `controllers` take input and convert it tom command for ***models*** and ***views***.



Besides MVC, Yii application also have the following entities:

	- entry scripts: they are PHP scripts that are directly accessible by end users. They are responsible for starting a request handling cycle.
	
	- applications: they are globally accessible objects that manage application components and coordinate them to fulfill requests.
	
	- application components:  they are objects registered with applications and provide various services for 