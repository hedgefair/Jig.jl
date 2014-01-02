Jig.jl
======

Testing framework for Julia

Proposed API
=======

````julia
using Series, Jig

@runtest Series array io
array:
     index is preserved ....
     conversion is correct ..
     broadcasting is correct ..x.
io:
     readseries reads csv ...
     readseries reads minds xxxx
````

The expected location of test files is in the package's test directory. You can also be a little
clever and name a file all.jl where you include all the test files, thereby making this possible:

````julia

@runtest Series all
pair:
     everything works ....
array:
     index is preserved ....
     conversion is correct ..
     broadcasting is correct ..x.
io:
     readseries reads csv ...
     readseries reads minds xxxx
````
