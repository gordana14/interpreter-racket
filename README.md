# interpreter-racket

My Intevaluator entry point should be a function (iv exp env), 
where exp is an Intervaluator expression and env is the environment in which the expression will be evaluated. 
The functionality described in the following sections:

1 Data types
• Numerical values (const n): if n is a numerical value in Racket, then (const n) is a numerical value in Intervaluator.
• Logical values (bool b): if b is a logical value in Racket, then (bool b) is a logical value in Intervaluator.
• Intervals (interval a b): if a and b are numerical values in Racket, then (interval a b) is an Intervaluator interval
with given lower and upper bounds (inclusive), representing [a,b], where a ≤ b. 
• Pairs (pair e1 e2): if e1 and e1 are Intervaluator expressions, then (pair e1 e2) is an Intervaluator pair of values v1 and v2 that 
result by evaluating expressions e1 and e2, respectively, representing (e1,e2). 
• Null (nil): this expression represents a null value (analogous to null in Racket). 
Caution: (nil) is an expression, but nil (without the parentheses) is not.

2 Processing and control ﬂow 
• Branching (if-then-else b e1 e2): this expression represents branching in Intervaluator.
If b evaluates to (bool #t), then the result of the expression is a value that results by evaluating e1
, otherwise it equals a value that results by evaluating e2. Only one of either e1 or e2 should be evaluated.
• Type queries (is-const? e), (is-bool? e), (is-interval? e), (is-nil? e): if e is an Intervaluator expression, 
then (is-const? e), (is-bool? e), (is-interval? e) and (is-nil? e) evaluate to logical values in Intervaluator, 
which are true if the value that results by evaluating e is const, bool, interval or nil, respectively, and false otherwise.
• Negation (negate e): if e is an Intervaluator expression, then (negate e) is a negation of the value that results by evaluating e.
Negating logical values yields the opposite logical value, negating a numerical value v yields −v, 
and negating an interval [a,b] yields [−b,−a].
• Addition (add e1 e2): if e1 and e2 are Intervaluator expressions, then (add e1 e2) is a sum of the values v1 and v2 
that result by evaluating e1 and e2, respectively. If v1 and v2 are numerical values, then the result is a numerical value 
of the sum of v1 and v2. If v1 and v2 are intervals [a,b] and [c,d], then the result is an interval [a+c,b+d]. 
If one of v1 and v2 is a numerical value v and the other one is an interval [a,b], then the result is an interval [a + v,b + v]. 
• Multiplication (multiply e1 e2): if e1 and e2 are Intervaluator expressions, then (multiply e1 e2) is a product of the values v1 and v2 
that result by evaluating e1 and e2, respectively. 
If v1 and v2 are numerical values, then the result is a numerical value of the product of v1 and v2.
If v1 and v2 are intervals [a,b] and [c,d], then the result is an interval [min{ac,ad,bc,bd},max{ac,ad,bc,bd}].
• Exponentiation (exponentiate e): if e is an Intervaluator expression, then (exponentiate e) is the exponentiation of 
the value v that results by evaluating e. If v is a numerical value v, then the result is a numerical value ev. 
If v is an interval [a,b], then the result is an interval [ea,eb].
• Extraction (left e), (right e): if e is an Intervaluator expression, then (left e) and (right e) are extractions of the value v 
that results by evaluating e. If v is a pair (a,b), then (left e) is a and (right e) is b. If v is an interval [a,b], then (left e)
is a numerical value of a and (right e) is a numerical value of b. 
• Comparison (greater e1 e2): if e1 and e2 are Intervaluator expressions, then (greater e1 e2) is an expression in Intervaluator
that represents comparison. If v1 and v2 are numerical values that result by evaluating e1 and e2, respectively, 
then the result is (bool #t) if v1 > v2 and (bool #f) otherwise. If v1 and v2 are intervals that result by evaluating e1 and e2, 
respectively, then the result is (bool #t) if the width of v1 is strictly greater than the width of v2 and (bool #f) otherwise. 
The width of an interval [a,b] is b−a. 
• Intersection (intersect e1 e2): if e1 and e2 are Intervaluator expressions that evaluate to intervals [a,b] and [c,d], respectively, 
then (intersect e1 e2)
is an interval in Intervaluator that is the result of the intersection [a,b]∩[c,d] or (nil), if the intersection is empty.



