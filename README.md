#Tutorial gulp

  **Cài đặt gulp**

Cài đặt nodejs và npm.Sau đó dùng lệnh npm install gulp để cài đặt 

Tạo project với lệnh npm init(Đang đứng ở thu mục muốn chứa project)

Chạy lệnh npm install gulp để cài gulp cho project

Chạy lệnh touch gulpfile.js để tạo file hoạt động chính của gulp

Trong project tạo file 'src' là file code chính,nó chứa index.html,file sass,css và js

     *Tính năng đầu tiên trong gulp là gộp  file css và js*

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
      
