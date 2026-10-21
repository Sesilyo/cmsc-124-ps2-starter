# Vector and Scalar Evaluation

## Vector Operations

### Which operations in the vector version act on all elements at once?

Our clean_scores_vector() function processes the scores through three vector operations in sequence. First, is.na(scores) creates a logical mask identifying missing values, and subassignment replaces those positions with 0. Next, scores * 2 doubles every element. Finally, scores > 20 creates another logical mask, and subassignment replaces values above 20 with 20. These operations preserve the names attached to the vector.

For the shared input c(Ada = 8, Grace = NA_real_, Linus = 12, Barbara = 4), the first operation produces c(Ada = 8, Grace = 0, Linus = 12, Barbara = 4). Doubling produces c(Ada = 16, Grace = 0, Linus = 24, Barbara = 8). Applying the cap gives c(Ada = 16, Grace = 0, Linus = 20, Barbara = 8). Grace’s missing value becomes zero before multiplication, so it remains zero and does not satisfy the condition for capping.

### Where does the scalar loop make evaluation order visible?

We consider the order to be mainly visible when we assign `curr_score` with the values of index `i` and if the question means where do we evaluate the NA score case it's in `is.na(curr_score)`. Grace's NA score is handles on the second pass of the loop: `curr_score` is NA, `is.na(curr_score)` is TRUE, and `out[[2]] <- 0` stores 0. This differs from the vector implementation where it processes all elements at the same time (using vector expressions and subassignment).

### One concrete input where careless recycling changes the answer

Recycling requires care because R repeats shorter operands. For example, multiplying c(8, 0, 12, 4) by c(2, 3) produces c(16, 0, 24, 12), rather than the intended c(16, 0, 24, 8). After capping, Barbara incorrectly receives 12 instead of 8. R gives no warning because four is a multiple of two. Our length-one multiplier, 2, intentionally applies the same factor to every score.

### Which implementation would you keep in an R program, and what tradeoff does that choice make?

We choose the keep the scalar implementation. A loop-implementation is easier to read since it is already familiar and the form is similar throughout different programming languages. Another reason why we want to keep this implementation is because unlike the vector implementation, there's no recycling hazard _e.g._ `scores <- scores * 2`. One major trade-off of this implementation Cost-wise is that R is optimized by vector operation and using a loop to process elements one by one is slower and computationally expensive as well as using a loop do not respect the domain specification of R.