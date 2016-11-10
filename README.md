# gulp-documentation

[![Circle CI](https://circleci.com/gh/documentationjs/gulp-documentation.svg?style=svg)](https://circleci.com/gh/documentationjs/gulp-documentation)

Use [gulp](http://gulpjs.com/) with
[documentation](https://github.com/documentationjs/documentation)
to generate great documentation for your JavaScript projects.

## Installation

```sh
$ npm install --save-dev gulp-documentation
```

## API

### documentation

Documentation stream intended for use within the gulp system.

**Parameters**

-   `format` **\[[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)]** format - one of 'html', 'md', or 'json' (optional, default `md`)
-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** documentation options - the same as given to [documentation](https://github.com/documentationjs/documentation)
    -   `options.filename` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** custom filename for md or json output
-   `formatterOptions` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** output options - same as given to documentation
    -   `formatterOptions.name` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** if format is HTML, specifies the name of the project

**Examples**

```javascript
var gulpDocumentation = require('gulp-documentation'),
var gulp = require('gulp');
//  Out of the box, you can generate JSON, HTML, and Markdown documentation
gulp.task('documentation', function () {

  // Generating README documentation
  gulp.src('./index.js')
    .pipe(gulpDocumentation('md'))
    .pipe(gulp.dest('md-documentation'));

  // Generating a pretty HTML documentation site
  gulp.src('./index.js')
    .pipe(gulpDocumentation('html))
    .pipe(gulp.dest('html-documentation'));

  // Generating raw JSON documentation output
  gulp.src('./index.js')
    .pipe(gulpDocumentation('json'))
    .pipe(gulp.dest('json-documentation'));

});

// Generate documentation for multiple files using normal glob syntax.
// Note that this generates one documentation output, so that it can
// easily cross-reference and use types.
gulp.task('documentation-multiple-files', function () {

  gulp.src('./src/*.js')
    .pipe(gulpDocumentation({ format: 'md' }))
    .pipe(gulp.dest('md-documentation'));

});


// If you're using HTML documentation, you can specify additional 'name'
// and 'version' options
gulp.task('documentation-html-options', function () {

  gulp.src('./src/*.js')
    .pipe(gulpDocumentation('html', {}, {
      name: 'My Project',
      version: '1.0.0'
    }))
    .pipe(gulp.dest('html-documentation'));

});
```

Returns **[stream.Transform](https://nodejs.org/api/stream.html#stream_class_stream_transform)** 
