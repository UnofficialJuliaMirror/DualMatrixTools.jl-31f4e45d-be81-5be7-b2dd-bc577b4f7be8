# DualMatrixTools.jl

<p>
  <a href="https://briochemc.github.io/DualMatrixTools.jl/stable">
    <img src=https://img.shields.io/badge/docs-stable-blue.svg>
  </a>
  <a href="https://travis-ci.com/briochemc/DualMatrixTools.jl">
    <img alt="Build Status" src="https://travis-ci.com/briochemc/DualMatrixTools.jl.svg?branch=master">
  </a>
  <a href="https://travis-ci.org/briochemc/DualMatrixTools.jl">
    <img alt="Build Status" src="https://travis-ci.org/briochemc/DualMatrixTools.jl.svg?branch=master">
  </a>
  <a href='https://coveralls.io/github/briochemc/DualMatrixTools.jl?branch=master'>
    <img src='https://coveralls.io/repos/github/briochemc/DualMatrixTools.jl/badge.svg?branch=master' alt='Coverage Status' />
  </a>
  <a href="https://codecov.io/gh/briochemc/DualMatrixTools.jl">
    <img src="https://codecov.io/gh/briochemc/DualMatrixTools.jl/branch/master/graph/badge.svg" />
  </a>
  <a href="https://github.com/briochemc/DualMatrixTools.jl/blob/master/LICENSE">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg">
  </a>
</p>

This package provides an overloaded `factorize` and `\` that work with dual-valued arrays.

It uses the dual type defined by the [DualNumbers.jl](https://github.com/JuliaDiff/DualNumbers.jl) package.
The idea is that for a dual-valued matrix

<a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;M&space;=&space;A&space;&plus;&space;\varepsilon&space;B" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;M&space;=&space;A&space;&plus;&space;\varepsilon&space;B" title="M = A + \varepsilon B" /></a>,

its inverse is given by

<a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;M^{-1}&space;=&space;(I&space;-&space;\varepsilon&space;A^{-1}&space;B)&space;A^{-1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;M^{-1}&space;=&space;(I&space;-&space;\varepsilon&space;A^{-1}&space;B)&space;A^{-1}" title="M^{-1} = (I - \varepsilon A^{-1} B) A^{-1}" /></a>.

Therefore, only the inverse of <a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;A" title="A" /></a> is required to evaluate the inverse of <a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;M" title="M" /></a>.
This package makes available a `DualFactors` type which containts the factors of <a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;A" title="A" /></a> and the non-real parts of <a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;M" title="M" /></a>, and overloads `factorize` to create an instance of `DualFactors`, which can then be called with `\` to efficiently solve dual-valued linear systems of the type <a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;M&space;x&space;=&space;b" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;M&space;x&space;=&space;b" title="M x = b" /></a>. 

This package should be useful for evaluation of second derivatives of functions that use `\` (e.g., with iterative solvers).
Note the same idea extends to hyper dual numbers (see the [HyperDualMatrixTools.jl](https://github.com/briochemc/HyperDualMatrixTools.jl) package).

## Usage

- Create your dual-valued matrix `M`:
    ```julia
    julia> M = A + ε * B
    ```

- Factorize `M`:
    ```julia
    julia> Mf = factorize(M)
    ```

- Apply `\` to solve systems of the type `M * x = b`
    ```julia
    julia> x = Mf \ b
    ```




