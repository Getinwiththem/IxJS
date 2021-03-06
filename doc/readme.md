# Ix.js <sup>v1.0.5</sup>

# Enumerable object #

The Enumerable object represents a pull based collection.  This class exposes the enumerator, which supports a simple iteration over a collection.  This object also provides a set of methods for querying objects that inherit from the Enumerable class.

## <a id="Enumerable1"></a>`Enumerable Methods`
- [case](#switchCase)
- [catch](#catchException1)
- [concat](#concat1)
- [create](#create)
- [defer](#defer)
- [doWhile](#doWhile)
- [for](#forIn)
- [fromArray](#fromArray)
- [generate](#generate)
- [if](#ifThen)
- [onErrorResumeNext](#onErrorResumeNext1)
- [range](#range)
- [repeat](#repeat1)
- [return](#returnValue)
- [start](#start)
- [using](#using)
- [while](#whileDo)

<!-- div -->

<!-- div -->

## <a id="Enumerable2"></a>`Enumerable Instance Methods`
- [aggregate](#aggregate)
- [all](#all)
- [any](#any)
- [average](#average)
- [bufferWithCount](#bufferWithCount)
- [catch](#catchException2)
- [concat](#concat2)
- [contains](#contains)
- [count](#count)
- [defaultIfEmpty](#defaultIfEmpty)
- [distinct](#distinct)
- [distinctBy](#distinctBy)
- [distinctUntilChanged](#distinctUntilChanged)
- [do](#doAction)
- [elementAt](#elementAt)
- [elementAtOrDefault](#elementAtOrDefault)
- [empty](#empty)
- [finally](#finallyAction)
- [first](#first)
- [firstOrDefault](#firstOrDefault)
- [groupBy](#groupBy)
- [groupJoin](#groupJoin)
- [ignoreElements](#ignoreElements)
- [isEmpty](#isEmpty)
- [join](#join)
- [last](#first)
- [lastOrDefault](#lastOrDefault)
- [max](#max)
- [maxBy](#maxBy)
- [min](#min)
- [minBy](#minBy)
- [onErrorResumeNext](#onErrorResumeNext2)
- [repeat](#repeat2)
- [replay](#replay)
- [retry](#retry)
- [sample](#sample)
- [scan](#scan)
- [select](#select)
- [selectMany](#selectMany)
- [single](#single)
- [singleOrDefault](#singleOrDefault)
- [skip](#single)
- [skipLast](#singleOrDefault)
- [skipWhile](#skipWhile)
- [sum](#sum)
- [switchLatest](#switchLatest)
- [take](#take)
- [takeLast](#takeLast)
- [takeWhile](#takeWhile)
- [throwException](#throwException)
- [toArray](#toArray)
- [where](#where)
- [zip](#zip)


### <a id="switchCase"></a>`Ix.Enumerable.case`
<a href="#switchCase">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/ix.js#L1224-L1233 "View in source") [&#x24C9;][1]

Returns a sequence from a dictionary based on the result of evaluating a selector function, also specifying a default sequence.
An alias for this method is switchCase for browsers <IE9.

#### Arguments
1. `selector` *(Function)*: Selector function used to pick a sequence from the given sources.
2. `sources` *(Object)*: Dictionary mapping selector values onto resulting sequences.
3. [`defaultSource`] *(Enumerable*): Default sequence to return in case there's no corresponding source for the computed selector value; if not provided defaults to empty Enumerable.

#### Returns
*(Enumerable)*: The source sequence corresponding with the evaluated selector value; otherwise, the default source.

#### Example
```js
var source = Ix.Enumerable.case(
	Ix.Enumerable.return(42), {
		42: 'foo',
		24: 'bar'
	}, 
	Ix.Enumerable.return(56));

console.log(source.first());

// => 'foo'
```

* * *

### <a id="catchException"></a>`Ix.Enumerable.catch`
<a href="#catchException">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/ix.js#L998-L1055 "View in source") [&#x24C9;][1]

Creates a sequence by concatenating source sequences until a source sequence completes successfully.  An alias for this method is catchException for browsers <IE9.

#### Arguments
1. `array` *(arguments)*: An arguments array containing Enumerable sequences.  

#### Returns
*(Enumerable)*: Sequence that continues to concatenate source sequences while errors occur.

#### Example
```js
var source = Ix.Enumerable.catch(
	Ix.Enumerable.throw(new Error('first')),
	Ix.Enumerable.throw(new Error('second')),
	Ix.Enumerable.return(42)
);

console.log(source.first());

// => 42
```

* * *

### <a id="concat1"></a>`Ix.Enumerable.concat`
<a href="#concat1">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L2009-L2011 "View in source") [&#x24C9;][1]

Concatenates all given sequences as arguments.

#### Arguments
1. `array` *(arguments)*: An arguments array containing Enumerable sequences.  

#### Returns
*(Enumerable)*: An Enumerable that contains the concatenated elements of the input sequences.

#### Example
```js
var source = Ix.Enumerable.concat(
	Ix.Enumerable.return(42),
	Ix.Enumerable.return(56)
);

source.forEach(function (item) {
	console.log(item);
});

// => 42
// => 56
```

* * *

### <a id="concat2"></a>`concat`
<a href="#concat2">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L790-L799 "View in source") [&#x24C9;][1]

Concatenates two or more sequences.

#### Arguments
1. `other` *(arguments)*: An arguments array containing Enumerable sequences.  

#### Returns
*(Enumerable)*: An Enumerable that contains the concatenated elements of the two (or more) input sequences.

#### Example
```js
var source = Ix.Enumerable.return(42);
var other = Ix.Enumerable.return(56);

var result = source.concat(other);

result.forEach(function (item) {
	console.log(item);
});

// => 42
// => 56
```

Can also be used to provide multiple sequences to be concatenated

#### Example
```js
var source = Ix.Enumerable.return(42);
var other = Ix.Enumerable.return(56);
var other2 = Ix.Enumerable.return(57);

var result = source.concat(other, other2);

result.forEach(function (item) {
	console.log(item);
});

// => 42
// => 56
// => 57
```

* * *

### <a id="create"></a>`Ix.Enumerator.create`
<a href="#create">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L598-L623 "View in source") [&#x24C9;][1]

Creates an state machine that lazily executes an iterator function to update the current value.
Useful for creating lazy evaluated sequences.
See `Enumerable.create` below

#### Arguments
1. `moveNext` *(Function)*: Function that evaluates the next iteration and returns true if the state machine is able to iterate forward, else returns false.
2. `getCurrent` *(Function)*: Function that gets the current value for the state machine.
3. `dispose` *(Function)*: Function that terminates the state machine and deterministically releases any resources held by it.
 
#### Returns
*(Enumerator)*: Enumerator state machine.

#### Example
```js

return Ix.Enumerable.create(function () {
        var current = 0;
        return Ix.Enumerator.create(
            function () {
                return current++ <5;
            },
            function () { return current; },
			function () { console.log('disposed'); }
        );
    });

source.forEach(function (item) {
	console.log(item);
});

// => 1
// => 2
// => 3
// => 4
// => 5
// => disposed
```

### `Ix.Enumerable.create`
[&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L2013-L2021 "View in source") [&#x24C9;][1]

Creates an enumerable sequence based on an enumerator factory function. 
Useful for creating lazy evaluated sequences.
See [Enumerator.create](#create) above.

#### Arguments
1. `getEnumerator` *(Function)*: Enumerator factory function.

#### Returns
*(Enumerable)*: Sequence that will invoke the enumerator factory upon a call to `getEnumerator`.

#### Example
```js

return Ix.Enumerable.create(function () {
        var current = 0;
        return Ix.Enumerator.create(
            function () {
                return current++ <5;
            },
            function () { return current; },
			function () { console.log('disposed'); }
        );
    });

source.forEach(function (item) {
	console.log(item);
});

// => 1
// => 2
// => 3
// => 4
// => 5
// => disposed
```

* * *

### <a id="fromArray"></a> `Ix.Enumerable.fromArray`
<a href="#fromArray">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L2037-L2059 "View in source") [&#x24C9;][1]

Converts an Array to an Enumerable sequence.

#### Arguments
1. `array`: An array to convert to an Enumerable sequence.

#### Returns
*(Enumerable)*: An Enumerable sequence created by the values in the array.

#### Example
```js
var source = Ix.Enumerable.fromArray([42,56]);

source.forEach(function (item) {
	console.log(item);
});

// => 42
// => 56
```

* * *

### <a id="generate"></a> `Ix.Enumerable.generate`
<a href="#generate">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/ix.js#L504-L535 "View in source") [&#x24C9;][1]

Generates a sequence by mimicking a for loop.

#### Arguments
1. `initialState` *(Any)*: Initial state of the generator loop.
2. `condition ` *(Function)* : Loop condition
3. `iterate ` *(Function)*: State update function to run after every iteration of the generator loop.
4. `resultSelector ` *(Function)*: Result selector to compute resulting sequence elements.

#### Returns
*(Enumerable)*: Sequence obtained by running the generator loop, yielding computed elements.

#### Example
```js
var source = Ix.Enumerable.generate(
    0,
	function (x) { return x < 10; },
	function (x) { return x + 1; },
	function (x) { return x * x });

source.forEach(function (item) {
	console.log(item);
});

// => 0
// => 1
// => 4
// => 9
// => 16
// => 25
// => 36
// => 49
// => 64
// => 81
```

* * *

### <a id="join"></a> `join`
<a href="#join">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L1175-L1222 "View in source") [&#x24C9;][1]

Correlates the elements of two sequences based on matching keys. 

#### Arguments
1. `inner` *(Enumerable)*: The sequence to join to the first sequence.
2. `outerKeySelector` *(Function)* : A function to extract the join key from each element of the first sequence.
3. `innerKeySelector` *(Function)*: A function to extract the join key from each element of the second sequence.
4. `resultSelector` *(Function)*: A function to create a result element from two matching elements.

#### Returns
*(Enumerable)*: An Enumerable that has elements that are obtained by performing an inner join on two sequences.

#### Example
```js

var outer = Ix.Enumerable.fromArray([
				{number : 0, word : "zero"},
		        {number : 1, word : "one"},
		        {number : 2, word : "two"},
		        {number : 3, word : "three"}
	        ]);
var inner = Ix.Enumerable.fromArray([
				{number : 1, word : "uno"},
		        {number : 2, word : "dos"},
		        {number : 3, word : "tres"},
		        {number : 4, word : "cuatro"}
	        ]);

var result = outer.join(inner, 
		function(eng) { return eng.number; }, 
		function(esp) { return esp.number; }, 
		function(eng, esp) { 
			return {
				english : eng.word, 
				spanish : esp.word 
				};
		});

result.forEach(function (item) {
	console.log(item);
});

// => {english:"one", spanish:"uno"},
// => {english:"two", spanish:"dos"}
// => {english:"three", spanish:"tres"}
```

* * *

### <a id="range"></a> `Ix.Enumerable.range`
<a href="#range">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L2086-L2108 "View in source") [&#x24C9;][1]

Generates a sequence of integral numbers within a specified range.

#### Arguments
1. `start` *(Number)*: The value of the first integer in the sequence.
2. `count ` *(Number)* : The number of sequential integers to generate.


#### Returns
*(Enumerable)*: An Enumerable that contains a range of sequential integral numbers.

#### Example
```js
var source = Ix.Enumerable.range(0, 3);

source.forEach(function (item) {
	console.log(item);
});

// => 0
// => 1
// => 2
```

* * *

### <a id="repeat"></a> `Ix.Enumerable.repeat`
<a href="#repeat">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L2110-L2132 "View in source") [&#x24C9;][1]

Generates a sequence that contains one repeated value.

#### Arguments
1. `value` *(Any)*: The value to be repeated.
2. `repeatCount` *(Number)* : The number of times to repeat the value in the generated sequence.


#### Returns
*(Enumerable)*: An Enumerable that contains a repeated value.

#### Example
```js
var source = Ix.Enumerable.repeat(42, 3);

source.forEach(function (item) {
	console.log(item);
});

// => 42
// => 42
// => 42
```

* * *

### <a id="return"></a> `Ix.Enumerable.return`
<a href="#return">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L2061-L2084 "View in source") [&#x24C9;][1]

Returns a sequence with a single element.
An alias for this method is `returnValue` for browsers <IE9.

#### Arguments
1. `value` *(Any)*: Single element of the resulting sequence.

#### Returns
*(Enumerable)*: Sequence with a single element.

#### Example
```js
var result = Enumerable.return(42);

result.forEach(function (item) {
	console.log(item);
});

// => 42
```

* * *

### <a id="scan"></a> `scan`
<a href="#scan">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/ix.js#L803-L861 "View in source") [&#x24C9;][1]

Generates a sequence of accumulated values by scanning the source sequence and applying an accumulator function.

#### Arguments
1. `seed` *(Any)*: Accumulator seed value.
2. `accumulator` *(Function)*: Accumulation function to apply to the current accumulation value and each element of the sequence.

#### Returns
*(Enumerable)*: Sequence with all intermediate accumulation values resulting from scanning the sequence.

#### Example
```js
var source = Ix.Enumerable.fromArray([0,1,2,3,4])
	.scan(0, function(accumulation, currentValue){ 
		return accumulation+currentValue;
	})

source.forEach(function (item) {
	console.log(item);
});

// => 0
// => 1
// => 3
// => 6
// => 10
```

* * *

### <a id="select"></a> `select`
<a href="#select">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L1437-L1470 "View in source") [&#x24C9;][1]

Projects each element of a sequence into a new form by incorporating the element's index.

####Alias
 * map

#### Arguments
1. `selector` *(Function)*: A transform function to apply to each source element; the second parameter of the function represents the index of the source element.
2. `thisArg` *(Any)*: An optional scope for the selector.

#### Returns
*(Enumerable)*: An Enumerable whose elements are the result of invoking the transform function on each element of source.

#### Example
```js
var source = Ix.Enumerable.fromArray([0,1,2,3,4])
	.select(function(item){ 
		return item+5;
	})

source.forEach(function (item) {
	console.log(item);
});

// => 5
// => 6
// => 7
// => 8
// => 9
```

* * *

### <a id="selectMany"></a> `selectMany`
<a href="#selectMany">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L1472-L1520 "View in source") [&#x24C9;][1]

Projects each element of a sequence to an Enumerable, flattens the resulting sequences into one sequence, and invokes a result selector function on each element therein.
The index of each source element is used in the intermediate projected form of that element.

>Note: `selectMany` is the term taken from Microsoft's LINQ (Language Integrated Query) technology. The more popular term for a method like this is `flatMap`.

####Alias
 * flatMap _TBD_

#### Arguments
1. `collectionSelector` *(Function)*: A transform function to apply to each source element; the second parameter of the function represents the index of the source element.
2. `resultSelector` *(Function)*: An optional transform function to apply to each element of the intermediate sequence.

#### Returns
*(Enumerable)*: An Enumerable whose elements are the result of invoking the one-to-many transform function `collectionSelector` on each element of source and then mapping each of those sequence elements and their corresponding source element to a result element.

#### Example
```js

//From the sequence [1,2,3]
var source = Ix.Enumerable.fromArray([1,2,3])
	.selectMany(function(item){
		//Produce the inner sequences of [1], [2,2] and [3,3,3] 
		return Ix.Enumerable.repeat(item, item)
	})

source.forEach(function (item) {
	console.log(item);
});

// => 1
// => 2
// => 2
// => 3
// => 3
// => 3
```

* * *

### <a id="toArray"></a> `toArray`
<a href="#toArray">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L1784-L1802 "View in source") [&#x24C9;][1]

Creates an array from an Enumerable.

#### Arguments
None

#### Returns
*(Array)*: An array that contains the elements from the input sequence.

#### Example
```js
var source = Ix.Enumerable.return(42)
	.toArray()

console.log(source);

// => [ 42 ]
```


* * *

### <a id="zip"></a> `zip`
<a href="#zip">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/IxJS/blob/master/l2o.js#L1966-L2002 "View in source") [&#x24C9;][1]

Applies a specified function to the corresponding elements of two sequences, which produces a sequence of the results.

#### Arguments
 1. `right` *(Enumerable)*: The second sequence to merge.
 2. `selector` *(Function)*: A function that specifies how to merge the elements from the two sequences.

#### Returns
*(Enumerable)*: An Enumerable that contains merged elements of two input sequences.

#### Example
```js
var left = Ix.Enumerable.fromArray([1,2,3]);
var right = Ix.Enumerable.fromArray(['a','b','c']);

var result = left.zip(right, 
	function(lhs, rhs){
		return {left:lhs, right:rhs};
	});

result.forEach(function (item) {
	console.log(item);
});

// => { left: 1, right: 'a' }
// => { left: 2, right: 'b' }
// => { left: 3, right: 'c' }
```

* * *
