Models

[Models](https://www.yiiframework.com/doc/guide/2.0/en/structure-models)


Models are part of the `MVC` architecture. ***They are objects representing business data, rules and logic.

You can create model classes by extending `yii\base\Model` or its child classes.

The base class `yii\base\Model` supports many useful features:

	- Attributes: represent the business data and can be accessed like normal properties or array elements;
	
	- Attribute labels: specify the display labels fro attributes;
	
	- Massive assignment: supports populating multiple attributes in a single step;
	
	- Validation rules: ensures input data based on the declared validation rules;
	
	- Data Exporting: allows model data to be exported in terms of arrays with customizable formats.
	
The `Model` class is also the base class for more advanced models, such as `ActiveRecord`.

Info: You are not required to base your model classes on `yii\base\Model`. However, because there are many Yii components built to support `yii\base\Model`, it is usually the preferable base class for a model.


### Attributes

Models represent business data in terms of attributes. Each attribute is like a publicly accessible property of a model. 

The method `yii\base\Model::attributes()` specifies what attributes a model class has.

You can access an attribute like accessing a normal object property:

```
$model = new \app\models\ContactForm;

// "name" is an attribute of ContactForm
$model->name = 'example';
echo $model->name;

```


You can also access attributes like accessing array elements, thanks to the support for `ArrayAccess` and `Traversable` by `yii\base\Model`:

```
$model = new \app\models\ContactForm;

// accessing attributes like array elements
$model['name'] = 'example';
echo $model['name'];

// Model is traversable using foreach

foreach($model as $name => $value) {}

```


