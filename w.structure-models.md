### structure-models

> https://www.yiiframework.com/doc/guide/2.0/en/structure-models

## Scenarios

A model may be used in different scenario. For example, a `User` model may be used to collect user login inputs, but it may also be used for the user registration purpose.

In different scenarios, a model may use different business rules and logic.

For example, the `email` atrribute may be required during ***user registration***, but not so during ***user login***.




A model uses the `yii\base\Model::$scenario` property to keep track of the scenario it is being used in.

By default, a model supports only a single scenario named `default`. The following code shows two ways of setting the scenario of a model:

```
	// scenario is set as a property
	$model = new User;
	$model->scenario = User::SCENARIO_LOGIN;
	
	// scenario is set through configuration
	$model = new User(['scenario' => User::SCENARIO_LOGIN]);
	
```

By default, the scenarios supported by a model are determined by the `validation rules` declared in the model. 

However, you can customize this behavior by overriding the `yii\base\Model::scenario()` method, like the following:


```
namespace app\models;

use yii\db\ActiveRecord;

class User extends ActiveRecord
{
	const SCENARIO_LOGIN= 'login';
	const SCENARIO_REGISTER = 'register';
	
	public function scenarios()
	{
		return [
			self::SCENARIO_LOGIN => ['username', 'password'],
			self::SCENARIO_REGISTER => ['username', 'email', 'password'],
		];
	}
}

```

> Info: In the above and following examples, the model classes are extending from `yii\db\ActiveRecord` because the usage of multiple scenarios usually happens to `ActiveRecord` classes.


----

The `scenarios()` method returns an array whose keys are the scenario names and values the corresponding active attributes.

**An active attribute can ba `massively assigned` and is subject to `validation`.**

In the above example, the `username` and `password` attributes are active in the `login` scenario; while in the `register` scenario, email is also active besides `username` and `password`.


The default implementation of `scenario()` will return all scenarios found in the validation rule declaration method `yii\base\Model::rules()`.

When overriding `scenarios()`, if you want to introduce new scenarios in addition to the default ones, you may write code like the following:

```
namespace app\models;

use yii\db\ActiveRecord;

class User extends ActiveRecord
{
	const SCENARIO_LOGIN = 'login';
	const SCENARIO_REGISTER = 'register';
	
	public function scenarios()
	{
		$scenarios = parent::scenarios();
		$scenarios[self::SCENARIO_LOGIN] = ['username', 'password'];
		$scenario[self::SCENARIO_REGISTER] = ['username', 'password', 'email'];
		
		return $scenarios;
	}
}
```

----
	
	


----

### Validation Rules

You may call `yii\base\Model::validate()` to validate the received data. The method will use the validation rules declared in `yii\base\Model::rules()` to validate every relevant attibute. If no error is found, it will return `true`. Otherwise, it will keep the errors in the `yii\base\model::$errors` property and return `false`. For example,

```
	
	$model = new \app\models\ContactForm;
	
	// populate model attributes with user inputs
	$model->attributes = \Yii::$app->request->post('ContactForm');
	
	if ($model->validate()) {
		// all inputs are valid
	} else {
		// validate failed: $errors is an array containing error messages
		$errors = $model->errors;
	}
	
```

To declare validation rules associated with a model, override the `yii\base\Model::rules()` method by returning the rules that the model attributes should satisfy. The following example shows the validation rules declared for the `ContactForm` model:


```
public function rules()
{
	return [
		// the name, email, subject and body attributes are required
		[['name', 'email', 'subject', 'body'], 'required'],
		['emial', 'email']
	];
}

```

A rule can be used to validate one or multiple attributes, and an attribute may be validated by one or multiple rules.

Please refer to the `Validateing Input` section for more details on how to validation rules.

