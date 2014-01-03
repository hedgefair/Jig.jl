[![Build Status](https://travis-ci.org/milktrader/Jig.jl.png)](https://travis-ci.org/milktrader/Jig.jl)

Jig.jl
======

Testing framework for Julia

The `@runtest` macro takes a package name and any number of valid test files. It expects the 
test files to be in the `/test` directory and to be appended by `.jl`. If the test file does
not use Jig macros for added colorful dots, the test should pass silently.

````julia
using Jig

@runtest Stats means variability instats
means:
variability:
intstats:
````

If Jig macros are used in the test file, added feedback is supported.

````julia
@runtest Jig foo bar

foo:
      foo is foo  ..
      foo is not bar  .x

bar:
      bar is bar  xx.
      bar is not qux  ..x
````
Success is indicated by a green dot, and failure by a red x. In the toy example above, the
`@context` macro was called first to print a string about what is being tested. The result
of "foo is foo" is two successful tests. The tests are assertions passed to the `@jtest` macro
inside the `test/foo.jl` file. 

As a clever trick, a file can be placed in the package's test directory named `all.jl` to run all the 
tests. The `all.jl` file simply calls `include` on test files to be included in the suite. This is
customizable of course, and the file can be called whatever the package author deems useful.

````julia
@runtest Jig all
all:
      foo is foo  ..
      foo is not bar  .x

      bar is bar  xx.
      bar is not qux  ..x
````

In this case, the contents of `all.jl` is simply this:

````julia
include("foo.jl")
include("bar.jl")
````

Jig includes a nested module named `Quant` that provides objects and constants useful to testing packages
in the JuliaQuant organization. This module must be called specifically to get those objects and constants.

````julia
julia> using Jig.Quant, Series

julia> cl |> percentchange |> tail |> head
1-element Array{SeriesPair{Date{ISOCalendar},Float64},1}:
 1980-01-04  0.012355065576886993
````
