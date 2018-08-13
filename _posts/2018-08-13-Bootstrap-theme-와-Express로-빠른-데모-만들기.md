# Bootstrap theme와 Express로 빠른 데모 만들기
## Bootstrap open theme 선택
[https://startbootstrap.com](https://startbootstrap.com)에서 적당한 Bootstrap open theme 선택하고 git clone 등으로 download 한다.

## Express 설치
[http://expressjs.com/ko/starter/hello-world.html](http://expressjs.com/ko/starter/hello-world.html)의 Hello World 작업까지 진행한다.

## Bootstrap과 Express 연동
download 한 Bootstrap 폴더를 Express의 public 폴더로 복사하고 app.js에 root path를 public의 index.html로 설정한다.

<code>
app.use('/dashboard', express.static(path.join(__dirname,'public')));
app.get('/', function(req,res){
  res.redirect('/dashboard');
});
</code>
