[如何为 hasOne 方法的联查添加条件？](https://www.yiichina.com/tutorial/969)


使用 hasOne 与 hasMany 来实现联查


### 联查中设置条件

```

public function getOrderList() {
	$tableAlias = Table::tableName;
	$where['status'] = 1;
	
	return $this->hasOne(Table::className(), ['table_id' => 'id'])->where($where);
}
```

----

**如果条件是可变的，比如要加一个 $where['store_id'] = xx **，要怎么办？

在 getOrderList() 上面添加参数，但是在控制器中，这个方法的调用如下：

```
$model = new ActiveDataProvider([
	'query' => Table::find()->where($where)->with('getOrderList')->orderBy('id desc'),
	'pagination' => ['pageSize' => 10]
])

```

这是使用 with 调用的，怎么加条件？

看了文档中 with 方法后，发现参数是可以使用 callback的。如下所示：

```
Customer::find()->with([
	'orders' => function ($query) {
		$query->andWhere('status = 1');
	},
	'country'
])->all();

```

上面的问题：动态添加条件，就可以用下面的代码解决了。


```
$model = new ActiveDataProvider([
	'query' => Table::find()->where($where)->with(
		[
			'tableType' => function($query) {
				$query->andWhere(['status' => 1, 'store_id' => $this->storeid]);
			}
		]
	)->orderBy('id desc'),
	'pagination' => [
		'pageSize' => 10
	]
])

```


