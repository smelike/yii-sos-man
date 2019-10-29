Yii - 配置



Yii-restful-api-config

main.php/ main-localhost.php



## 方法

Yii::createObject() - 接受一个配置数组并根据数组中指定的类名创建对象。

对象实例化后，剩余的参数被用来初始化对象的属性，事件处理和行为。


Yii::configure($object, $config) - 根据配置去初始化对象 $object 属性



## 配置格式

一个配置的格式描述如下：

[
	'class' => 'className',
	'propertyName' => 'propertyValue',
	'on eventName' => $eventHandler,
	'on behaviorName' => $behaviorConfig
]


## 配置

1) 应用的配置；2) 小部件的配置；3) 配置文件 (configuration Files)


> 配置文件
	
```

return [
	'id' => 'basic',
	'basePath' => dirname(__DIR__),
	'extensions' => require __DIR__ . '/../vendor/yiisoft/extensions.php',
	'components' => require __DIR__ . '/components.php'
]

```




