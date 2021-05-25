# laravel-jwt权限



我的laravel 是6.0的

5.6 php



### 1、安装

​     `composer require tymon/jwt-auth`

这里要是卡死 修改composer下载路径
composer config -g repo.packagist composer https://packagist.phpcomposer.com
或
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/



### 2、配置app.config

```json
//providers元素中添加：
Tymon\JWTAuth\Providers\LaravelServiceProvider::class,

//aliases元素中添加：
'JWTAuth' => Tymon\JWTAuth\Facades\JWTAuth::class,
'JWTFactory' => Tymon\JWTAuth\Facades\JWTFactory::class,
```



### 3、生成jwt.config

 `php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"`

  会自动生成 jwt.config文件



### 4、生成加密密钥

 `php artisan jwt:secret`

//.env 文件下生成一个加密密钥



### 5、设置一个登录模型

   手动创建一张表home_users表

```mysql
SET FOREIGN_KEY_CHECKS=0;
-- ----------------------------
-- Table structure for home_users
-- ----------------------------
DROP TABLE IF EXISTS `home_users`;
CREATE TABLE `home_users` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `email` varchar(50) NOT NULL COMMENT '邮箱',
  `name` varchar(50) NOT NULL COMMENT '姓名',
  `password` varchar(188) NOT NULL COMMENT '密码',
  `status` tinyint(3) DEFAULT '1' COMMENT '状态，1启用，2禁用',
  `created_at` timestamp NULL DEFAULT NULL,
  `updated_at` timestamp NULL DEFAULT NULL,
  `deleted_at` timestamp NULL DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `email` (`email`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8mb4 COMMENT='用户表';

```

​    实现JWTSubject接口，实现getJWTIdentifier()和getJWTCustomClaims()方法

   我的登录模型  放在App\Http\Models\HomeUsers.php;代码如下：

 

```PHP
<?php
namespace App\Http\Models;

use Illuminate\Notifications\Notifiable;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Tymon\JWTAuth\Contracts\JWTSubject;

class HomeUsers extends Authenticatable implements JWTSubject
{

    use Notifiable;

    public function getJWTIdentifier()
    {
        return $this->getKey();
    }

    public function getJWTCustomClaims()
    {
        return [];
    }
    
    public $table='home_users';
    protected $fillable = [
        'email', 'name', 'password','status',
    ];

    protected $dates = ['created_at', 'updated_at', 'deleted_at'];

}

```

###     6、修改 auth.php

​          config/auth.php

  修改：

​    

```json
  'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],

        'api' => [
            'driver' => 'jwt',    //修改为jwt
//            'provider' => 'users',   
            'provider' => 'homeUsers',   //好像设置一个对应于模型
        ],
    ],
    
    
    
    'providers' => [
        'users' => [
            'driver' => 'eloquent',
            'model' => App\User::class,
        ],

        //加入
         'homeUsers' => [
             'driver' => 'eloquent',
             'model' => App\Http\Models\HomeUsers::class, //刚刚自己弄的登录模型
         ],
    ],
    
```

​    

### 7、新建一个控制器

​     我新建立的一个控制器，

   App\Http\Controllers\Api\LoginController  ；代码如下

