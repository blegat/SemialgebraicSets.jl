# SemialgebraicSets

| **Build Status** |
|:----------------:|
| [![Build Status][build-img]][build-url] |
| [![Codecov branch][codecov-img]][codecov-url] |

Extension of MultivariatePolynomials to semialgebraic sets, i.e. sets defined by inequalities and equalities between polynomials.
The following example shows how to build an [algebraic set/algebraic variety](https://en.wikipedia.org/wiki/Algebraic_variety)
```julia
using TypedPolynomials
@polyvar x y z
# Algebraic variety https://en.wikipedia.org/wiki/Algebraic_variety#/media/File:Elliptic_curve2.png
@set y^2 == x^3 - x
@set x^3 == 2x*y && x^2*y == 2y^2 - x
@set x*y^2 == x*z - y && x*y == z^2 && x == y*z^4
@set x^4*y^2 == z^5 && x^3*y^3 == 1 && x^2*y^4 == 2z
@set x == z^2 && y == z^3
```

Once the algebraic set has been created, you can check whether it is zero-dimensional and if it is the case, you can get the finite number of elements of the set simply by iterating over it, or by using `collect` to transform it into an array containing the solutions.
```julia
V = @set y == x^2 && z == x^3
iszerodimensional(V) # should return false
V = @set x^2 + x == 6 && y == x+1
iszerodimensional(V) # should return true
collect(V) # should return [[2, 3], [-3, -2]]
```

The following example shows how to build an [basic semialgebraic set](http://www.mit.edu/~parrilo/cdc03_workshop/10_positivstellensatz_2003_12_07_02_screen.pdf)
```julia
using TypedPolynomials
@polyvar x y
@set x^2 + y^2 <= 1 # Euclidean ball
# Cutting the algebraic variety https://en.wikipedia.org/wiki/Algebraic_variety#/media/File:Elliptic_curve2.png
@set y^2 == x^3 - x && x <= 0
@set y^2 == x^3 - x && x >= 1
```

[build-img]: https://github.com/JuliaAlgebra/SemialgebraicSets.jl/workflows/CI/badge.svg?branch=master
[build-url]: https://github.com/JuliaAlgebra/SemialgebraicSets.jl/actions?query=workflow%3ACI
[codecov-img]: http://codecov.io/github/JuliaAlgebra/SemialgebraicSets.jl/coverage.svg?branch=master
[codecov-url]: http://codecov.io/github/JuliaAlgebra/SemialgebraicSets.jl?branch=master
