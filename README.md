[![Build Status](https://travis-ci.org/deckarep/golang-set.png?branch=master)](https://travis-ci.org/deckarep/golang-set)
[![GoDoc](https://godoc.org/github.com/deckarep/golang-set?status.png)](http://godoc.org/github.com/deckarep/golang-set)

golang-set
==========

A simple set type for the Go language.  Until Go has sets built-in like maps, slices, and channels...use this.

Coming from Python one of the things I miss is the superbly wonderful set collection.  This is my attempt to mimic the primary features of the set from Python.
You can of course argue that there is no need for a set in Go, otherwise the creators would have added one to the standard library.  To those I say simply ignore this repository
and carry-on and to the rest that find this useful please contribute in helping me make it better by:

* Helping to make more idiomatic improvements to the code.
* Helping to increase the performance of it. ~~(So far, no attempt has been made, but since it uses a map internally, I expect it to be mostly performant.)~~
* Helping to make the unit-tests more robust and kick-ass.
* Helping to fill in the [documentation.](http://godoc.org/github.com/deckarep/golang-set)
* Simply offering feedback and suggestions.  (Positive, constructive feedback is appreciated.)

I have to give some credit for helping seed the idea with this post on [stackoverflow.](http://programmers.stackexchange.com/questions/177428/sets-data-structure-in-golang)

Please see the unit test file for additional usage examples.  The Python set documentation will also do a better job than I can of explaining how a set typically [works.](http://docs.python.org/2/library/sets.html)    Please keep in mind 
however that the Python set is a built-in type and supports additional features and syntax that make it awesome.  This set for Go is nowhere near as comprehensive as the Python set
also, ~~this set has not been battle-tested or used in production~~.  Also, this set is not goroutine safe.  The rationale for this is the same reasons that the built-in
maps and slices are not thread-safe.  Performance is favored over synchronization because this largely depends on your application requirements.  If you need synchronization,
perhaps use a channels for a high-level solution or use mutex and embedding for a more low-level solution.
 
Examples but not exhaustive:

```go
requiredClasses := NewSet()
requiredClasses.Add("Cooking")
requiredClasses.Add("English")
requiredClasses.Add("Math")
requiredClasses.Add("Biology")

scienceSlice := []interface{}{"Biology", "Chemistry"}
scienceClasses := NewSetFromSlice(scienceSlice)

electiveClasses := NewSet()
electiveClasses.Add("Welding")
electiveClasses.Add("Music")
electiveClasses.Add("Automotive")

bonusClasses := NewSet()
bonusClasses.Add("Go Programming")
bonusClasses.Add("Python Programming")

//Show me all the available classes I can take
allClasses := requiredClasses.Union(scienceClasses).Union(electiveClasses).Union(bonusClasses)
fmt.Println(allClasses) //Set{Cooking, English, Math, Chemistry, Welding, Biology, Music, Automotive, Go Programming, Python Programming}


//Is cooking considered a science class?
fmt.Println(scienceClasses.Contains("Cooking")) //false

//Show me all classes that are not science classes, since I hate science.
fmt.Println(allClasses.Difference(scienceClasses)) //Set{Music, Automotive, Go Programming, Python Programming, Cooking, English, Math, Welding}

//Which science classes are also required classes?
fmt.Println(scienceClasses.Intersect(requiredClasses)) //Set{Biology}

//How many bonus classes do you offer?
fmt.Println(bonusClasses.Size()) //2

//Do you have the following classes? Welding, Automotive and English?
fmt.Println(allClasses.ContainsAll("Welding", "Automotive", "English")) //true
```

Thanks!

-Ralph

[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/deckarep/golang-set/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

[![Analytics](https://ga-beacon.appspot.com/UA-42584447-2/deckarep/golang-set)](https://github.com/igrigorik/ga-beacon)


