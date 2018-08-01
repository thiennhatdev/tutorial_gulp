#Tutorial gulp

  **Cài đặt gulp**

Cài đặt nodejs và npm.Sau đó dùng lệnh npm install gulp để cài đặt 

Tạo project với lệnh npm init(Đang đứng ở thu mục muốn chứa project)

Chạy lệnh npm install gulp để cài gulp cho project

Chạy lệnh touch gulpfile.js để tạo file hoạt động chính của gulp

Trong project tạo file 'src' là file code chính,nó chứa index.html,file sass,css và js

     **Tính năng đầu tiên trong gulp là gộp  file css và js**

npm install --save-dev gulp-concat:  Dùng câu lệnh này để cài gulp concat(gộp file)

Trong file gulpfile.js dán toàn bộ đoạn code này
    ================================
    var gulp = require('gulp');
     
      var concat = require('gulp-concat');
     
      
     
      gulp.task('css', function(){
        return gulp.src('thu_mục_chứa_file_css/*.css')
          .pipe(concat('file_css_dc_gop'))
          
          .pipe(gulp.dest('./thu_muc_chua_file_tren/'));
      });

     
      gulp.task('default', [  'css']);
      ====================================
   
      
      
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
==================================================

1.Dùng lệnh npm install  gulp-template-html --save để cài task html cho  project

2.Trong folder gốc tạo 2 folder chứa 2 file html,1 file nguồn tên được gắn vào biến trong file gulpfile.js và 1 file con được gộp

3.Trong file gulpfile.js lưu thêm đoạn code
   
   var build_template = require('gulp-template-html'); 
   gulp.task('build_template', function(){
    
    return gulp.src('src/html/*.html')
    
    .pipe(template('src/template/build-template.html'))
    
    .pipe(gulp.dest('./dist/'));

});

4.Trong file gốc những phần động đặt là <!--build:ten_the_hoac_khoi-->

5.Trong file con nội dung được viết trong <!--build:ten_the_hoac_khoi-->Nội dung được build ra<!--/build:ten_the_hoac_khoi-->

6.Sau khi xong chạy lệnh gulp ten_task.File đầu ra sẽ nằm ở thư mục được cài đặt trong gulpfile.js


===========================================
1.var pug = require('gulp-pug');

gulp.task('pug-html',function() {
 
  return gulp.src('./pug/*.pug')
  
    .pipe(pug())
    
    .pipe(gulp.dest('./pug'));

});

2.Gõ lệnh npm install --save-dev gulp-pug dể cài đặt pug trên gulp
