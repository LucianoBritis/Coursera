# Coursera

 # Web Tools: Grunt and Gulp

# Objectives and Outcomes

In this lesson you will learn about JavaScript based Task runners, Grunt and Gulp. You will learn to automate your web development tasks using these tools. At the end of this lesson, you will be able to:

Configure Grunt tasks and automate your web development using Grunt

Define Gulp tasks in code to automate the web development using Gulp

# Web Tools: Task Runners
# Web Tools: Grunt
# Exercise (Video): Web Tools: Grunt
# Exercise (Instructions): Web Tools: Grunt
# Web Tools: Gulp
# Exercise (Video): Web Tools: Gulp
# Exercise (Instructions): Web Tools: Gulp
Exercise (Instructions): Web Tools: Gulp

Objectives and Outcomes

In this exercise, you will learn to use Gulp, the task runner. You will install Gulp CLI and install Gulp plugins using NPM. Thereafter you will configure a Gulp file with a set of tasks to build and serve your web project. At the end of this exercise, you will be able to:

Install Gulp CLI and Gulp plugins in your project
Configure a Gulp file with a set of tasks to build a web project from a source, and serve the built project using a server.
Clean node_modules Folder

Go to the node_modules folder in conFusion, and delete all the folders/files there. We will not be using the Grunt modules existing there for this exercise.
Initialize package.json File

Next, update the package.json file in the conFusion folder with the following content:
{
  "name": "conFusion",
  "private": true,
  "devDependencies": {

  },
  "engines": {
    "node": ">=0.10.0"
  }
}
Installing Gulp

Note: You should already have Node and NPM installed on your computer before you proceed further. Also, those using OSX or Linux should use sudo while installing global packages in node (when you use the -g flag).

At the command prompt, type the following to install Gulp command-line interface (CLI) globally:

npm install -g gulp

This will install the Gulp globally so that you can use it in all projects.

Next install Gulp to use within your project. To do this, go to the conFusion folder and type the following at the prompt:

npm install gulp --save-dev

This will install local per-project Gulp to use within your project.

Install Gulp Plugins

Install all the Gulp plugins that you will need for this exercise. To do this, type the following at the command prompt:

npm install jshint gulp-jshint jshint-stylish gulp-imagemin gulp-concat gulp-uglify gulp-minify-css gulp-usemin gulp-cache gulp-changed gulp-rev gulp-rename gulp-notify  browser-sync del --save-

Creating a Gulp File

Next you need to create a Gulp file containing the tasks to be run when you use Gulp. To do this, create a file named gulpfile.js in the conFusion folder.
Loading Gulp Plugins

Load in all the Gulp plugins by including the following code in the Gulp file:

var gulp = require('gulp'),
    minifycss = require('gulp-minify-css'),
    jshint = require('gulp-jshint'),
    stylish = require('jshint-stylish'),
    uglify = require('gulp-uglify'),
    usemin = require('gulp-usemin'),
    imagemin = require('gulp-imagemin'),
    rename = require('gulp-rename'),
    concat = require('gulp-concat'),
    notify = require('gulp-notify'),
    cache = require('gulp-cache'),
    changed = require('gulp-changed'),
    rev = require('gulp-rev'),
    browserSync = require('browser-sync'),
    del = require('del');
    
Adding Gulp Tasks

Next, we will add the code for the JSHint task, the Clean task and the default task as follows:

gulp.task('jshint', function() {
  return gulp.src('app/scripts/**/*.js')
  .pipe(jshint())
  .pipe(jshint.reporter(stylish));
});

// Clean
gulp.task('clean', function() {
    return del(['dist']);
});

// Default task
gulp.task('default', ['clean'], function() {
    gulp.start('usemin', 'imagemin','copyfonts');
});

Next, paste in the code for the usemin, imagemin and copyfonts tasks:

gulp.task('usemin',['jshint'], function () {
  return gulp.src('./app/menu.html')
      .pipe(usemin({
        css:[minifycss(),rev()],
        js: [uglify(),rev()]
      }))
      .pipe(gulp.dest('dist/'));
});

// Images
gulp.task('imagemin', function() {
  return del(['dist/images']), gulp.src('app/images/**/*')
    .pipe(cache(imagemin({ optimizationLevel: 3, progressive: true, interlaced: true })))
    .pipe(gulp.dest('dist/images'))
    .pipe(notify({ message: 'Images task complete' }));
});

