
批量插入数据



```

$fields = ['field1', 'field2', 'field3'];

$data = [
	['value1', 'value12', 'value3'],
	['value1', 'value12', 'value3'],
	['value1', 'value12', 'value3']
];

$res = Yii::$app->db->createCommand()->batchInsert(Model::tableName(), $fields, $data)->execute();

```