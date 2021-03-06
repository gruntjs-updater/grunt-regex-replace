# grunt-regex-replace

[![NPM](https://nodei.co/npm/grunt-regex-replace.png?downloads=true)](https://npmjs.org/package/grunt-regex-replace)

Grunt plugin to search and replace text content of files based on regular expression patterns

## Getting Started
Install this grunt plugin next to your project's [grunt.js gruntfile][getting_started] with: 

```
npm install --save-dev grunt-regex-replace
```

Then add this line to your project's `grunt.js` gruntfile:

```javascript
grunt.loadNpmTasks('grunt-regex-replace');
```

[grunt]: http://gruntjs.com/
[getting_started]: https://github.com/gruntjs/grunt/blob/master/docs/getting_started.md

## How to use
Here is an sample of the definition within the object passed to grunt.initConfig 

###Sample Code

    "regex-replace": {
        foofoo: { //specify a target with any name
            src: ['foo/bar.js'],
            actions: [
                {
                    name: 'bar',
                    search: '(^|\\s)console.log',
                    replace: '//console.log',
                    flags: 'g'
                },{
                    name: 'foo',
                    search: 'var v = \'[^\']*\';',
                    replace: 'var v = \'<%= pkg.release.version_code %>\';',
                    flags: ''
                },{
                   name: 'foobar',
                   search: new RegExp('\\w+'),
                   replace: function() {
                   	    return 'foofoo';
                   }
                }
            ]
        }
    }

### src property
Takes the path to the files relative to the grunt file, it accepts strings as well as an array of file paths.
Also supports templates, e.g
      
    src: 'customisation/*.js',
    src: '**/*.js',
    src: ['foo/bar.js','foo/foo.js'],
    src: ['<%= pkg.id %>/bar.js', 'foo/foo.js']
      
### actions property (array | function)
Accepts an array of objects or a function (which returns an array of objects) representing the actions to take place. Each action contains an optional name property, a search property, a replace property and 
a flags property. Example af an object.
      
    {
        name: 'foo',
        search: '(^|\\s)console.log',
        replace: '//console.log',
        flags: 'gi'
    }
      
    {
        name: 'bar',
        search: /\\w+/g, //also accepts new RegExp()
        replace: function() {
            return 'foo';
        }
    }
#### name property
A string value 

#### search property (regexp | substr)
A regular expression string or object defining the text content to be found.

#### replace property (substr | function)
A string / regular expression pattern or function to replace the text content.
For the replace function, values that match the parenthesized substring matches are passed as arguments
```
    {
        search: new RegExp(/(\w+)\s(\w+)/),
        replace: function(arg1, arg2, ... argN) {
          // arg1 is the full string matched
          // arg2 is the first parenthesized substring match
          // argN is the Nth parenthesized substring match
        }
    }
```
See [MDN Documentation](https://developer.mozilla.org/en/docs/Web/JavaScript/Guide/Regular_Expressions#Using_parenthesized_substring_matches) for details on "using parenthesized substring matches."

#### flags property
Regular expressions options (ie gmi). if the flags property is not defined it defaults to 'g'. To specify no options, set the
flags to empty string (ie flags : '').

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [grunt][grunt].

## Release History

v0.1.0 - First Release

v0.1.1 - 

v0.1.2 - Changes to readme

v0.2.1 - Updated to support grunt 0.4.x

v0.2.2 - version fixes

v.0.2.3 - task format fixes for compatibilty with 0.4.0 ,

v.0.2.4 - added name property, search property now supports regexp object, replace property now supports functions. 

v.0.2.5 - fix /bin not exist error

v.0.2.6 - Support for file globbing patterns.

v.0.2.7 - Support for passing a function to the action property, Updated documentation for using parenthesized substring matches

## License
Copyright (c) 2012 Hubert Boma Manilla  
Licensed under the MIT license.
=======
