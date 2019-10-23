#### 新建视图

在resource/view目录下新建php文件

在控制器中 return view\('模板的名称'\)

```php
class NameController extends Controller
{

    public function actionForm(Request $request)
    {
        return view('pandaWeb.chineseName.index', ['meta' => $meta]);
    }
```

- 实际上在view下建立的都是php模板，可以复用。所以文件不再只是以php结尾，而是以.blade.php结尾。

- 一般情况下，一个控制器对应着一个视图模板目录，所以一般先在view下新建目录，然后在其中建立相关的模板。因为laravel的控制器默认是以view作为根目录的，所以view中传入的阐述也要做相应的修改。需要说明的是，这里可以用.表示层级目录，如view('pandaWeb.chineseName.index'）就是pandaWeb下的chineseName下的index文件。

- 如果想向模板中传入参数，则在view中写一个map传入。如return view('pandaWeb.chineseName.index', ['meta' => $meta]);是将名字为meta的值传入。
- 在php模板中使用{{$meta}}的php语法即可获得变量的值。




