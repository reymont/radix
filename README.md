# radixtrie

An implementation of the [radix trie data structure](http://en.wikipedia.org/wiki/Radix_tree) in Go

## Usage

Get the package:

	$ go get github.com/sauerbraten/radixtrie

Import the package:

	import (
		"github.com/sauerbraten/radixtrie"
	)

You can use the radixtrie as a key-value structure, where every node's can have its own value (as shown in the exmaple below), or you can of course just use it to look up strings, like so:

	trie := radixtrie.New()
	trie.Insert("foo", true)
	fmt.Printf("foo is contained: %v\n", trie.Find("foo"))


### Example

This example code is taken from the radixtrie_test.go file

	package main
	
	import (
		"github.com/sauerbraten/radixtrie"
		"fmt"
	)
	
	func main() {
		// create new trie
		trie := radixtrie.New()
		
		// insert some strings
		trie.Insert("abc", "value 1")
		trie.Insert("a", "value 2")
		trie.Insert("abd", []byte("value 3"))
		trie.Insert("b", 4)
		
		// print trie structure, the parameter sets the initial level of indentation
		trie.Print(0)
		
		// delete some strings, even strings not contained
		trie.Delete("c")
		trie.Delete("b")
		trie.Delete("ab")
		
		// print again, notice the changes:
		// 'b' is gone, 'ab' is no longer an end note, means it is no longer contained as a string
		trie.Print(0)
		
		// use Find() to check if a string is contained in the trie
		fmt.Printf("'a' holds: %v\n", trie.Find("a"))
		fmt.Printf("'c' holds: %v\n", trie.Find("c"))
		fmt.Printf("'abd' holds: %v\n", trie.Find("abd"))
	}

This example should print the following:

	''  end: <nil>
	'a'  end: value 2
		'b'  end: <nil>
			'c'  end: value 1
			'd'  end: [118 97 108 117 101 32 51]
	'b'  end: 4
	''  end: <nil>
		'a'  end: value 2
			'b'  end: <nil>
				'c'  end: value 1
				'd'  end: [118 97 108 117 101 32 51]
	'a' holds: value 2
	'c' holds: <nil>
	'abd' holds: [118 97 108 117 101 32 51]

### Documentation

For full package documentation, visit http://go.pkgdoc.org/github.com/sauerbraten/radixtrie.

## License

This code is licensed under the MIT License:

	Copyright (C) 2012 Alexander Willing
	
	Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), 
	to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, 
	and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
	
	The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
	
	THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, 
	FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, 
	WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.