# Minify step for wercker
This [wercker](http://wercker.com) step minifies static resources like HTML, CSS and JS files.

[![wercker status](https://app.wercker.com/status/777b41e2e1d76a0ef8b13d56da4bdcbb/m "wercker status")](https://app.wercker.com/project/bykey/777b41e2e1d76a0ef8b13d56da4bdcbb)

This step is designed to be used with a static site generator like [Jekyll](http://jekyllrb.com) or [hugo](http://gohugo.io). You can configure it to fit your needs.

## Configuration

All parameters are optional. Don't put them in your *wercker.yml* to use the default values.

* `basedir`: The directory containing the website to be minified. *Default is `public`.*
* `threads`: The number of simultaneous operations. Put this between quotes (e.g. *"4"*). *Default is the number of cores of the host.*
* `htmlargs`: The arguments for [html-minifier](https://github.com/kangax/html-minifier). *Default is `--use-short-doctype --remove-style-link-type-attributes --remove-script-type-attributes --remove-comments --minify-css --minify-js --collapse-whitespace --remove-comments-from-cdata --conservative-collapse --remove-cdatasections-from-cdata`.*
* `yuiargs`: The arguments for [yuicompressor](https://github.com/yui/yuicompressor). *No arguments by default.*
* `html`: Set this to `false` to disable HTML minification. *Default is `true`.*
* `css`: Set this to `false` to disable CSS minification (CSS in HTML files will still be minified if you don't change `html` or `htmlargs`). *Default is `true`*
* `js`: Set this to `false` to disable JS minification (JS in HTML files will still be minified if you don't change `html` or `htmlargs`). *Default is `true`*
* `htmlext`: The extension of the HTML files to be minified. Default is `html`.
* `cssext`: The extension of the CSS files to be minified. Default is `css`.
* `jsext`: The extension of the JS files to be minified. Default is `js`.

### New Wercker (*ewok*) infrastructure example (with Docker)

	box: debian
	build:
	  steps:
	    - samueldebruyn/minify:
	        basedir: _site
	        threads: "3"

### Old Wercker infrastructure example

	box: wercker/default
	build:
	  steps:
	    - samueldebruyn/minify:
	        basedir: _site
	        threads: "3"

## How it works

This script uses [html-minifier](https://github.com/kangax/html-minifier) to minify HTML files and [yuicompressor](https://github.com/yui/yuicompressor) to minify CSS and JS files. This also means that the script installs node, curl and java if they aren't already installed.

The script should work on any OS using *apt-get* or *yum* as package managers.

## Contributing and license

This wercker step is licensed under the MIT License. Create a pull request or an issue to contribute.