# Javascript-Obfuscation-Tests
A series of experments with javascript obfuscation

##Methods Employed
This experiment uses several obfuscation techniques that do not depend on whitespace removal, and can be implemented automatically.

Joke: "How do you outrun a bear?" Answer: "I don't have to outrun a bear, I only have to outrun you!"

Note: Obfuscation is only a tactic to increase the time needed for a human to analyze code, especially in JavaScript where all clients receive a copy of the source code. Obfuscation is most useful to hide the purpose of a page or function. It is only security by obscurity, or not much security at all.

Challenge: If you can find the purpose of index.html please send me your guess. If you guess correctly, I will reveal it here.

###Padded Heap
When a static number is needed, a large padded heap can overwhelm important numbers.
To implement, create a long array of random numbers. When an index or static number is needed, choose a semi-random instance of the number you would like to implement, then call it from the array, or an array lookup function.

Simple Example:
```javascript
var importantIndex = 1;
```

Becomes:
```javascript
var a = [21,5,23,25,10,25,12,9,8,1,20,12,24,8,13,20,1,16,21,7,17,0,8,8,18]; //global array
function b(ba,bb){ //global function
  return ba[bb];
}
var c = b(a,9); //local usage
```

To my knowledge, this technique can also be used with strings or any other type.

###Numbers and Factorization
When a static number is needed, you can factorize a number, or reduce it to a set of basic math computations that are easy for a computer, but time-consuming for a person.

Simple example:
```javascript
var importantNumber = 517;
```

Becomes:
```javascript
var a = Math.pow(2,8) + (3*5*17) + 6;
```

###Function and Variable naming
Changing the naming of functions and variables is an obvious technique, but can quickly become overwhelming for a person to memorize. This is not a new technique, but an important one to note.

Simple example:
```javascript
var importantNumber = 517;
```

Becomes:
```javascript
var a = 517;
```

###Characters and ASCII codes
If short static strings are needed, they can be obscured by converting numbers to ascii characters.

Note: This should not be used to obscure anything similar to a password or key, these should never appear in any form in code executed by a client.

Simple example:
```javascript
var importantString = 'secret';
```

Becomes:
```javascript
function a(aa,ab){ //Global function, also see 'Parameter padding'
return String.fromCharCode(aa);
}
var b = a(115,15) + a(101,489) + (99,18) + a(114,82910) + a(101,48) + a(114,46);
```

###Parameter padding
When creating functions, you may choose to add extra bogus parameters even if not needed. I prefer to use the max number of needed parameters on all functions. The useful parameter index can be randomized.

Simple example:
```javascript
var multiplied = multiply(1);
function multiply(number){
	return number * 100;
}
```

Becomes:
```javascript
var a = b(12,3,1,4,13,3,15,2);
function b(ba,bb,bc,bd,be,bf,bg){
	return bc * 100;
}
```

###Base64 Encoding
JavaScript can also be encoded as a base64 string and embedded in html, a fairly simple technique.

Example:
```html
<script type="text/javascript" href="data:text/javascript;base64,JChkb2N1bWVudCkucmVhZHkoZnVuY3Rpb24oKXthbGVydCgiSGVsbG8gV29ybGRzISIpfSk7"></script>
```

###Nesting
All of the above techniques are fairly simple to observe the intent of the programmer, but when nested the intent is quite easily lost.

While a few levels of nesting can obscure the intent of code, step by step debugging can quickly 

###Extra Functions
Extraneous functions can also be added to obscure important functions. All of the above techniques can be compounded as long as desired.

Nested functions can also contribute an ineffective value to any of the above to obscure even further. Imagine 10 nested functions that compute (0+0).

However, by analyzing functions one can find the number of dependencies (functions, sub-functions, global arrays). The greater number of dependencies can indicate the importance of any function. So, red herring functions should have similar level of obfuscation to the function(s) you wish to obscure.

### End Game
All of this can be reduced into this: obfuscation as compute time. The time needed for a person to compute a obscured function is almost exponential, but for a computer is closer to linear. 

If you use 1 layer of obfuscation or 10,000, it is a computational arms race, one that any modern web browser can easily win. But, a specialized tool (like a browser) can also easily undo all complexity and make the the abstraction compute. 

In conclusion, real secrets can't be obscured (keys, passwords), they are easily enough to deduce. But, the intention of code is much easier to hide.

