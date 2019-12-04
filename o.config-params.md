获取配置文件中的参数值

yii2 中的主要的配置是在 params.php 和 params-local.php 文件中。


参数格式：

```
<?php
	return [
		'adminEmail' => 'admin@example.com',
		'supportEmail' => 'support@example.com',
		'user.passwordResetTokenExpire' => 36000
	];
```

代码中获取参数：

```

\Yii::$app->params['adminEmail'];

```