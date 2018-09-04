# Tutorial gulp
 ##  Cài đặt gulp
1. Cài đặt nodejs và npm.Sau đó dùng lệnh npm install gulp để cài đặt 
2. Tạo project với lệnh npm init(Đang đứng ở thu mục muốn chứa project)
3. Chạy lệnh npm install gulp để cài gulp cho project
4. Chạy lệnh touch gulpfile.js để tạo file hoạt động chính của gulp
5. Trong project tạo file 'src' là file code chính,nó chứa index.html,file sass,css và js

 ## Tính năng đầu tiên trong gulp là gộp  file css và js**

npm install --save-dev gulp-concat:  Dùng câu lệnh này để cài gulp concat(gộp file)

Trong file gulpfile.js dán toàn bộ đoạn code này
  
  `var gulp = require('gulp');
   var concat = require('gulp-concat');
   gulp.task('css', function(){
     return gulp.src('thu_mục_chứa_file_css/*.css')
       .pipe(concat('file_css_dc_gop'))
       .pipe(gulp.dest('./thu_muc_chua_file_tren/'));
   });
   gulp.task('default', [  'css']);`
      
      
    
   
      
      
**Các plugin cho gulp**

1.npm install browser-sync --save-dev:trình duyệt tự load khi ctrl + s.

2.Trong terminal gõ lệnh 'gulp task_name' để thực hiện nhiệm vụ nào đó như gộp file hay chuyển scss thành css

3.gulp watch có tác dụng tự động chuyển scss thành css mà không cần phải gõ lệnh gulp task nhiều




***Cài đặt các module để thực hiện minify***

Ta cũng sử dụng npm như trên, thực thi lần lượt các câu lệnh sau để tiến hành cài đặt các module

npm install gulp-minify-css --save-dev

npm install gulp-minify --save-dev

npm install gulp-imagemin --save-dev

npm install imagemin-pngquant --save-dev

**Tạo ra một task mới, đặt tên là compress với nội dung như sau:**


  gulp.task('compress', function() {   //cấu hình minify js

    gulp.src('assets/js/*.js') //đường dẫn đến thư mục chứa các file js

   .pipe(minify({
   
          exclude: ['tasks'],
   
          ignoreFiles: ['-min.js'] //những file không muốn nén
      
      }))
      
      .pipe(gulp.dest('dist/js')); //thư mục dùng để chứa các file js sau khi nén
      
                //cấu hình minify css
       
       gulp.src('assets/css/*.css') //đường dẫn đến thư mục chứa các file css
       
          .pipe(minifyCss({compatibility: 'ie8'}))
         
          .pipe(gulp.dest('dist/css')); //thư mục dùng để chứa các file css sau khi nén
                //cấu hình minify image
        
       gulp.src('assets/images/*') //đường dẫn đến thư mục chứa các file images
       
       .pipe(imagemin({
       
            progressive: true,
            
            svgoPlugins: [{removeViewBox: false}],
            
            use: [pngquant()]
       
       }))
    
    .pipe(gulp.dest('dist/images')); //thư mục dùng để chứa các file images sau khi nén
 
 });
 
 Để thực thi task này (chỉ nên thực thi sau khi đã hoàn tất project), chúng ta gõ lệnh: gulp compress
 
 Trong thư mục project của bạn sẽ xuất hiện thêm một thư mục dist (chứa các file đã được nén) như hình dưới
       compress
  
  File gulpfile.js hoàn chỉnh như sau

      var gulp = require('gulp');

      var browserSync = require('browser-sync');

      var reload = browserSync.reload;

      var minify = require('gulp-minify');

      var minifyCss = require('gulp-minify-css');

      var imagemin = require('gulp-imagemin');

      var pngquant = require('imagemin-pngquant');

      
      
      gulp.task('serve', [], function () {

      browserSync({
      
          notify: false,
          
          server: {
              baseDir: '.'
          }
      });
      
      gulp.watch(['*.html'], reload);
      
      gulp.watch(['assets/js/*.js'], reload);
      
      gulp.watch(['assets/css/*.css'], reload);
      
      gulp.watch(['assets/images/*.css'], reload);
  
     });

  
  
  gulp.task('compress', function() {
  
     //cấu hình minify js
    
     gulp.src('assets/js/*.js') //đường dẫn đến thư mục chứa các file js
     
     .pipe(minify({
      
          exclude: ['tasks'],
          
          ignoreFiles: ['-min.js'] //những file không muốn nén
      }))
      
      .pipe(gulp.dest('dist/js')); //thư mục dùng để chứa các file js sau khi nén
    //cấu hình minify css
    
    gulp.src('assets/css/*.css') //đường dẫn đến thư mục chứa các file css
     
      .pipe(minifyCss({compatibility: 'ie8'}))
    
       .pipe(gulp.dest('dist/css')); //thư mục dùng để chứa các file css sau khi nén
    
    //cấu hình minify image
    
    gulp.src('assets/images/*') //đường dẫn đến thư mục chứa các file images
    
        .pipe(imagemin({
        
             progressive: true,
          
             svgoPlugins: [{removeViewBox: false}],
          
              use: [pngquant()]
      }))
      
       .pipe(gulp.dest('dist/images')); //thư mục dùng để chứa các file images sau khi nén
  });

===========================================
1.
var pug = require('gulp-pug');

gulp.task('pug-html',function() {
 
  return gulp.src('./pug/*.pug')
  
    .pipe(pug({
     pretty : true//dòng này để export ra file html như bình thường
    }))
    
    .pipe(gulp.dest('./pug'));

});

2.Gõ lệnh npm install --save-dev gulp-pug dể cài đặt pug trên gulp



==============================
gulp.task('sass',function() {
    return gulp.src('src/scss/*.scss')
        .pipe(sass().on('error', sass.logError))
        .pipe(gulp.dest('src/css/'));
});
