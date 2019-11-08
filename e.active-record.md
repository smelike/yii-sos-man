# ActiveRecord


`An Active Record class` is associated with `a database table`, 
`an Active Record instance` corresponds to `a row of that table`, 
and `an attribute of an Active Record instance` represents `the value of a particular column` in that row.


## Tools

- Using a migration to create database tables

- Using Gii to create defaule model code




## Declaring an Active Record Class in a Model

How to transform a Yii model to leverage Actice Record.


Using Active Record with a model is quite simple; notice the `class Launch extends \yii\db\ActiceRecord`:


```
<?php
namespace frontend\models;

use Yii;
use yii\db\ActiveRecord;

/**
	* This is the model class for the table "launch"
	*@property integer $id
	*@property string $email
	*@property string $ip_addr
	*@property integer $status
	*@property integer $created_at
	*@property integer $updated_at
	
*/

class Launch extends \yii\db\ActiveRecord
{
	cosnt STATUS_REQUEST = 0;
	
	/**
	* @inheritdoc
	*/
	public static function tableName()
	{
		return 'launch';
	}
}
```

## Building Queries

Let's look at some common Acitve Record queries.


If you have a record ID, often from a query parameter  from a controller, it's easy to find the record you want:

```
public function actionSomething($id)
{
	$model = Launch::findOne($id);
}
```

This is identical to:

```

$model = Launch::find()
		->where(['id' => $id])
		->one();
		
```

Extend the `->where` array with more fields or boolean conditions:


```
$model = Launch::find()
		->where(['id' => $id, 'status' => Launch::ACTIVE_REQUEST])

// equivalent to 
$model = Launch::find()
		->where(['id' => $id])
		->andWhere(['status' => Launch::ACTIVE_REQUEST])
		->orWhere(['status' => Launch::FUTURE_REQUEST]);
```

## Multiple Records

An example of finding all records that match a specific `status` sorted by `$id`:


```
$people = Launch::find()
	->where([''status' => Launch::STATUS_REQUEST])
	->orderBy('id')
	->all();
```

The variable `$people`  is returned as an array of model objects.

## Return an Array

Using `indexBy` returns an array of items indexed by their `id`:

```
	$people = Launch::find()
			->indexBy('id')
			->all();
```

Return an associative array with `->asArray`:

```
	$peopl = Launch::find->asArray()->all();
	
```

```

Note: `asArray` saves memory and improves performance, it is closer to the lower DB abstraction layer and you will lose most of the Active Record features.

```

## Counting Records 

Return just a `count` from a query:

```

$count = Launch::find()
		->where(['status' => Launch::STATUS_REQUEST])
		->count();


```

### Where condition

```
	->where()
	->andWhere()
	->orWhere()
	
```

### Accessing the Data

Once you've queried data, such as an individual model, it's easy to access the data as a model object:

```

	$model = Launch::findOne($id);
	$id = $model->id;
	$email = $model->email;

```

Process arrays this way:

```
	$users = User::findAll();
	foreach($users as $u) {
		$id = $u->id;
		$email = $u->email;
	}
```

### Massive Assignment

Assign an array to a model record via ActiveRecord:

```
	$values = [
		'name' => 'Jmaes',
		'email' => 'jamesx@example.com'
	];
	
	$customer = new Customer();
	$customer->attributes = $values;
	$customer->save();
	
```

This is often used for populating model data after a form submission:


```
	if (isset($_POST['formName'])) {
		$model->attributes = $_POST['formName'];
		if ($model->save()) {
			// handle success
		}
	}
```

Or you can use `->load()` for this:

```
	if ($model->load(Yii::$app->request->post(), '') && $model->save()) {
		// ...
	}
```

Yii's Gii scaffolding code generation is great at generating models using ActiveRecord that do a lot of this for you, e.g. models, controllers, forms, views, etc.

## Saving Data

a new record is created and saved - and then a record is loaded by id, and updates are saved:


```
// insert a new row of data
$customer = new Customer();

$customer->name = 'james';
$customer->email = 'jamesx@example.com';
$customer->save();


// update an existing row of data
$customer = Customer::findOne(123)
$customer->email = 'jemasx@exa.com';
$customer->save();

```


## Deleting Records

```

$u = User::findOne(99);
$u->delete();

```

## Updating Counters

a user schedules another meeting

```

$u = User::findOne(99);
$u->updateCounters(['meeting_count' => 1]);

```

## Relations

Connecting tables across indexes is one of Active Record's most powerful capabilities.

For example, in Meeting Planner, each meeting may have 0 or more `MeetingPlaces`.

The Meeting.php model defines a relational ActiveQuery for this:

```
	/**
	* @property MeetingPlace[] $meetingPlaces
	* @return \yii\db\ActiveQuery
	*/
	public function getMeetingPlaces()
	{
		return $this->hasMany(MeetingPlace::className(), ['meeting_id' => 'id']);
	}

```

















