# To efficiently find the determinant of an nxn matrix

## 1. Generate a set of permutations of [1,n] (=n! # of permutations)
(If you're familiar with binary counting, this is much like that but with n digits and with no repititions of digits allowed)

For n=5, that would look like:
|   |   |   |   |   |
|---|---|---|---|---|
| 12345 | 21345 | 31245 | 41235 | 51234 |
| 12354 | 21354 | 31254 | 41253 | 51243 |
| 12435 | 21435 | 31425 | 41325 | 51324 |
| 12453 | 21453 | 31452 | 41352 | 51342 |
| 12534 | 21534 | 31524 | 41523 | 51423 |
| 12543 | 21543 | 31542 | 41532 | 51432 |
| 13245 | 23145 | 32145 | 42135 | 52134 |
| 13254 | 23154 | 32154 | 42153 | 52143 |
| 13425 | 23415 | 32415 | 42315 | 52314 |
| 13452 | 23451 | 32451 | 42351 | 52341 |
| 13524 | 23514 | 32514 | 42513 | 52413 |
| 13542 | 23541 | 32541 | 42531 | 52431 |
| 14235 | 24135 | 34125 | 43125 | 53124 |
| 14253 | 24153 | 34152 | 43152 | 53142 |
| 14325 | 24315 | 34215 | 43215 | 53214 |
| 14352 | 24351 | 34251 | 43251 | 53241 |
| 14523 | 24513 | 34512 | 43512 | 53412 |
| 14532 | 24531 | 34521 | 43521 | 53421 |
| 15234 | 25134 | 35124 | 45123 | 54123 |
| 15243 | 25143 | 35142 | 45132 | 54132 |
| 15324 | 25314 | 35214 | 45213 | 54213 |
| 15342 | 25341 | 35241 | 45231 | 54231 |
| 15423 | 25413 | 35412 | 45312 | 54312 |
| 15432 | 25431 | 35421 | 45321 | 54321 |

## 2. Assign a +ve or a -ve sign to them depending on if they are an even or odd permutation of (1,2,...,n)
First make sure that the permutations are in **order** with respect to how ascending or descending the digits of the permutations are.
(So 12345 should be first in the list and 54321 should be the last one)

In our example above, they are already in order:
```12345,12354,12435,12453,12534,12543,13245,13254,13425,13452,13524,13542,14235,14253,14325,14352,14523,14532,15234,15243,15324,15342,15423,15432,21345,21354,21435,21453,21534,21543,23145,23154,23415,23451,23514,23541,24135,24153,24315,24351,24513,24531,25134,25143,25314,25341,25413,25431,31245,31254,31425,31452,31524,31542,32145,32154,32415,32451,32514,32541,34125,34152,34215,34251,34512,34521,35124,35142,35214,35241,35412,35421,41235,41253,41325,41352,41523,41532,42135,42153,42315,42351,42513,42531,43125,43152,43215,43251,43512,43521,45123,45132,45213,45231,45312,45321,51234,51243,51324,51342,51423,51432,52134,52143,52314,52341,52413,52431,53124,53142,53214,53241,53412,53421,54123,54132,54213,54231,54312,54321```

Next, since you've ordered the permulations you can directly assign +ve,-ve,-ve,+ve cyclically to all of them.

Once you do that, you should get something like this:
```12345,-12354,-12435,12453,12534,-12543,-13245,13254,13425,-13452,-13524,13542,14235,-14253,-14325,14352,14523,-14532,-15234,15243,15324,-15342,-15423,15432,-21345,21354,21435,-21453,-21534,21543,23145,-23154,-23415,23451,23514,-23541,-24135,24153,24315,-24351,-24513,24531,25134,-25143,-25314,25341,25413,-25431,31245,-31254,-31425,31452,31524,-31542,-32145,32154,32415,-32451,-32514,32541,34125,-34152,-34215,34251,34512,-34521,-35124,35142,35214,-35241,-35412,35421,-41235,41253,41325,-41352,-41523,41532,42135,-42153,-42315,42351,42513,-42531,-43125,43152,43215,-43251,-43512,43521,45123,-45132,-45213,45231,45312,-45321,51234,-51243,-51324,51342,51423,-51432,-52134,52143,52314,-52341,-52413,52431,53124,-53142,-53214,53241,53412,-53421,-54123,54132,54213,-54231,-54312,54321```

## 3. Find products

Each of the values in the list from step 2 corresponds to a product of n values from our nxn matrix.

A number from our list, say "42351", encodes 5 nxm positions on the matrix. Each digit encodes the **column** and its index/positional placement in the string encodes the **row**:

```
"42351" maps to a product of 5 numbers from a matrix M ⇒ M_14 ⋅ M_22 ⋅ M_33 ⋅ M_45 ⋅ M_51

If a term from the list is -ve we also assign a -ve sign to our product. 

"-54123" ⇒ - M_15 ⋅ M_24 ⋅ M_31 ⋅ M_42 ⋅ M_53
```

Now map each of the terms from the list in step 2 using the above rule to obtain another list.

## 4. Sum it up!

Sum the values from the previous step to obtain the determinant of the matrix `M`.

One can also do all of the four steps directly by looking at a matrix once they have enough practice with this process.

Determinant calculator: https://www.desmos.com/calculator/nqjnpwzbte
