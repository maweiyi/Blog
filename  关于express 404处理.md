

```
app.use(function(req, res, next) {
  var err = new Error('Not Found');
  err.status = 404;
  next(err);
});

// error handler
app.use(function(err, req, res, next) {
  // set locals, only providing error in development
  res.locals.message = err.message;
  res.locals.error = req.app.get('env') === 'development' ? err : {};

  // render the error page
  res.status(err.status || 500);
  res.render('error');
});

```
处理404的中间件放在所有的路由中间件的下面，当请求过来的时候，如果和所有的路由中间件都不匹配，那么将转到404处理中间件

##### 自定义404页面

```
app.use(function(req, res, next) {
  var err = new Error('Not Found');
  err.status = 404;
  res.render('404');
});
```