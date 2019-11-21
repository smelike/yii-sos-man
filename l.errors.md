$cars = Vehicle::find()->select(['column1', 'column2'])->where(['status' => 0, 'disabled' => 0]);



$cars = Vehicle::find()->where(['status' => 0, 'disabled' => 0]);



```
{
    "success": false,
    "data": {
        "name": "PHP Warning",
        "message": "Invalid argument supplied for foreach()",
        "code": 2,
        "type": "yii\\base\\ErrorException",
        "file": "E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\base\\ArrayableTrait.php",
        "line": 218,
        "stack-trace": [
            "#0 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\base\\ArrayableTrait.php(218): yii\\base\\ErrorHandler->handleError(2, 'Invalid argumen...', 'E:\\\\dxsys\\\\serve\\\\...', 218, Array)",
            "#1 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\base\\ArrayableTrait.php(125): yii\\base\\Model->resolveFields(Array, Array)",
            "#2 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\helpers\\BaseJson.php(157): yii\\base\\Model->toArray()",
            "#3 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\helpers\\BaseJson.php(176): yii\\helpers\\BaseJson::processData(Object(common\\models\\Vehicle), Array, '5dd5ee093b99a9....')",
            "#4 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\helpers\\BaseJson.php(176): yii\\helpers\\BaseJson::processData(Array, Array, '5dd5ee093b99a9....')",
            "#5 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\helpers\\BaseJson.php(61): yii\\helpers\\BaseJson::processData(Array, Array, '5dd5ee093b99a9....')",
            "#6 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\web\\JsonResponseFormatter.php(119): yii\\helpers\\BaseJson::encode(Array, 320)",
            "#7 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\web\\JsonResponseFormatter.php(104): yii\\web\\JsonResponseFormatter->formatJson(Object(yii\\web\\Response))",
            "#8 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\web\\Response.php(1050): yii\\web\\JsonResponseFormatter->format(Object(yii\\web\\Response))",
            "#9 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\web\\Response.php(337): yii\\web\\Response->prepare()",
            "#10 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\base\\Application.php(392): yii\\web\\Response->send()",
            "#11 E:\\dxsys\\serve\\api\\web\\index.php(20): yii\\base\\Application->run()",
            "#12 {main}"
        ]
    }
}

```



## block#2

$idleCars = Vehicle::find()->select('id', 'car_number')->where(['status' => 0, 'disabled' => 0]);
return $idleCars;


```
{
    "success": false,
    "data": {
        "name": "Exception",
        "message": "Cannot use object of type yii\\db\\ActiveQuery as array",
        "code": 0,
        "type": "Error",
        "file": "E:\\dxsys\\serve\\api\\config\\main.php",
        "line": 338,
        "stack-trace": [
            "#0 [internal function]: {closure}(Object(yii\\base\\Event))",
            "#1 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\base\\Component.php(627): call_user_func(Object(Closure), Object(yii\\base\\Event))",
            "#2 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\web\\Response.php(336): yii\\base\\Component->trigger('beforeSend')",
            "#3 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\base\\Application.php(392): yii\\web\\Response->send()",
            "#4 E:\\dxsys\\serve\\api\\web\\index.php(20): yii\\base\\Application->run()",
            "#5 {main}"
        ]
    }
}

```

----


## block#3

 $idleCars = Vehicle::find()->select(['id', 'car_number'])->where(['status' => 0, 'disabled' => 0]);
        return $idleCars->all();

```
{
    "success": false,
    "data": {
        "name": "PHP Warning",
        "message": "Invalid argument supplied for foreach()",
        "code": 2,
        "type": "yii\\base\\ErrorException",
        "file": "E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\base\\ArrayableTrait.php",
        "line": 218,
        "stack-trace": [
            "#0 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\base\\ArrayableTrait.php(218): yii\\base\\ErrorHandler->handleError(2, 'Invalid argumen...', 'E:\\\\dxsys\\\\serve\\\\...', 218, Array)",
            "#1 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\base\\ArrayableTrait.php(125): yii\\base\\Model->resolveFields(Array, Array)",
            "#2 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\helpers\\BaseJson.php(157): yii\\base\\Model->toArray()",
            "#3 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\helpers\\BaseJson.php(176): yii\\helpers\\BaseJson::processData(Object(common\\models\\Vehicle), Array, '5dd5f28ec645a2....')",
            "#4 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\helpers\\BaseJson.php(176): yii\\helpers\\BaseJson::processData(Array, Array, '5dd5f28ec645a2....')",
            "#5 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\helpers\\BaseJson.php(61): yii\\helpers\\BaseJson::processData(Array, Array, '5dd5f28ec645a2....')",
            "#6 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\web\\JsonResponseFormatter.php(119): yii\\helpers\\BaseJson::encode(Array, 320)",
            "#7 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\web\\JsonResponseFormatter.php(104): yii\\web\\JsonResponseFormatter->formatJson(Object(yii\\web\\Response))",
            "#8 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\web\\Response.php(1050): yii\\web\\JsonResponseFormatter->format(Object(yii\\web\\Response))",
            "#9 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\web\\Response.php(337): yii\\web\\Response->prepare()",
            "#10 E:\\dxsys\\serve\\vendor\\yiisoft\\yii2\\base\\Application.php(392): yii\\web\\Response->send()",
            "#11 E:\\dxsys\\serve\\api\\web\\index.php(20): yii\\base\\Application->run()",
            "#12 {main}"
        ]
    }
}

```