gulp.task('copyfonts', ['clean'], function() {
   gulp.src('./bower_components/font-awesome/fonts/**/*.{ttf,woff,eof,svg}*')
   .pipe(gulp.dest('./dist/fonts'));
   gulp.src('./bower_components/bootstrap/dist/fonts/**/*.{ttf,woff,eof,svg}*')
   .pipe(gulp.dest('./dist/fonts'));
});
Finally, we add the code for the watch and browserSync tasks:

// Watch
gulp.task('watch', ['browser-sync'], function() {
  // Watch .js files
  gulp.watch('{app/scripts/**/*.js,app/styles/**/*.css,app/**/*.html}', ['usemin']);
      // Watch image files
  gulp.watch('app/images/**/*', ['imagemin']);

});

gulp.task('browser-sync', ['default'], function () {
   var files = [
      'app/**/*.html',
      'app/styles/**/*.css',
      'app/images/**/*.png',
      'app/scripts/**/*.js',
      'dist/**/*'
   ];

   browserSync.init(files, {
      server: {
         baseDir: "dist",
         index: "menu.html"
      }
   });
        // Watch any files in dist/, reload on change
           gulp.watch(['dist/**']).on('change', browserSync.reload);
    });
    
    Save the Gulp file
    
    Running the Gulp Tasks

    At the command prompt, if you type gulp it will run the default task: gulp
    
    Using BrowserSync and Watch

    We configured the BrowserSync and the Watch tasks in the Gulp file. To use them, type the following at the command prompt: gulp watch
    
    
    You may need to reload the page in the browser.

    You can edit the menu.html file in the app folder and see the watch task and BrowserSync action in reloading the updated page.
    
    Conclusions

    In this exercise, you learnt to use Gulp, install Gulp plugins, configure the gulpfile.js and then use Gulp to automate the web         development tasks.
    
    
  
  



 
 

# Teste para praticar: Task Runners
# Web Tools: Grunt and Gulp: Additional Resources

  Grunt Resources

Grunt http://gruntjs.com/
Writing an Awesome Build Script with Grunt   http://www.sitepoint.com/writing-awesome-build-script-grunt/
Clean Grunt http://anders.janmyr.com/2014/01/clean-grunt.html
File Globbing http://gruntjs.com/configuring-tasks#globbing-patterns
grunt-contrib-jshint https://github.com/gruntjs/grunt-contrib-jshint
jshint-stylish https://github.com/sindresorhus/jshint-stylish
grunt-contrib-copy https://github.com/gruntjs/grunt-contrib-copy
grunt-contrib-clean https://github.com/gruntjs/grunt-contrib-clean
grunt-usemin https://github.com/yeoman/grunt-usemin
grunt-contrib-concat https://github.com/gruntjs/grunt-contrib-concat
grunt-contrib-cssmin https://github.com/gruntjs/grunt-contrib-cssmin
grunt-contrib-uglify https://github.com/gruntjs/grunt-contrib-uglify
grunt-filerev  https://github.com/yeoman/grunt-filerev


Gulp Resources 

Gulp  http://gulpjs.com/
An Introduction to Gulp.js  http://www.sitepoint.com/introduction-gulp-js/
Getting started with gulp http://www.sitepoint.com/introduction-gulp-js/
Building with Gulp http://www.smashingmagazine.com/2014/06/building-with-gulp/

Tasks

Minification http://www.smashingmagazine.com/2014/06/building-with-gulp/
UglifyJS http://lisperator.net/uglifyjs/
JSHint http://lisperator.net/uglifyjs/


General Resources

Node, Grunt, Bower and Yeoman - A Modern web dev's Toolkit  http://juristr.com/blog/2014/08/node-grunt-yeoman-bower/
The Advantages of Using Task Runners https://www.dbswebsite.com/blog/2015/02/24/the-advantages-of-using-task-runners/
Gulp vs Grunt. Why one? Why the Other? https://www.dbswebsite.com/blog/2015/02/24/the-advantages-of-using-task-runners/
Why we should stop using Grunt & Gulp  http://blog.keithcirkel.co.uk/why-we-should-stop-using-grunt/


end

