flow-iqr
========

Reduce transform stream which computes the interquartile over a stream of numeric data.

Note: in order to calculate the interquartile range exactly, all data must be buffered into memory. As a result, this stream acts as a sink. Use caution when applying the transform to large datasets.


## Installation

``` bash
$ npm install flow-iqr
```


## Examples

``` javascript
var eventStream = require( 'event-stream' ),
	qStream = require( 'flow-iqr' );

// Create some data...
var data = new Array( 1000 );
for ( var i = 0; i < data.length; i++ ) {
	data[ i ] = Math.round( Math.random() * 100 );
}

// Create a readable stream:
var readStream = eventStream.readArray( data );

// Create a new stream:
var stream = qStream()
	.stream();

// Create a pipeline:
readStream.pipe( stream )
	.pipe( eventStream.map( function( d, clbk ) {
		clbk( null, d.toString() );
	}))
	.pipe( process.stdout );
```

## Tests

Unit tests use the [Mocha](http://visionmedia.github.io/mocha) test framework with [Chai](http://chaijs.com) assertions.

Assuming you have installed Mocha, execute the following command in the top-level application directory to run the tests:

``` bash
$ mocha
```

All new feature development should have corresponding unit tests to validate correct functionality.


## License

[MIT license](http://opensource.org/licenses/MIT). 


---
## Copyright

Copyright &copy; 2014. Athan Reines.

