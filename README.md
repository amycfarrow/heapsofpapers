
<!-- README.md is generated from README.Rmd. Please edit that file -->

# heapsofpapers

<!-- badges: start -->
<!-- badges: end -->

The goal of `heapsofpapers` is to make it really easy to respectfully
get, well, heaps of papers (and CSVs and websites). For instance, you
may want to understand the state of open code and open data across a
bunch of different pre-print repositories, e.g. Collins and Alexander,
2021, and in that case you need a way to quickly download thousands of
PDFs.

Essentially, the main function in the package,
`heapsofpapers::get_and_save()` is a wrapper around a `for` loop and
`utils::download.file`, but there are a bunch of small things that make
it handy to use instead of rolling your own each time. For instance, the
package automatically slows down your requests, lets you know where it
is up to, and adjusts for papers that you’ve already downloaded.

## Installation

You can `heapsofpapers` from [GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("RohanAlexander/heapsofpapers")
```

## Example

Here is an example of getting two papers from SocArXiv:

``` r
library(heapsofpapers)
two_pdfs <-
  tibble::tibble(
    locations_are = c("https://osf.io/preprints/socarxiv/z4qg9/download",
                      "https://osf.io/preprints/socarxiv/a29h8/download"),
    save_here = c("competing_effects_on_the_average_age_of_infant_death.pdf",
                  "cesr_an_r_package_for_the_canadian_election_study.pdf")
    )

heapsofpapers::get_and_save(
  data = two_pdfs,
  links = "locations_are",
  save_names = "save_here"
)
```

You could also specify the directory, for instance, if you have a folder
called ‘inputs’.

``` r
heapsofpapers::get_and_save(
  data = two_pdfs,
  links = "locations_are",
  save_names = "save_here",
  dir = "./inputs"
)
```

Let’s say that you had already downloaded some PDFs, but weren’t sure
and didn’t want to download them again. You could use
`check_for_existence` to check.

``` r
heapsofpapers::check_for_existence(data = two_pdfs, 
                                   save_names = "save_here")
```

## Roadmap

-   ~~Allow the user to specify how long they would like to wait.~~
-   ~~Add so that it checks whether the file exists and asks the user
    whether they’d like to re-download that or skip that.~~
-   ~~Add option to save to AWS bucket~~
-   ~~Add something that automatically looks at whether the folder
    exists and if not, creates it.~~
-   ~~Don’t sleep after the last paper.~~
-   ~~Update check\_for\_existence()~~
-   Add vignettes of doing this for CSVs and for html.
-   Add tests.
-   Add CI.
-   Add message that estimates how long it’ll take and asking whether
    the user would like to proceed.
-   Make the length of the pause dependent on the size of the file that
    is downloaded, by default.
-   Make the printing of the message again optional, or every X or
    similar, as specified by the user.
-   Option to save to Dropbox.
-   Add email notification for when it’s done.
-   Add a check for any PDFs that are very small (which usually
    indicates there’s something wrong with them).

## Related packages

There are many packages that are designed for scraping websites for
instance, [`polite`](https://dmi3kno.github.io/polite/) and
[`rvest`](https://rvest.tidyverse.org/). Those packages are more general
and more useful in a wider range of scenarios than ours is. Ours is
focused on the specific use-case where you have a large list of items
that you need to download.

## Citation

Please cite the package if you use it: Alexander, Rohan, Annie Collins,
and A Mahfouz, 2021, ‘heapsofpapers: Easily get heaps of papers’ 20
March, <https://github.com/RohanAlexander/heapsofpapers>.
