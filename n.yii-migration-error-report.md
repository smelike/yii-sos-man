Yii-migration-Error-Report

[stack-overflow-explain](https://stackoverflow.com/questions/1814532/1071-specified-key-was-too-long-max-key-length-is-767-bytes)

```

i think your calculation is a bit wrong here. mysql uses 1 or 2 extra bytes to record the values length: 1 byte if the column's max length is 255 bytes or less, 2 if it's longer than 255 bytes. the utf8_general_ci encoding needs 3 bytes per character so varchar(20) uses 61 bytes, varchar(500) uses 1502 bytes in total 1563 bytes 

```

## Yii2 migration error: sql-max key length is 767 bytes.

----

```
*** applying m191127_073727_create_clue_table
    > create table {{%clue}} ...Exception: SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes
The SQL being executed was: CREATE TABLE `clue` (
        `id` int(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
        `title` varchar(256) NOT NULL UNIQUE COMMENT '线索名称',
        `type` tinyint(3) NOT NULL DEFAULT 0 COMMENT '0-企业，1-个人',
        `industry_id` int(11) COMMENT '行业类型',
        `connect` varchar(64) COMMENT '联系电话',
        `mobile` varchar(12) COMMENT '联系手机',
        `addr` varchar(128) COMMENT '通信地址',
        `note` varchar(256) COMMENT '备注',
        `charged_by` int(11) COMMENT '负责人，默认创建人',
        `created_by` int(11) COMMENT '创建人',
        `created_at` int(11) COMMENT '创建时间',
        `updated_at` int(11) COMMENT '更新时间'
) CHARACTER SET utf8 COLLATE utf8_general_ci ENGINE=InnoDB (E:\dxsys\serve\vendor\yiisoft\yii2\db\Schema.php:664)


```


## Yii2 migration-error

```
Apply the above migrations? (yes|no) [no]:yes
*** applying m191127_073727_create_clue_table
    > create table {{%clue}} ...Exception: SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key wates
The SQL being executed was: CREATE TABLE `clue` (
        `id` int(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
        `title` varchar(256) NOT NULL UNIQUE COMMENT '线索名',
        `type` tinyint(3) NOT NULL DEFAULT 0 COMMENT '0-企,1-个',
        `industry_id` int(11) COMMENT '行业',
        `connect` varchar(64) COMMENT '联系电话',
        `mobile` varchar(12) COMMENT '联系手机',
        `addr` varchar(128) COMMENT '通信地址',
        `note` varchar(256) COMMENT '备注',
        `charged_by` int(11) COMMENT '默认创建人',
        `created_by` int(11) COMMENT '创建人',
        `created_at` int(11) COMMENT '创建时间',
        `updated_at` int(11) COMMENT '更新时间'
) CHARACTER SET utf8 COLLATE utf8_general_ci ENGINE=InnoDB (E:\dxsys\serve\vendor\yiisoft\yii2\db\Schema.php:664)
#0 E:\dxsys\serve\vendor\yiisoft\yii2\db\Command.php(1295): yii\db\Schema->convertException(Object(PDOException), '
#1 E:\dxsys\serve\vendor\yiisoft\yii2\db\Command.php(1091): yii\db\Command->internalExecute('CREATE TABLE `c...')
#2 E:\dxsys\serve\vendor\yiisoft\yii2\db\Migration.php(323): yii\db\Command->execute()
#3 E:\dxsys\serve\console\migrations\m191127_073727_create_clue_table.php(33): yii\db\Migration->createTable('{{%cl
#4 E:\dxsys\serve\vendor\yiisoft\yii2\db\Migration.php(114): m191127_073727_create_clue_table->safeUp()
#5 E:\dxsys\serve\vendor\yiisoft\yii2\console\controllers\BaseMigrateController.php(725): yii\db\Migration->up()
#6 E:\dxsys\serve\vendor\yiisoft\yii2\console\controllers\BaseMigrateController.php(199): yii\console\controllers\B1127_073727_...')
#7 [internal function]: yii\console\controllers\BaseMigrateController->actionUp(0)
#8 E:\dxsys\serve\vendor\yiisoft\yii2\base\InlineAction.php(57): call_user_func_array(Array, Arra
#9 E:\dxsys\serve\vendor\yiisoft\yii2\base\Controller.php(157): yii\base\InlineAction->runWithPar
#10 E:\dxsys\serve\vendor\yiisoft\yii2\console\Controller.php(148): yii\base\Controller->runActio
#11 E:\dxsys\serve\vendor\yiisoft\yii2\base\Module.php(528): yii\console\Controller->runAction(''
#12 E:\dxsys\serve\vendor\yiisoft\yii2\console\Application.php(180): yii\base\Module->runAction('
#13 E:\dxsys\serve\vendor\yiisoft\yii2\console\Application.php(147): yii\console\Application->run
#14 E:\dxsys\serve\vendor\yiisoft\yii2\base\Application.php(386): yii\console\Application->handle
#15 E:\dxsys\serve\yii(23): yii\base\Application->run()
#16 {main}
```