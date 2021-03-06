场景：csrf 校验


全局认证和局部认证的接口设置

### $enableCsrfValidation 与 behaviors 中的  authenticator


yii behaviors authenticator 与 enableCsrfValidation



ii2在使用restful作为接口的时候，yii\rest\Controller中已经把全局的csrf验证设置为false，

public $enableCsrfValidation = false;

也就是在post数据的时候，不会在进行_csrf参数的验证。

** 在开发restful接口的时候，比如一个app的服务端restful接口，用户分为游客和登录用户。**

开始，游客打开 app，并没有登录，只是游客身份来访问。这时，app的页面必须的有内容显示，这些内容就是通过restful接口返回的json数据。

所以这些不需要token认证的restful接口就必须设置可以直接访问内容，无需认证，当然这也就是权限设置。

当游客点击app的一个tag,例如“我”，对关于“我”的这个接口，在服务端肯定是要判断用户是否登录了，这个接口只有登录用户才能使用，所以就需要进行token的认证。


公共开放的内容不管是什么身份，只要访问了都可以有权限访问，不需认证。

属于私人的内容呢，就必须要登录了，通过认证了才能访问。

在yii2的restful中，我们可以设置三种安全认证的方式，参考：

http://www.yiichina.com/doc/guide/2.0/rest-authentication



----

### 第一种：使用 HTTP Basic Auth:

```
use yii\helpers\ArrayHelpers;
use yii\filters\auth\HttpBasicAuth;

public function behaviors ()
{
	$parent = parent::behaviors();
	$parent['authenticator'] = [
		'class' => HttpBasicAuth::className(),
		/*
			设置 auth，则按照 auth 进行认证；
			否则是默认使用 access-token 的方式
		*/
		'auth' => function ($username, $password) {
			return \app\models\User::findOne([
				'username' => $username,
				'password' => $password
			])
		}
	];
}

```


### 第二种：access-token 

```
use yii\helpers\ArrayHelper;
use yii\filters\auth\QueryParamAuth;

public function behaviors()
{
	$parent = parent::behaviors();
	$parent['authenticator'] = [
		'class' => QueryParamAuth::className(),
		'tokenParam' => 'token'
	];
}

```

> yii\filters\auth\QueryParamAuth 的 authenticate()

```
public function authenticate($user, $request, $response)
{
	$accessToken = $request->get($this->tokenParam);
	if (is_string($accessToken)) {
		$identify = $user->loginByAccessToken($accessToken, get_class($this));
		if ($identify !== null) {
			return $identify;
		}
	}
	if ($accessToken !== null) {
		$this->handleFailure($response);
	}
	return null;
}

```

----

### 局部设置认证


```
function behaviors () 
{
	$behaviors = parent::behaviors();
	
	$currentAction = Yii::$app->controller->action->id;
	
	$authActions = ['index'];
	
	if (in_array($currentAction, $authActions)) {
		$behaviors['authenticator'] = [
			'class' => QueryParamAuth::className()
		];
	}
	
	return ArrayHelper::merge([
		[
			'class' => Cors::className(),
			'cors' => [
				'Origin' => ['*'],
				'Access-Control-Request-Headers' => ['Origin', 'X-Requested-With', 'Content-Type', 'Accept'],
				'Access-Control-Request-Method' => ['GET', 'POST', 'PUT', 'PATCH', 'DELETE', 'HEAD', 'OPTIONS']
			]
		]
	], $behaviors);
}

```

