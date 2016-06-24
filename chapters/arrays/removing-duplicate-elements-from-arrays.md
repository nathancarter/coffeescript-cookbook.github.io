---
layout: recipe
title: Removing Duplicate Elements from Arrays
chapter: Arrays
---
## Problem

You want to remove duplicate elements from an array.

## Solution

{% highlight coffeescript %}
Array::unique = ->
  output = {}
  output[@[key]] = @[key] for key in [0...@length]
  value for key, value of output

[1,1,2,2,2,3,4,5,6,6,6,"a","a","b","d","b","c"].unique()
# => [ 1, 2, 3, 4, 5, 6, 'a', 'b', 'd', 'c' ]
{% endhighlight %}

## Discussion

There are many implementations of the `unique` method in JavaScript. This one is based on "The fastest method to find unique items in array" found [here](http://www.shamasis.net/2009/09/fast-algorithm-to-find-unique-items-in-javascript-array/).

**Warning:** This fast solution assumes that the elements of your array can be distinguished by converting each to a string, and comparing those strings.  That may not be the case for your array; for example, in the array `[{a:1},{b:1}]`, both elements convert to strings as `[object Object]`, and so this solution will treat them as equal, and filter out the first of the two.  Also, in the array `[1,"1"]`, both elements are the same when considered as strings, and so it will become `["1"]`.  If your array may pose this problem, use an algorithm that incorporates an equality function appropriate to your array elements.  If your array contains only strings or only numbers, the function written above will work fine.

**Note:** Although it's quite common in languages like Ruby, extending native objects is often considered bad practice in JavaScript (see: [Maintainable JavaScript: Don’t modify objects you don’t own](http://www.nczonline.net/blog/2010/03/02/maintainable-javascript-dont-modify-objects-you-down-own/); [Extending built-in native objects. Evil or not?](http://perfectionkills.com/extending-built-in-native-objects-evil-or-not/)).


