SQL-Query


```
SQLSTATE[42000]: Syntax error or access violation: 1064 You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '! NULL) AND (`lend_trans_id` IN (4, 6, 7, 8, 9, 10, 11, 12, 13))' at line 1 The SQL being executed was: 

SELECT * FROM `seal_lend_log` WHERE (`lend_time` ! NULL) AND (`lend_trans_id` IN (4, 6, 7, 8, 9, 10, 11, 12, 13))

```

> select * from tableName where back_time != null;

> select * from tableName where back_time <> null;

> select * from tableName where back_time;

----

多表关联

[多表关联浅析](https://www.yii-china.com/topic/detail/110)

### 定义多个关联

```

class Customer extends \yii\db\ActiveRecord
{
    public function getBigOrders($threshold = 100)
    {
        return $this->hasMany(Order::className(), ['customer_id' => 'id'])
        ->where('subtotal > :threshold', [':threshold' => $threshold])
        ->orderBy('id');
    }
}

```