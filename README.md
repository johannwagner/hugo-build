# hugo-build

A docker container to build, test and minify hugo websites with wercker.

[![docker](http://dockeri.co/image/samueldebruyn/hugo-build "docker")](https://registry.hub.docker.com/u/samueldebruyn/hugo-build/)

## What this container is for

This container is ideally used in a [wercker](http://wercker.com) step to build a static site made with [hugo](http://gohugo.io). You can also use it to check your website for dead links and syntax errors and to minify the generated code.

## Packages

The following packages and its dependencies are installed:

* curl
* git
* [html-minifier](https://github.com/kangax/html-minifier) (Node.js)
* [html-proofer](https://github.com/gjtorikian/html-proofer) (Ruby)
* hugo
* [yuicompressor](https://github.com/yui/yuicompressor) (Java)
* wget

## Recommended wercker steps

* [samueldebruyn/minify](https://app.wercker.com/#applications/55b127f1f32b86a9291fe992/tab/details)
* [kyleboyle/html-proofer-test](https://app.wercker.com/#applications/54e78c6cd9b14636630e8c10/tab/details)

## Example *wercker.yml*

*This is taken from [my own hugo site](https://github.com/SamuelDebruyn/chipsncookies-site).*

	build:
	  box: samueldebruyn/hugo-build
	  steps:
	    - script:
	        name: initialize git submodules
	        code: |
	            git submodule update --init --recursive
	    - script:
	        name: build with hugo
	        code: |
	            hugo
	    - samueldebruyn/minify
