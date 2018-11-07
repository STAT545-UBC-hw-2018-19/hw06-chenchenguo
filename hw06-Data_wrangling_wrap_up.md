Hw-06-ChenchenGuo
================
Chenchen GUO
October 30, 2018

-   [Introduction](#introduction)

    -[Goals](#goals)
-   [Part1: Character data](#part-1-character-data)

    -[Requirements](#requirements)

    -[Implementation](#implementation)

-   [Part2: File I/O](#part-2-file-io)

    -[Requirements2](#requirements2)

    -[Implementation2](#implementation2)

-   [Part3: Visualization design](#part-3-visualization-design)

    -[Requirements3](#requirements3)

    -[Implementation3](#implementation3)

Introduction
------------

[Homework 06](http://stat545.com/Classroom/assignments/hw06/hw06.html): Data wrangling wrap up

Goals:
------

The first assignment of STAT 547M, complete two of the six topics.

Part 1: Character data
----------------------

Requirements
------------

Work the exercises in the Strings chapter or R for data science.

Implementation
--------------

Strings charpter

Firstly load all needed packages

``` r
suppressPackageStartupMessages(library(gapminder))
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(stringr))
suppressPackageStartupMessages(library(knitr))
suppressPackageStartupMessages(library(broom))
suppressPackageStartupMessages(library(MASS))
```

14.2.5 Exercises
----------------

### 1. Whats the difference between paste() and paste0()? What the equivalent stringr functions of them?

``` r
(name_sports <- paste("Bas", "ket", "ball"))
```

    ## [1] "Bas ket ball"

``` r
(name_sports1 <- paste0("Bas", "ket", "ball"))
```

    ## [1] "Basketball"

``` r
# The difference between paste() and paste0() is the argument sep by default is " " for paste() and "" for paste0()

# paste0() is equivalent to str_c
(name_sports2 <- str_c("Bas", "ket", "ball"))
```

    ## [1] "Basketball"

``` r
# paste() is equivalent to str_c(.., sep = " ")
(name_sports3 <- str_c("Bas", "ket", "ball", sep = " "))
```

    ## [1] "Bas ket ball"

### 2. Describe the difference between sep and collapse arguments to str\_C()?

``` r
x <- c("a", "b", "c", "d")
y <- c("w", "x", "y", "z")
paste(x, y, sep="%%")
```

    ## [1] "a%%w" "b%%x" "c%%y" "d%%z"

``` r
paste(x, y, collapse="%%")
```

    ## [1] "a w%%b x%%c y%%d z"

``` r
paste(x, y, sep="%%", collapse=",")
```

    ## [1] "a%%w,b%%x,c%%y,d%%z"

``` r
paste(x, y, sep=",", collapse="%%")
```

    ## [1] "a,w%%b,x%%c,y%%d,z"

``` r
# Hence, the sep defines what separates the entries in those tuple-wise concatenations
# the collapse will return any concatenated pairs as part of a sigle length-1 character vector
```

### 3. Use str\_lennth() and str\_sub() to extract the middle character from a string. What will you do if the string has an even number of length?

``` r
vec_str <- "asdfghj"
vec_length <- str_length(vec_str)
str_sub(vec_str,(vec_length+1)/2, (vec_length+1)/2)
```

    ## [1] "f"

``` r
vec_str1 <- "asdfgh"
vec1_length <- str_length(vec_str1)
str_sub(vec_str1,(vec1_length)/2, (vec1_length)/2+1)
```

    ## [1] "df"

### 4. What does str\_wrap() do?

``` r
txt <- c("Jane can run quickly.  So can Dick.",
         "",
         "The quick red fox jumped over the lazy brown dog.")
writeLines(strwrap(txt, width = 25))
```

    ## Jane can run quickly.
    ## So can Dick.
    ## 
    ## The quick red fox jumped
    ## over the lazy brown dog.

``` r
writeLines(strwrap(txt, width = 30, indent=5))
```

    ##      Jane can run quickly.
    ## So can Dick.
    ## 
    ##      The quick red fox jumped
    ## over the lazy brown dog.

``` r
# strwrap can print strings into paragraphs
```

### 5. What does str\_trim() do?

``` r
vec_5 <- c("hi", "hello", "Richard Jeffeson")
vec_5
```

    ## [1] "hi"               "hello"            "Richard Jeffeson"

``` r
strtrim(vec_5, 7)
```

    ## [1] "hi"      "hello"   "Richard"

### 6. Write a function that turns a vector c("a", "b", "c") into the string a, b, and c.

``` r
vector_to_string <- function(v){
    if(length(v)==0){
        stop("NA")
    }
    if(length(v)==1){
        return(v)
    }
    str1 <- str_c(v[1:length(v)-1], collapse = ", ")
    str2 <- str_c(str1, v[length(v)], sep = ", and ")
}
vec_6 <- c("s","o","s")
(vector_to_string(vec_6))
```

    ## [1] "s, o, and s"

14.3.1.1 Exercises
------------------

### 1. Explain why each of these strings don't match a : "","\\","\\"?

### 2. How would you match the sequence "'?

3. What patterns will the regular expression ...... match? How to represent it as a string?
-------------------------------------------------------------------------------------------

14.3.2.1 Exercises
------------------

### 1. How would you match the literal string "$^$"?

### 2. Given the corpus of common words in stringr::words, create regular expressions that find all words that:

        1. Start with "y"
        2. End with "x"
        3. Are exactly three letters long.
        4. Have seven letters or more.
        

14.3.3.1 Exercises
------------------

### 1. Create regular expressions to find all words that:

        1. Start with a vowel.
        2. That only contains constants.
        3. End with ed, but not with eed.
        4. End with ing or ise.

### 2. Empirically verify the rule "i before e except after c"?

### 3. Is "q" always followed by a "u"?

### 4. Write a regular expression that matches a word if its probably written in British English, not American English?

### 5. Create a regular expression that will match telephone numbers as commonly written in your country?

14.3.4.1 Exercises
------------------

### 1. Describe the equivalents of ?, +, \* in {m,n} form.

### 2. Describe in words what these regular expressions match:

    1. ^.*$
    2. "\\{.+\\}"
    3. \d{4}-\d{2}-\d{2}
    4. "\\\\{4}"

### 3. Create regular expressions to find all words that:

    1. Start with three consonants.
    2. Have three or more vowels in a row.
    3. Have two or more vowel-consonant pairs in a row.

14.3.5.1 Exercises
------------------

### 1. Describe in words what these expressions will match:

    1. (.)\1\1
    2. "(.)(.)\\2\\1"
    3. (..)\1
    4. "(.).\\1.\\1"
    5. "(.)(.)(.).*\\3\\2\\1"

### 2. Construct regular expressions to match words that:

    1. Start and end with the same character.
    2. Contain a repreated pair of letters.
    3. Contain one letter repeated in at least three places.

14.4.2 Exercises
----------------

### 1. For each of the following challenges, solve it by using both a singular expression and a combination of multiple str\_detect() calls.

    1. Find all words that start or end with x.
    2. Find all words that start with a vowel and end with a constant.
    3. Are there any words that contain at least one of each different vowel?

### 2. What word has the highest number of vowels? What words has the highest proportion of vowels?

14.4.3.1 Exercises
------------------

### 1. In the previous example, you might have noticed that the regular expression matched "flickered", which is not a colour. Modify the regex to fix the problem.

### 2. From the Harvard sentences data, extract:

    1. The first word from each sentence.
    2. All words ending in ing.
    3. All plurals.

14.4.4.1 Exercises
------------------

### 1. Find all words that come after a "number" like "one", "two", "three"etc. Pull out both the number and the word.

### 2. Find all contractions, separate out the pieces before and after the apostrophe.

14.4.5.1 Exercises
------------------

### 1. Replace all forward slashes in a string with backslashes.

### 2. Implement a simple version of str\_to\_lower() using replace\_all()

### 3. Switch the first and last letters in words. Which of those strings are still words?

14.4.6.1 Exercises
------------------

### 1. Split up a string like "apples, pears, and bananas" into individual components.

### 2. Why is it better to split up by boundary("word") than " "?

### 3. What does splitting with an empty string ("")do?

14.5.1 Exercises
----------------

### 1. How would you find all strings containing  with regex() vs. with fixed()?

### 2. What are the five most common words in sentences?

14.7.1 Exercises
----------------

### 1. Find all stringi functions that:

        1. Count the number of words.
        2. Find duplicated strings.
        3. Generate random text.

### 2. How do you control the language that stri\_sort() using for sorting?
