# Unate-Recursive-Paradigm
This project deals with calculation of complement of a boolean function using Unate Recursive Paradigm. Tested for functions with upto 10 variables and 150 product terms. 
Can handle functions efficiently with upto 20 variables and 2^20 product terms.

We can very well calculate complements for small boolean functions comprising of 3 or 4 variables by hand. But when you are given a function with more than 10 variables with hundreds of product terms, it becomes tedious. So for a very large scale operation, we have to come up with an efficient algorithm to complement functions with huge number of variables and product terms. In this project, Unate Recursive Paradigm (URP) is used

A simple version of the algorithm is below: 
  
1. cubelist Complement(function) {
2. // check if func is simple enough to complement it directly and quit
if (function is simple and we can complement it directly ):
return(direct complement using Demorgan's laws)
else {
// do recursion
let x = most binate variable for splitting
Pos_CF = Complement(positiveCofactor(function, x ))
Neg_CF= Complement(negativeCofactor(function, x'))
P=AND(x,Pos_CF)
N=AND(x’,Neg_CF)
return(OR(P,N))
} // end recursion
}

# Termination Conditions:
If a cubelist is empty, and has no cubes in it, then this represents the Boolean equation “0”. The complement is clearly “1”, which is
represented as a single cube with all its variable slots set to don’t cares. For ex: if cubelist=0, then our complement cubelist will be [11]*(No of variables)

If Cube list contains "All Don’t Cares Cube" means that the function is '1' and clearly complement is '0'
And if the Cube list contains just one cube, we can directly complement it using Demorgan's theorem. For ex: if the single cubelist is [[11,01,10,01]] which is yz'w, the complement cubelist is clearly: (y’ + z + w’) = [[11,10,11,11], [11,11,01,11],[11,11,11,10]] which is easy to compute. You get one new cube for each non-don’t-care slot in the F cube. Each new cube has don’t cares in all slots but one, and that one variable is the complement of the value in the function cubelist.

# Selection Criteria
The most Binate variable that appears in most number of product terms is chosen as a splitting variable to find cofactors of the function. In case there is a tie between two or more Binate variables, |T-C| (difference of number of positive and negative occurrences of a variable in the cubelist) of those variables is evaluated, and the one with the lowest value of |T-C| is chosen as the splitting variable. If a further tie ensues, the one with the lowest index in the cubelist is chosen.

And again if there are no Binate variables to choose from, the number of unate variables are observed. The variable that appears in most number of product terms is chosen as splitting variable. In case there is a tie between two or more unate variables, the one with the lowest index in the cubelist is chosen. 

The positive and negative cofactors of the function are calculated by quantifying away the splitting variable from the function . Recursion takes place until we obtain a single cube that can be directly complemented using Demorgan's laws, or until we obtain a "All don't cares" cube that can be complemented directly. The resulting cubelists after recursion are ANDed seperately with the splitting variable and ORed as per the complement version of shannon expansion:

OR ( x AND (Complement (fx)) , x' AND (Complement (fx') ))

where x is the splitting var, fx is positive cofactor, fx' is negative cofactor
