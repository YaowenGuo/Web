获取请求参数

$music_file = $request->file('data');
$filename = $request->name;
$uuid = $request->input('uuid', '');

$request->has('google_token')
$request->google_token

$data[$key] = $request->{$key} ?? $value;
$request->all();


> CSRF in form

https://stackoverflow.com/questions/28500525/laravel-5-csrf-global-token-hidden-field-for-all-forms-in-a-page

headers: {
   'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
},


laravel request 类里 get方法和input的方法的区别？
2016年07月27日 23:47:14
阅读数：8293

同样一个post请求，以form-data的形式传送一个数据'title'的时候，get('title')和input('title')都可以取到。

但是以json的形式传送的时候，get('title')得到的是null，而input('title')却可以正确的取到值。

对于get请求，get和input方法都可以取到相同的值。

get和input的方法的实现类其实并不一样。

get在：

Symfony\Component\HttpFoundation

input在：

Illuminate\Http

即便是 FromDate

word = $.parseJSON(word);

let formData = new FormData();

即便是 FormDate() 是和用来传递文件。但是即便是 FormData 也无法传递Json对象，需要先转换为Json 字符串。然后再传递。



PandaDictWords::where('word', 'like', $q.'%')
                    ->select(['words.id as id', 'word', 'py', 'trans'])
                    ->join('words_slug', 'words_slug.word_id', '=', 'words.id')
                    ->orderBy('order')->limit(10)->get();



https://www.cnblogs.com/shubiao/p/4450879.html

https://blog.csdn.net/a258831020/article/details/45867191


https://blog.csdn.net/bestcxx/article/details/50732244


https://www.cnblogs.com/yankchina/archive/2010/03/23/1692703.html

https://www.cnblogs.com/alsf/p/7528104.html

https://blog.csdn.net/bestcxx/article/details/50732244

https://blog.csdn.net/hello_word2/article/details/54311125
