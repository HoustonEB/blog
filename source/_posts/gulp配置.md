---
title: gulp配置
date: 2019-09-21 16:57:17
categories: gulp
tags:
- gulp
---
### gulp api
1. task
gulp.task([taskName], taskFunction).
```js
gulp.task('build', ['task1', 'task2'], function() {});

gulp在4版本后不在支持这种嵌套任务的写法.改用一下写法.
gulp.task('build, gulp.series('task1', 'task2'), function() {console.log('this is build task')});

gulp 执行多个任务是存在异步的问题.如果需要上一个任务执行完毕后执行任务二.需要使用cb();
eg: gulp.task('task1', function(cb) {
  console.log('taks1 content');
  cb()
});
gulp.taks('task2',gulp.series('task1', function() {
  console.log('task2');
})})

result: task1 content  task2

```
<!-- more -->
2. series(串行)
```js
gulp.task('test', function(cb) {
    console.log('2');
    cb();
});

gulp.task('test1', function(cb) {
    setTimeout(function() {
        console.log('test1');
        cb();
    },2000)
});
gulp.task('test2', function(cb) {
    console.log('test2');
    cb();
});
gulp.task('default', gulp.series('test1', 'test2', function() {
    console.log('end')
}));
// cb函数要放在异步函数内,否则无效. 输出test2 end test1
result: test1 test2 end
```
3. parallel(并行)
```js
gulp.task('test1', function(cb) {
    console.log('start1')
    setTimeout(function() {
        console.log('test1');
        cb();
    },2000)
});
gulp.task('test2', function(cb) {
    console.log('start2')
    console.log('test2');
    cb();
});
gulp.task('default', gulp.parallel('test1', 'test2', function() {
    console.log('end')
}));

result: start1 start2 test2 end test1
```
### gulp plugins
1. less
```js
var gulp = require('gulp');
var less = require('gulp-less');

gulp.task('css', function(cb) {
   gulp.src('./css/**/*.less').pipe(
       less()
   ).pipe(
       gulp.dest('./release/css')
   );
    cb()
});
```
 [gulp-less](https://github.com/gulp-community/gulp-less)
2. less-plugin-autoprefix
```js
var LessAutoprefix = require('less-plugin-autoprefix');
var autoprefix = new LessAutoprefix({ browsers: ['last 2 versions'] });

return gulp.src('./less/**/*.less')
  .pipe(less({
    plugins: [autoprefix]
  }))
  .pipe(gulp.dest('./public/css'));
```
 [less-plugin-autoprefix](https://github.com/less/less-plugin-autoprefix)
3. gulp-sourcemaps
定位错误位置
```js
var gulp = require('gulp');
var plugin1 = require('gulp-plugin1');
var plugin2 = require('gulp-plugin2');
var sourcemaps = require('gulp-sourcemaps');

gulp.task('javascript', function() {
  gulp.src('src/**/*.js')
    .pipe(sourcemaps.init())
      .pipe(plugin1())
      .pipe(plugin2())
    .pipe(sourcemaps.write('../maps'))
    .pipe(gulp.dest('dist'));
});
```
 [gulp-sourcemaps](https://github.com/gulp-sourcemaps/gulp-sourcemaps)