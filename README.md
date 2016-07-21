# grunt
grunt使用模板
```
module.exports = function (grunt) {

    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),

        concat: {
            foo: {
                files: [
                    { src: ['public/lib/validate_form.js', 'public/javascripts/comment.js', 'public/lib/template.js'], dest: 'public/build/grunt-comment.js' },
                    { src: ['public/lib/validate_form.js', 'public/javascripts/alert.js', 'public/javascripts/login.js'], dest: 'public/build/grunt-login.js' },
                    { src: ['public/lib/jquery.html5uploader.min.js', 'public/lib/validate_form.js', 'public/javascripts/alert.js', 'public/javascripts/reg.js'], dest: 'public/build/grunt-reg.js' }
                ]
            }
        },

        uglify: {
            options: {
                // 是否生成min.js.map
                // sourceMap: true,
                banner: '/*! <%= pkg.name %> - v<%= pkg.version %> - ' + '<%= grunt.template.today("yyyy-mm-dd") %> */',
                footer: '\n/*这是一个压缩后底部*/'
            },
            dist: {

                // 此处对多个js文件进行压缩，用数组表示
                files: [{ 'public/build/grunt-comment-mini.js': 'public/build/grunt-comment.js' },
                    { 'public/build/grunt-login-mini.js': 'public/build/grunt-login.js' },
                    { 'public/build/grunt-reg-mini.js': 'public/build/grunt-reg.js' }
                ]

            }
        },

        cssmin:{
            target:{
                files:{
                    'build/css/build.css':['','']
                }
            }
        },

        watch:{
            script:{
                files:['Gruntfile.js','package.json'],
                tasks:['default']
            }
        }
    });

    // 注册一个合并代码任务
    grunt.loadNpmTasks('grunt-contrib-concat');
    // 注册一个压缩代码任务
    grunt.loadNpmTasks('grunt-contrib-uglify');
    grunt.loadNpmTasks('grunt-contrib-cssmin');
    grunt.loadNpmTasks('grunt-contrib-watch');

    // 默认被执行的任务列表。
    grunt.registerTask('default', ['concat','uglify','cssmin','watch']);
}
