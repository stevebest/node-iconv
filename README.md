# node-iconv

Text recoding in JavaScript for fun and profit!

## Usage

Encode from one character encoding to another:

	// convert from UTF-8 to ISO-8859-1
	var Buffer = require('buffer').Buffer;
	var Iconv  = require('./iconv').Iconv;
	var assert = require('assert');
	
	var iconv = new Iconv('UTF-8', 'ISO-8859-1');
	var buffer = iconv.convert('Hello, world!');
	var buffer2 = iconv.convert(new Buffer('Hello, world!'));
	assert.equals(buffer.inspect(), buffer2.inspect());
	// do something useful with the buffers

Look at test.js for more examples and node-iconv's behaviour under error conditions.

## Compiling

In the Platonic realm one only needs to type:

	node-waf

In the real world, however, node-waf appears to be broken more often than not
and you will have to compile the source by hand. Fear not, it's easier than it sounds:

	export NODE_PATH=/path/to/nodejs
	g++ -I$NODE_PATH/include/node -O2 -fPIC -shared -Wall -ansi -o iconv.node iconv.cc

There. That wasn't so bad, was it?

## Notes

EINVAL is raised when the input ends in a partial character sequence. This is a feature,
not a bug. 