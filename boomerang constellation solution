/ sample input coordinates (try one at a time)
a:(0 0;0 1;0 2;0 3;0 4)         / expected output: 4
a:(0 0;-3 4;0 5;-5 0)           / expected output: 3
a:(0 0;0 100;100 0;100 100)     / expected output: 3
a:(5 6;6 5;7 6;6 7;7 8;8 7)     / expected output: 12
a:(0 0;0 1;0 3)                 / expected output: 0

/
helper functions
\
nc2:{x*(x-1)%2}                 / choosing 2 out of n coordinates
distance:{[x;y] enlist[(x;y)]!enlist sum(y-x)xexp 2}      / return a dictonary of coordinates and the square of distance between the points 

/ compute all possible distance combinations between the input points
all_segments:raze{[i] raze distance[a[i];]each a except enlist a[i]} each til count a;   

/ remove duplicate distance computations; very inefficient - needs revisit
distance_dictionary: (!) . (z;all_segments[z:distinct asc each key all_segments]);

/ group equidistant coordinates and combine (nc2) two pairs that are equidistant 
sum raze nc2 each value each count each'group each raze each value group distance_dictionary;

==========================================================================================================================

/
a more q-ish solutions
\

a:(0 0;-3 4;0 5;-5 0)
sum {x*(x-1)%2} each raze {value count each group `int$sum flip ((a x)-/:(a except enlist a x)) xexp 2} each til count a

/
a more optimized version
\
a:(0 0;-3 4;0 5;-5 0)
sum {x*(x-1)%2} raze deltas each ({where differ asc sum each x}each n*n:a-/:'a@m _/:m:til l),'-1+l:count a
