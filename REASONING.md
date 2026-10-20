# Reasoning Before Execution

Write the rule behind each case before you commit your predictions. Replace every placeholder line below with one to three sentences that name the rule producing that case's value, type, length, and dimensions. One rule is enough. After you run and find a miss, add a short correction entry under that case in a later commit.

## P01
Rule: Atomic Vector Coercion
The rule says that all elements of a vector must share the same type. That is why TRUE -> 1, 2L -> 2, and 3.5 stays as is since double takes greatest precedence of P01's vector, all the elements become a double type. The length is 3 because there are 3 elements, and the dimension is none because plain atomic vectors do not carry a dimension attribute.

## P02
Rule: Atomic Vector Coercion
Similar to P01 but the coercion ladder ends at character so all elements becomes character types. type: character, length: 3 because there are 3 elements, dim: none because atomic vectors do not carry dimension attribute.

## P03
Rule: Vector Recycling Rule
When adding two vectors, the vector with the shorter length repeat its values to map it and add it respectively with the elements of the vector of longer length. That is why value: [11L, 22L, 31L, 42L], type: integer because the vector's elements are all integers, length: 4, dim: none.

## P04
Rule: Integer Index Reordering
[c(3L, 1L)] selects the third integer and first integer elements in that order that is why value: [third=9L, first=8L], type: integer because it's just integers with "variables", length: 2, dim: none.

## P05
Rule: Negative Index Exclusion
[-2L] removes the 2nd integer from the vector that is why value: [4L, 9L], type: integer, length: 2, dim: none.

## P06
Rule: Logical OR (|) and NA Propagation
is.na(x) checks if every element of vector x is of the NA type and returns TRUE or FALSE and x > 10L compares every elements of vector x to 10L and then since is.na(x) is compared with x > 10L, their vector's elements are mapped to each other and evalauted using the logical OR x[] "collect" the elements that are true, that is value: [NA, 12L], type: integer, length: 2, dim: none

## P07
Rule: Factor Storage
factor(c("low", "high", "low"), levels = c("low", "high")) maps "low" -> 1L and "high" -> 2L that is why type: integer, value: factor[low,high,low];levels=[low,high], length: 3 is still the from vector, dim: none.

## P08
Rule: Heterogenous List
Lists preserves integer and character types (doesn't coerce them), therefore, the type is: list, value: list{scores=[3,5],label=["A"]}, length (from scores): 2, dim: none.

## P09
Rule: Data Frame List-Under-The-Hood Model
Data frame is actually a list of columns of equal length.

## P10
Rule: Column-Major Matrix Recycling
Matrix builds a 2 row matrix with 1:6 and then the 2nd vector recycles it's values across the vector. Hence, value: matrix[2x3](11,22,13,24,15,26), type: integer because the matrix specifies it, length: 6, dim: c(2L,3L).

## P11
Rule: Infection in Summary Operations
Since there is a missing value, mean() evaluates the vector as NA, therefore, value: NA, type: double, length: 1, dim: none.

## P12
Rule: Explicit Missing Value Removal
na.rm removes the missing value giving us value: 9, type: double, length: 1, dim: none

## P13
Rule: Mixed-Mode Subassignmenth
The first line initializes an integer vector and line 2 writes a double into the 2nd position of the integer vector which widens the vector. Value: [1,2.5,3], type: double, length: 3, dim: none.

## P14
Rule: Vectorized Conditional
ifelse converts NA -> 0 and doubles non-missing values. Value: [14,0,15,8], type: double, length: 4. dim: none.


## P15
Rule: 3D Array Column-Major Reshaping
array() adds a 3D dimension vector to the integer vector with 8 elements. Value: [14,0,15,8], type: integer, length 8, dim: c(2L, 2L, 2L)

## P16
Rule: 0-Index Empty Vector Selection
Index 0L extracts nothing from the vector, so value: [], type: integer because the length is: 0, dim: none
