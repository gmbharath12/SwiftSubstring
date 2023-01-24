# SwiftSubstring

Write a program to check if strings are rotations of each other. 

> s1 = "ABCD", s2 = "CDAB" -> return `true`

> s1 = "ABCD" and s2 = "ACBD" -> return `false`

Basic idea is to concantenate `s1` with `s1` call it a `s` and check if `s2` is contained in `s1`. Of course if `s1` and `s2` length doesn't match return `false`  

First let's understand how strings work in Swift:


<img width="637" alt="Screenshot 2023-01-23 at 10 57 23 PM" src="https://user-images.githubusercontent.com/1192700/214230266-e8df109e-878f-4b5e-afde-7933ed86c959.png">


Strings got a pretty big overhaul in Swift 4. When you get some substring from a String now, you get a Substring type back rather than a String. Why is this? Strings are value types in Swift. That means if you use one String to make a new one, then it has to be copied over. This is good for stability (no one else is going to change it without your knowledge) but bad for efficiency.

A Substring, on the other hand, is a reference back to the original String from which it came. Here is an image from the documentation illustrating that.

<img width="474" alt="Screenshot 2023-01-23 at 10 57 43 PM" src="https://user-images.githubusercontent.com/1192700/214230303-3bac434c-bf67-4300-82e5-a1f67275000e.png">

No copying is needed so it is much more efficient to use. However, imagine you got a ten character Substring from a million character String. Because the Substring is referencing the String, the system would have to hold on to the entire String for as long as the Substring is around. Thus, whenever you are done manipulating your Substring, convert it to a String.

```
let myString = String(mySubstring)
```
This will copy just the substring over and the memory holding old String can be reclaimed. Substrings (as a type) are meant to be short lived.

Another big improvement in Swift 4 is that Strings are Collections (again). That means that whatever you can do to a Collection, you can do to a String (use subscripts, iterate over the characters, filter, etc).

The following examples show how to get a substring in Swift.

Getting substrings
You can get a substring from a string by using subscripts or a number of other methods (for example, prefix, suffix, split). You still need to use String.Index and not an Int index for the range, though. (See my other answer if you need help with that.)

**Beginning of a string**

You can use a subscript (note the Swift 4 one-sided range):

```let index = str.index(str.startIndex, offsetBy: 5)
let mySubstring = str[..<index] // Hello
```

or `prefix`:
```let index = str.index(str.startIndex, offsetBy: 5)
let mySubstring = str.prefix(upTo: index) // Hello
```
or even easier:

```let mySubstring = str.prefix(5) // Hello ```

**End of a string**

Using `subscripts`:
```
let index = str.index(str.endIndex, offsetBy: -10)
let mySubstring = str[index...] // playground
```

or `suffix`:
```
let index = str.index(str.endIndex, offsetBy: -10)
let mySubstring = str.suffix(from: index) // playground
```

or even easier:
```
let mySubstring = str.suffix(10) // playground
```
Note that when using the suffix(from: index) I had to count back from the end by using -10. That is not necessary when just using suffix(x), which just takes the last x characters of a String.

**Range in a string**
Again we simply use subscripts here.

```
let start = str.index(str.startIndex, offsetBy: 7)
let end = str.index(str.endIndex, offsetBy: -6)
let range = start..<end
let mySubstring = str[range]  // play
```

Converting `Substring` to `String`
Don't forget, when you are ready to save your substring, you should convert it to a String so that the old string's memory can be cleaned up.

```
let myString = String(mySubstring)
```
