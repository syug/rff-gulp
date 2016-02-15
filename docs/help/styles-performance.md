# Task "styles" is too slow

When you have huge stylesheets, CSS minification would be slow, especially [postcss-discard-duplicates](https://github.com/ben-eb/postcss-discard-duplicates) plugin has large performance hit.  
Set `discardDuplicates: false` to improve the performance.
But this decreases the compressibility.

```diff
gulp.task('styles', ['sprites', 'fonts'], function () {
  return gulp.src('app/styles/**/*.scss')
    .pipe($.sass().on('error', $.sass.logError))
    .pipe($.postcss([
      autoprefixer({browsers: browsers}),
      cssnano({
        safe: true,
-       autoprefixer: false
+       autoprefixer: false,
+       discardDuplicates: false
      })
    ]))
    .pipe(gulp.dest('dist/styles'));
});
```