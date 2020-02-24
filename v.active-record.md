https://www.yiiframework.com/doc/guide/2.0/en/db-active-record

Active Record

**Actuive Record** provides an object-oriented interface for accessing and manipulating data stored in database.

An Active Record class is associated with a database table, an Active Record instance corresponds to a row of that table, and an attribute of an Active Record instance represents the value of a particular column in that row.

Instead of writing raw SQL statements, you would access Active Record  attributes and call Active Record methods to access and manipulate the data stored in database tables.


For example, assume **Customer** is an Active Record class which is associated with the **customer** table and **name** is a column of the **customer** table. You can write the following code to insert a row into **customer** table:


```

$customer = new Customer();
$customer->name = 'Qiang';
$customer->save();

```

The above code is equivalent to using the following raw SQL statement for MySQL, which is less intuitive, more error prone, and may even have compatibility problems if you are using a different kind of database:

```

$db->createCommand('INSERT INTO `customer` (`name`) VALUES (:namne)', [
	':name' => 'Qiang',
])->execute();

```

----

Yii provides the Active Record support for the following relational database:

	- MySQL 4.1 or later: via *yii\db\ActiveRecord*

	- PostgreSQL 7.3 or later: via *yii\db\ActiveRecord*

	- SQLite 2 and 3: via *yii\db\ActiveRecord*

	- Microsoft SQL Server 2008 or later: via *yii\db\ActiveRecord*

	- Oracle: via *yii\db\ActiveRecord*

	- CUBRID 9.3 or later: via *yii\db\ActiveRecord* (Note that due to a bug in the cubrid PDO extension, quoting of values will not work, so you need CUBRID 9.3 as the client as well as the server)


	- Sphinx: via `yii\sphinx\ActiveRecord`, requires the `yii2-sphinx`

	- ElasticSearch: via `yii\elasticsearch\ActiveRecord`, requires the `yii2-elasticsearch` extension

Additionally, Yii also supports using Active Record with the following NoSQL databases:

	- Redis 2.6.12 or later: via `yii\redis\ActiveRecord`, required the `yii2-redis` extension
	
	- MongoDB 1.3.0 or later: via `yii\mongodb\ActiveRecord`, requires the `yii2-mongodb` extention
	
	
In this tutorial, we will mainly describe the usage of Active Record for relational database. However, most content described here are also applicable to Active Record for NoSQL databases.


----

### Declaring Active Record Classes

To get started, declare an Active Record class by extending `yii\db\ActiveRecord`.


#### Setting a table name


By default each Active Record class is associated wiht its database table. The `tableName()` method returns the table name by converting the class name via `yii\helpers\Inflector::camel2id`.

You may override this method if the table is not named after this convention.

Also a default `tablePrefix` can be applied. For example if `tablePrefix` is **tbl_**, **Customer** becomes `tbl_customer` and `OrderItem` becomes `tbl_order_item`.


If a table name is given as `{{%TableName}}`, then the percentage character `%` will be replaced with the table prefix.

For example, `{{%post}}` becomes `{{tbl_post}}`. The brackets around the table name are used for [quoting in an SQL Query](https://www.yiiframework.com/doc/guide/2.0/en/db-dao#quoting-table-and-column-names).


In the following example, we declare an Active Record class named `Customer` for the `customer` database table.


```
namespace app\models;

use yii\db\ActiveRecord;

class Customer extends ActiveRecord
{
	const STATUS_INACTIVE = 0;
	const STATUS_ACTIVE = 1;
	
	/**
	* @return string the name of the table associated with this ActiveRecord class.
	*/
	
	public static funciton tableName()
	{
		return '{{customer}}';
	}
}

```

Active records are called "models"

Active Record instances are considered as `models`. For this reason, we usually put Active Record classes under the `app\models` namespace (or other namespaces for keeping model classes).


Because `yii\db\ActiveRecord` extends from `yii\base\Model`, it inherits all `[model](https://www.yiiframework.com/doc/guide/2.0/en/structure-models)` features, such as attributes, validation rules, data serialization, etc.







