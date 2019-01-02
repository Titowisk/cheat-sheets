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
