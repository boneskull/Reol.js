# Reol.js

_Keep an array of objects indexed by field, for super-fast retrieval._

Have you ever created an array, filled it with objects, and then wanted to sometimes 
retrieve the objects based on "id", but sometimes based on "slug"? Did you simple 
create a `find(key, value)` method? That's okay, I've done it too. Just keep reading 
though, you'll love this module.

Reol lets you create an array of objects pretty much like you've always done, but 
you can also specify fields to be indexed. The advantage of indexes is that 
retrieving an object based on the value of an indexed field is a lot faster.


### How fast?

About twice as fast for tiny arrays (10 elements) and infintely faster for large (10000 elements) arrays.

See [this jsperf test](http://jsperf.com/reol-js-vs-naive-search) for exact data
and to verify in your own environment.


## Installation

If you're using node, just do `npm install reol`. Other may simply copy index.js and put it where you like it. Reol works in all js environments (I think), including commonJS (node) and AMD (requireJS) as well as old-fashioned `<script src="dist/reol.min.js"></script>`-style.

**Compatibility note:** Reol depends on a global JSON object. Use a polyfill if you wish to support older browsers (<IE8).


## Example

```javascript
// Supports deep indexes
var list = new Heap({
  test: true,
  'parent.child': true
});

// Chain adds if you feel like it
list.add({
  test: 'meow',
  parent: {
    child: 'baahh'
  }
});

// Indexing works even with undefined and complex values, though the latter is not recommended
list.add({
  test: function(){
    console.log("seriously try to not do this");
  }
});

// Un-indexed fields also work
list.add({
  woot: 'mooo'
});

// Find all matches
list.find({ test: 'meow' });

// findOne will speed up best-case scenarios for queries on un-indexed fields
list.findOne({ woot: 'mooo' });
```


## Caveats

Current version does not support non-unique indexes or queries on multiple fields.
This will be added, see [Todo](#todo).


## Todo

_Ordered by likeliness and simpleness to implement._

* .get() based on array index (insert-order)
* non-unique indexing (with option to enable)
* Multi-field queries
* Compound index
* Sparse index
* .remove() stuff
* option to not auto-serialize objects but use (possibly custom) toString instead
* A way too hook in external functionality, for example persisting data in localStorage


## Contribution

I just threw this together in a few hours to solve my problem at hand. If you
want to pick something on the todo list or have an opinion on how some method
should be implemented (or maybe not implemented at all), please don't hestitate
to create an issue, submit a pull request, tweet/email me or whatever.

For example I'm at the moment not sure if I should keep Raol as a very small
and basic utility or extend it with rather complex (but some might argue essential)
functionality such as .remove() and advanced indexing.

## License

MIT