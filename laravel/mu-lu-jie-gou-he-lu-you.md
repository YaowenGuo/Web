# 路由

路由就是Http中请求的类型，并转发到各个页面的过程，该过程很像网络中的路由，由此得名。

路由都写在app/Http/routes.php文件中。

### 基本路由

基本路由就是http中的请求类型，如get post delete

Route::get\("路径地址", function\(\) {

      // 返回页面或者内容的匿名方法

}\)

// post方法不能通过浏览器的地址访问

Route::post\("index", function\(\) {

      // 返回页面或者内容的匿名方法

      return "Hello Word";

}\)

### 多请求路由

指定的路由，例如get和post的

Route::match\(\['get', 'post'\], 'index', function{

    return "2";

}\)



### 路由参数

Route::get\('index/{id}', fucntion\($id\) {

    return $id;

}\)

可选

Route::get\('index/{id？}', fucntion\($id = null\) {

    return $id;

}\)

还可以用正则表达式

Route::get\('index/{id？}', fucntion\($id = null\) {

    return $id;

}\)->where\('id', '\[0-9\]'\);

Route::get\('index/{id？}/{name}', fucntion\($id = null, $name\) {

    return $id;

}\)->where\(\['id'=&gt; '\[0-9\]', 'name'=&gt;'\[A-Za-z+\]'\);



### 路由别名

Route::get\('index/user-senter', \['as' =&gt;'center',  fucntion\(\) {

    return route\('center'\);

}\]\);



### 路由群组



Route::group\(\['prefix' =&gt; 'member'\], function\(\) {

Route::post\("index", function\(\) {

      // 返回页面或者内容的匿名方法

      return "Hello Word";

}\)

Route::post\("user", function\(\) {

      // 返回页面或者内容的匿名方法

      return "Hello Word";

}\)

}\)

### 路由中输出视图

Route::get\("user", function\(\) {

      // 返回页面或者内容的匿名方法

      return view（"Welcom"\);

}\)



实际项目中，路由只负责接收请求，并转化为给控制器中的方法进行处理，很少在路由中输出视图。