```php
<?php

namespace App\Http\Controllers\Api;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Hash;

class LoginController extends Controller {


    /**
     * Create a new AuthController instance.
     * 要求附带email和password（数据来源users表）
     * @return void
     */
    public function __construct()
    {
        // 这里额外注意了：官方文档样例中只除外了『login』
        // 这样的结果是，token 只能在有效期以内进行刷新，过期无法刷新
        // 如果把 refresh 也放进去，token 即使过期但仍在刷新期以内也可刷新
        // 不过刷新一次作废
        $this->middleware('auth:api', ['except' => ['login']]);
        // 另外关于上面的中间件，官方文档写的是『auth:api』
        // 但是我推荐用 『jwt.auth』，效果是一样的，但是有更加丰富的报错信息返回
    }

    /**
     * Get a JWT via given credentials.
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function login()
    {
//        dd(Hash::make('123456'));  //生成一个加密的密码
        $credentials = request(['email', 'password']);
        if (! $token = auth('api')->attempt($credentials)) {
            return response()->json(['error' => 'Unauthorized'], 401);
        }
        return $this->respondWithToken($token);
    }

    /**
     * Get the authenticated User.
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function me()
    {
//        return response()->json(auth()->user());
        return response()->json(auth('api')->user());
    }

    /**
     * Log the user out (Invalidate the token).
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function logout()
    {
        auth('api')->logout();

        return response()->json(['message' => 'Successfully logged out']);

//        auth()->logout();
//
//        return response()->json(['message' => 'Successfully logged out']);
    }

    /**
     * Refresh a token.
     * 刷新token，如果开启黑名单，以前的token便会失效。
     * 值得注意的是用上面的getToken再获取一次Token并不算做刷新，两次获得的Token是并行的，即两个都可用。
     * @return \Illuminate\Http\JsonResponse
     */
    public function refresh()
    {
        return $this->respondWithToken(auth('api')->refresh());
    }

    /**
     * Get the token array structure.
     *
     * @param  string $token
     *
     * @return \Illuminate\Http\JsonResponse
     */
    protected function respondWithToken($token)
    {
        return response()->json([
            'access_token' => $token,
            'token_type' => 'bearer',
            'expires_in' => auth('api')->factory()->getTTL() * 60
        ]);
    }


}
```

###    8、路由设置

​    在route/api.php 中设置

   

```php
<?php
/*
|--------------------------------------------------------------------------
| API Routes
|--------------------------------------------------------------------------
|
| Here is where you can register API routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| is assigned the "api" middleware group. Enjoy building your API!
|
*/

Route::namespace('Api')->group(function (){
    Route::group(['prefix' => 'auth'], function(){
        Route::post('login', 'LoginController@login');
        Route::post('logout', 'LoginController@logout');
        Route::post('refresh', 'LoginController@refresh');
        Route::post('me', 'LoginController@me');
    });

});

```

  

9、自己手动插入数据库数据吧，密码加密不知道是什么，在login 方法中 dd(Hash::make('123456')) 打印自己喜欢的一个吧！



### 10、获取tokeng

   ![image-20200430180431604](C:\Users\admin\Desktop\log.png)



### 11、查看用户登录信息

   ![image-20200430180512581](C:\Users\admin\Desktop\me.png)







### 12、其他路由加入验证



 在中间建配置文件Kernel.php加入

 在$routeMiddleware 加入

 'jwtAuth'=>\App\Http\Middleware\GetJwtFromeUserToken::class,



GetJwtFromeUserToken.php代码如下：

```php
<?php
namespace App\Http\Middleware;

use Closure;
use Tymon\JWTAuth\Facades\JWTAuth;
use Tymon\JWTAuth\Exceptions\JWTException;
use Tymon\JWTAuth\Exceptions\TokenExpiredException;
use Tymon\JWTAuth\Exceptions\TokenInvalidException;
class GetJwtFromeUserToken {

    function handle($request,Closure $next){
        try {

            if (! $user = JWTAuth::parseToken()->authenticate()) {
                return response()->json([
                    'status' => 203,
                    'message' => 'user not found'
                ], 203);
            }

        } catch (TokenExpiredException $e) {

            return response()->json([
                'status' => 203,
                'message' => 'token expired'
            ], 203);

        } catch (TokenInvalidException $e) {

            return response()->json([
                'status' => 203,
                'message' => 'token invalid'
            ], 203);

        } catch (JWTException $e) {

            return response()->json([
                'status' => 203,
                'message' => 'token absent'
            ], 203);

        }
        return $next($request);
    }


}
```



路由加入:

```json
  Route::middleware('jwtAuth')->group(function (){
        Route::get('index', 'IndexController@index');
    });
```

访问这个接口就需要带入token要是不带token将验证不通过。



  



结束：有不对的地方请指导；

参考文档：https://www.cnblogs.com/mg007/p/10979469.html

​             	  https://jwt-auth.readthedocs.io/en/develop/quick-start/

 				 https://blog.csdn.net/huangdj321/article/details/104929323

