Class yii\behaviors\TimestampBehavior


Inheritance:

	yii\behaviors\TimestampBehavior  >> yii\behaviors\AttributeBehavior >> yii\bae\Behavior >> yii\base\BaseObject
	
Implements:

	yii\base\Configurable
	
	
----

TimestampBehavior automatically fills the specified attributes with the current timestamp.


To use TimestampBehavior, insert the following code to your ActiveRecord class:


```
use yii\behaviors\TimestampBehavior;

public function behaviors()
{
	return [
		TimestampBehavior::className()
	];
}

```


By default, TimestampBehavior will fill the ***created_at*** and ***updated_at*** attributes with the current timestamp when the associated AR object is being inserted; it will fill the ***updated_at*** attribute with the timestamp when the AR object is being updated. The timestamp value is obtained by ***time()***.

Because attribute values will be set automatically by this behavior, they are usually not user input and should therefore not be validated i.e. ***created_at*** and ***updated_at*** should not appear in the ***rules()*** method of the model.



For the above implementation to work with MySQL database, please declare the columns(***created_at, updated_at***) as int(11) for being UNIX timestamp.


If your attribute names are different or you want to use a different way of calculating the timestamp, you may configure the ***$createdAtAttribute, $updatedAtAttribute*** and ***$value*** properties like the following:


```
use yii\db\Expression;

public function behaviors()
{
	return [
		'class' => TimestampBehavior::className(),
		'createdAtAttribute' => 'created_at',
		'updatedAtAttribute' => 'updated_at',
		'value' => new Expression('NOW()'),
	];
}

```


In case you use an ***yi\db\Expression*** object as in the example above, the attribute will not hold the timestamp value, but the Expression object itself after the record has been saved. If you need the value from DB afterwords you should call the ***refresh()*** method of the record.


TimestampBehavior also provides a method named ***touch()*** that allows you to assign the current timestamp to the specified attribute(s) and save them to the database. For example,

```
 $model->touch('creation_time');
```



