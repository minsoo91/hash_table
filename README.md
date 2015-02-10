# Hash Table

This is an implementation of Hash Table in Ruby inspired by [a tutorial by Zed Shaw](http://learnrubythehardway.org/book/ex39.html)

The underlying data structure of the HashTable class defined in this piece of code is an array (@store). By default, this array is initialized with a length of 256. Although Ruby supports dynamic arrays, we are hard coding the length of the array to mimic the static nature of arrays in other languages.

Each index of @store contains an empty array upon initialization, representing an empty bucket. A bucket can also be represented by a Linked List data structure, but we are using an array for the sake of simplicity and to take advantage of O(1) lookup time with known index.

The high level concept of a Hash Table is as follows:
- You want to insert, find, and remove key-value pairs as quickly as possible (just like the native Hash class in Ruby!)

Given a key-value pair, a very simple implementation of Hash Table with an array can just convert the key to an index of the array (@store) and insert the value at that index. We would convert the key of the key-value pair to an index by using a Hash function (Why? Among other reasons, not all keys of key-value pairs are integers)

Now here is the problem. It seems extremely difficult to ensure that each index (acquired by running a hash function on a key) of the array (@store) maps exactly to a single value. In other words, unless we have a) an infinitely large array or b) an extremely good hash function that ensures that no two keys return the same hash, it seems almost impossible to prevent the storing of two different key-values within a single bucket. 

The above problem is called collision. When a collision occurs, one key-value pair assigned to a bucket will end up overwriting another key-value pair assigned to the same bucket. That will result in missing data, which is not good!

How do we solve this? We can solve this problem by using something called "buckets". Bucket simply means that instead of directly assigning a value to the index returned by hashing the key, we are going have an array that stores all the values with the same index. Now, we don't have to have an insanely large array or count on the hashing capabilities of a hash function (although a good hash function will always result in fewer collisions) to prevent collisions!