Our main goal now is to achieve convergence for the following model

![image](https://github.com/user-attachments/assets/66775f03-733e-41bb-bbc6-b899e4fc4233)

Task 1.1
1)	Macrotize proc glimmix option for more flexibility in running code and having possibility of different optimization procedures for each service line if needed to achieve convergence
a)	Will try line search methods until convergence achieved
b)	HSCRC will outline which optimization techniques to try and the ordering
i)	NMSIMP
ii)	Parameter statement
iii)	Run with overdispersion
iv)	Last option is for all hospitals to have the same effect for the given condition -- to lead to convergence - observed equals expected, which is similar to throwing out
v)	Start with three or four parameters to tweak and then the SAS code cycles through different combinations.
 2） Add warnings if any of the 15 service line regressions do not converge.


