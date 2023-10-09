
<!-- README.md is generated from README.Rmd. Please edit that file -->

# moggy <img src="man/figures/logo.png" align="right" width = "40%"/>

<!-- badges: start -->

![](https://img.shields.io/badge/cool-useless-green.svg)
![](https://img.shields.io/badge/status-VeryAlpha-orange.svg)
<!-- badges: end -->

`{moggy}` is a package for creating markdown documents from scratch
without using a template.

My use-case for this package is to create markdown documentation
directly from meta-information.

The completion of this package is proportional to the quality of the cat
image in the logo.

## Installation

You can install from [GitHub](https://github.com/coolbutuseless/moggy)
with:

``` r
# install.package('remotes')
remotes::install_github('coolbutuseless/moggy')
```

## Example

``` r
library(moggy)

doc <- MarkdownDoc$new()
doc$h1("First doc")
doc$add("Now is the time\n\nThe time is now")
doc$h2("Subsection goes here")
doc$table(head(mtcars))
doc$h1("A list of all my failings:")

words <- readLines("/usr/share/dict/words", n = 5)
doc$itemize(words)

doc$h2("Let me count the ways")
doc$enumerate(c("One", "Two", "Three", "Four", "Get on the Dance Floor"))
doc$code(r"(
  x <- 5
  x + 1
)"
)

doc
```

    # First doc 

    Now is the time

    The time is now

    ## Subsection goes here 

    |                  |  mpg| cyl| disp|  hp| drat|    wt|  qsec| vs| am| gear| carb|
    |:-----------------|----:|---:|----:|---:|----:|-----:|-----:|--:|--:|----:|----:|
    |Mazda RX4         | 21.0|   6|  160| 110| 3.90| 2.620| 16.46|  0|  1|    4|    4|
    |Mazda RX4 Wag     | 21.0|   6|  160| 110| 3.90| 2.875| 17.02|  0|  1|    4|    4|
    |Datsun 710        | 22.8|   4|  108|  93| 3.85| 2.320| 18.61|  1|  1|    4|    1|
    |Hornet 4 Drive    | 21.4|   6|  258| 110| 3.08| 3.215| 19.44|  1|  0|    3|    1|
    |Hornet Sportabout | 18.7|   8|  360| 175| 3.15| 3.440| 17.02|  0|  0|    3|    2|
    |Valiant           | 18.1|   6|  225| 105| 2.76| 3.460| 20.22|  1|  0|    3|    1|

    # A list of all my failings: 

    * A
    * a
    * aa
    * aal
    * aalii

    ## Let me count the ways 

    1. One
    2. Two
    3. Three
    4. Four
    5. Get on the Dance Floor

    ```{r }

      x <- 5
      x + 1

    ```

#### Save to file and then render/knit

``` r
writeLines(doc$as_character(), "working/temp.Rmd")
```

<img src="man/figures/render1.png" width="80%" />

## Example: Programmatic document creation

Generating some reference documentation for a [Top
Trumps](https://en.wikipedia.org/wiki/Top_Trumps) game based upon the
`mtcars` dataset.

``` r
library(moggy)
doc <- MarkdownDoc$new()
doc$h1("mtcars SuperTrumps")

for (i in 1:3) {
  doc$h2(rownames(mtcars)[i])
  doc$h3("Image")
  doc$add("<img src='https://dummyimage.com/640x4:3/' width='40%' />")
  doc$h3("Stats")
  doc$table(mtcars[i, 1:4])
}

writeLines(doc$as_character(), "working/temp.Rmd")
```

<img src="man/figures/supertrumps.png" width="80%" />

## Related Software

- [tinkr](cran.dev/tinkr)
- [parsemd](cran.dev/parsemd)

## Acknowledgements

- R Core for developing and maintaining the language.
- CRAN maintainers, for patiently shepherding packages onto CRAN and
  maintaining the repository
