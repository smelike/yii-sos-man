Class yii\db\BatchQueryResult

BatchQueryResult represents batch query from which you can retrieve data in batches.


You usually do not instantiate BatchQueryResult directly. Instead, you obtain it by calling ***yii\db\Query::batch()*** or ***yii\db\Query::each()***.

Because BatchQueryResult implements the ***Iterator*** interface, you can iterate it to obtain a batch of data in each iteration. For example,