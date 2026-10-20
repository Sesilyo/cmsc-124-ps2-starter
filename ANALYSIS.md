# Vector and Scalar Evaluation

## Vector Operations

Our clean_scores_vector() function processes the scores through three vector operations in sequence. First, is.na(scores) creates a logical mask identifying missing values, and subassignment replaces those positions with 0. Next, scores * 2 doubles every element. Finally, scores > 20 creates another logical mask, and subassignment replaces values above 20 with 20. These operations preserve the names attached to the vector.

For the shared input c(Ada = 8, Grace = NA_real_, Linus = 12, Barbara = 4), the first operation produces c(Ada = 8, Grace = 0, Linus = 12, Barbara = 4). Doubling produces c(Ada = 16, Grace = 0, Linus = 24, Barbara = 8). Applying the cap gives c(Ada = 16, Grace = 0, Linus = 20, Barbara = 8). Grace’s missing value becomes zero before multiplication, so it remains zero and does not satisfy the condition for capping.

Recycling requires care because R repeats shorter operands. For example, multiplying c(8, 0, 12, 4) by c(2, 3) produces c(16, 0, 24, 12), rather than the intended c(16, 0, 24, 8). After capping, Barbara incorrectly receives 12 instead of 8. R gives no warning because four is a multiple of two. Our length-one multiplier, 2, intentionally applies the same factor to every score.