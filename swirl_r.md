#R Basics
## Lesson 01:
## Lesson 02:
## Lesson 03:
## Lesson 04:
## Lesson 05:
## Lesson 06: Subsetting Vectors

- Vector can be subseted using the bracket notation:

```
> x[1:10]
 [1]  0.09388467          NA  1.84710457 -1.40099761  1.40375502 -0.54688241 -0.72124682
 [8]          NA          NA  1.24603014
```

- Logical expressions can be used to subset vectors:

```
> x[is.na(x)]
 [1] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA

```

```
> x[!is.na(x) & x>0]
 [1] 0.09388467 1.84710457 1.40375502 1.24603014 1.42248685 0.03902429 1.59590232 3.38350202
 [9] 1.89713986 1.33661643 0.93811063
```

- to get especifc nTH numbers I should use c():
```
> x[c(3,5,7)]
[1]  1.8471046  1.4037550 -0.7212468
```
- to get all elements except specific ones use the - notation:
```
> x[c(-2,-10)] or x[-c(2,10)]
 [1]  0.09388467  1.84710457 -1.40099761  1.40375502 -0.54688241 -0.72124682          NA
 [8]          NA -0.22099536          NA          NA          NA  1.42248685  0.03902429
[15]          NA          NA          NA  1.59590232          NA          NA          NA
[22]  3.38350202 -0.58426553  1.89713986          NA  1.33661643          NA -0.11045995
[29] -0.02973354  0.93811063 -0.42237719          NA          NA          NA -0.86124669
[36]          NA          NA          NA

```
- subsetting named vectors:
```
> vect <- c(foo = 11, bar = 2, norf = NA)
> vect
 foo  bar norf 
  11    2   NA 
> vect[c("foo", "bar")]
foo bar 
 11   2 

```
## Lesson 07: Matrices and Data Frames

The main difference, as you'll see, is that matrices can only contain a single class of data, while data frames can consist of many different classes of data

- It's okay if that last command seemed a little strange to you. It should! The dim() function
| allows you to get OR set the `dim` attribute for an R object. In this case, we assigned the
| value c(4, 5) to the `dim` attribute of my_vector

```
> dim(my_vector) <- c(4,5) gives my vector the dimensions 4 and 5 turningt it into a matrix
> my_vector
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    5    9   13   17
[2,]    2    6   10   14   18
[3,]    3    7   11   15   19
[4,]    4    8   12   16   20

```
- another way to build a matrix:
```
> my_matrix2 <- matrix(my_vector, nrow = 4, ncol = 5)
```
- creating data frames:
```
> patients <- c("Bill", "Gina", "Kelly","Sean")
> my_data <- data.frame(patients, my_matrix)
> my_data
  patients X1 X2 X3 X4 X5
1     Bill  1  5  9 13 17
2     Gina  2  6 10 14 18
3    Kelly  3  7 11 15 19
4     Sean  4  8 12 16 20

```
- setting column names:
```
> cnames <- c("patient", "age", "weight", "bp", "rating","test")
> colnames(my_data) <- cnames 
> my_data
  patient age weight bp rating test
1    Bill   1      5  9     13   17
2    Gina   2      6 10     14   18
3   Kelly   3      7 11     15   19
4    Sean   4      8 12     16   20
```
## Lesson 08: Logic

- Operadores:
```
== != & && | || ! > < >= <=
```
*Os operadores condicionais: &, &&, |, || funcionam diferente quando usados com vetores.

## Lesson 09: Functions
To understand computations in R, two slogans are helpful: 1. Everything that exists is an
| object. 2. Everything that happens is a function call.

- In R, functions are declared this way:
```
boring_function <- function(x) {
  x
}
```
* The last expression will be returned by the function

- I can pass functions as arguments (like javascript):
```
> args(remainder)
function (num, divisor = 2) 
NULL
```
- Ellipses (...) in functions:
```
telegram <- function(...){
  paste("START", ..., "STOP")
}
> telegram("Eita", "opa")
[1] "START Eita opa STOP"
```

- Unpacking with ellipses:
 Let's explore how to "unpack" arguments from an ellipses when you use the
 ellipses as an argument in a function. Below I have an example function that
 is supposed to add two explicitly named arguments called alpha and beta.
 
 add_alpha_and_beta <- function(...){
    First we must capture the ellipsis inside of a list
    and then assign the list to a variable. Let's name this
    variable `args`.

   args <- list(...)

    We're now going to assume that there are two named arguments within args
    with the names `alpha` and `beta.` We can extract named arguments from
    the args list by using the name of the argument and double brackets. The
    `args` variable is just a regular list after all!
   
   alpha <- args[["alpha"]]
   beta  <- args[["beta"]]
  
```
mad_libs <- function(...){
  # Do your argument unpacking here!
  args <- list(...)
  place <- args[["place"]]
  adjective <- args[["adjective"]]
  noun <- args[["noun"]]
  
  # Don't modify any code below this comment.
  # Notice the variables you'll need to create in order for the code below to
  # be functional!
  paste("News from", place, "today where", adjective, "students took to the streets in protest of the new", noun, "being installed on campus.")
}
  ```