(a validate-rule's format is an array, [])

Sometimes, you may want a rule to be applied in certain `scenario`.
To do so, you can specify the `on` property of a rule, like the following:

```
public function rules()
{
	return [
		[['username', 'email', 'password'], 'required', 'on' => self::SCENARIo_REGISTER],
		[['username', 'password'], 'required', 'on' => self::SCENARIO_LOGIN]
	];
}

```

If you do not specify the `on` property, the rule would be applied in all scenarios. A rule is called an active rule if it can be applied in the current `scenario`.


An attribute will be validated if and only if it is an active attribute declared in `scenarios()` and is associated with one or multiple active rules called in `rules()`.

----

### core-validator

https://www.yiiframework.com/doc/guide/2.0/en/tutorial-core-validators

----


### Massive Assignment

Massive assignment is a convenient way of populating a model with user inputs using a single line of code.

It populates the attributes of a model by assigning the input data directly to the `yii\base\Model::$attributes` property.

The following two pieces of code are equivalent, both trying to assign the form data submitted by end users to the attributes of the `ContactForm` model. Clearly, the former, which uses massive assignment, is much cleaner and less error prone than the latter:


```
## 1
$model = new \app\models\ContactForm;
$model->attributes = \Yii::$app->request->post('ContactForm');


##2

$model = new \app\models\ContactForm;
$data = \Yii::$app->request->post('ContactForm', []);
$model->name = isset($data['name']) ? $data['name'] : null;
$model->email = isset($data['email']) ? $data['email'] : null;
$model->subject = isset($data['subject']) ? $data['subject'] : null;
$model->body = isset($data['body']) ? $data['body'] : null;

```

### Safe Attributes

Massive assignment only applies to the so-called safe attributes which are the attributes listed in `yii\base\Model::scenarios()` for the current `scenario`of a model.

For example, if the `User` model has the following scenario declaration, **then when the current scenario is `login`,** only the `username` and `password` can be massively assigned. Any other attributes will kept untouched.


```
public function scenario()
{
	return [
		self::SCENARIO_LOGIN => ['username', 'password'],
		self::SCENARIO_REGISTER => ['username', 'password', 'email']
	];
}
```
----
> Info: The reason that massive assignment only applies to safe attributes is because you want to control which attributes can be modified by end user data. For example, if the `User` model has a `permission` attribute which determines the permission assigned to the user, you would like this attribute to be modifiable by adminstrators through a backend interface only.


----

Because the default implementation of `yii\base\Model::scenario()` will return all scenarios and attributes found in `yii\base\Model::rules()`, if you do not override this method, **it means an attribute is safe as long as it appears in one of *the active validation rules*.**


For this reason, a special validator aliased `safe` is provided so that you can declare an attribute to be safe without actually validating. For exampl, the following rules declared that both `title` and `description` are safe attributes.


```
	public function rules()
	{
		return [
			[['title', 'description'], 'safe']
		];
	}
```


### Unsafe Attributes (!)

As described above, the `yii\base\Model:scenarios()` method serves for two purpose: determining which attributes should be validated, and determining which attibutes are safe.

In some rare cases, you may want to *validate an attribute but do not want to mark it safe.* You can do so by prefixing an exclamation mark `!` to the attribute name when declaring ig in `scenarios()`, like the `secret` attribute in the following:


```
	public function scenarios()
	{
		return [
			self::SCENARIO_LOGIN => ['username', 'password', '!secret']
		];
	}
```

When the model is in the `login` scenario, all three attributes will be validated. However, only the `username` and  `password` attributes can be massively assigned. To assign an input value to `secret` attribute, you have to do it explicitly as follows,

```
$model->secret = $secret;

```

The same can be done in `rules()` method:

```
public function rules()
{
	return [
		[['username', 'password', '!secret'], 'required', 'on' => 'login']
	];
}
```

In this case attributes `username`,  `password` and `secret` are required, but `secret` must be assigned explicitly.


----

### Data Exporting

Models often need to be exported in different formats. For example, you may want to convert a collection of models into JSON or Excel format. The exporting process can be broken down into two independent steps:

- models are converted into arrays;

- the arrays are converted into target formats.

You may just focus on the first step, because the second step can be achieved by generic data formatters, such as `yii\web\JsonResponseFormatter`.

The simplest way of converting a model into an array is to use the `yii\base\Model::$attributes` property. For exaple,

```

$post = \app\models\Post::findOne(100);
$array = $post->attributes;

```

By default, the `yii\base\Model::$attributes` property will return the values of all attributes declared in `yii\base\Model::attributes()`.


A more flexible powerful way of converting a model into an array is to use the `yii\base\Model::toArray()` method. Its default behavior is the same as that of `yii\base\Model::$attributes`. However, it allows you to choose which data items, called fields, to be put in the resulting array and how they should be formatted. In fact, it is the default way of exporting models in RESTful Web service development, as described in the `[Response Formatting](https://www.yiiframework.com/doc/guide/2.0/en/rest-response-formatting)`.



----

### Fields

A field is simply a named element in the array that is obtained by calling the `yii\base\Model::toArray()` method of a model.

By default, field names are equivalent to attribute names. However, you can change this behavior by overriding the `fields()` and/or `extraFields()` methods.

- Fieldds()

Both methods should return a list of field  definitions. The fields defined by `fields()` are default fields, meaning that `toArray()` will return these fields by default. 

- ExtraFields()

The `extraFields()` method defines additionally available fields which can also be returned by `toArray()` as long as you specify them via the `$expand` parameter.

For example, the following code will return all fields defined in `fields()` and the `prettyName` and `fullAddress` fields if they are defined in `extraFields()`.


```

$array = $model->toArray([], ['prettyName', 'fullAddress']);

```


You can override `fields()` to add, remove, rename or redefine fields. The return value of `fields()` should be an array. The array keys are the field names, and the array values are the corresponding field definitions which can be either property/attribute names or anonymous functions returning the corresponding field values. In the special case when a field name is the same as its defining attribute name, you can omit the array key. For example,


```

public function fields()
{
	return [
		'id',
		'email' => 'email_address',
		'name' => function () {
			return $this->first_name . ' ' . $this->last_name;
		}
	];
}

public function fields()
{
	$fields = parent::fileds();
	
	// remove fields that contain sensitive information
	unset($fields['auth_key'], $fields['password_hash'], $fields['password_rest_token']);
	
	return $fields;
}
```

> Warning: Because by default all attributes of a model will included in the exported array, you should examin your data to make sure they do not contain sensitive information. If there is such information, you should override `fields()` to filter them out. In the above example, we choose to filter out `auth_key`, `password_hash` and `password_reset_token`.




----

## Best practices

In a well-designed application, models are usually much fatter than `[controllers](https://www.yiiframework.com/doc/guide/2.0/en/structure-controllers)`

In summary, models

- may contain attributes to represent business data;

- may contain validation rules to ensure the data validity and integrity;

- may contain methods implementing business logic;

- should NOT directly access request, session, or any other enviromental data. These data should be injected by `[controllers](https://www.yiiframework.com/doc/guide/2.0/en/structure-controllers)` into models;

- should avoid embeding HTML or other presentational code - this is bettern done in view;


- avoid having too many `[scenarios](https://www.yiiframework.com/doc/guide/2.0/en/structure-models#scenarios)` in  a single model.


----

You may usually consider the last recommendation above when you are developing large complex systems. In these systems, models could be very fast because they are used in many places and may thus contain many sets of rules and business logic.

This often ends up in a nightmare in maintaining the model code because a single touch of the code could affect several different places.

To make the model code more maintainable, you may take the following strategy:


- Define a set of base model classes are shared by different `[application](https://www.yiiframework.com/doc/guide/2.0/en/structure-applications)` or `[modules](https://www.yiiframework.com/doc/guide/2.0/en/structure-modules)`.

These model classes should contain minimal sets of rules and logic that are common all their usages.

- In each `[application](https://www.yiiframework.com/doc/guide/2.0/en/structure-applications)` or `[module](https://www.yiiframework.com/doc/guide/2.0/en/structure-modules)`

that uses a model, define a concrete model class by extending from

















