Our main goal now is to achieve convergence for the following model

proc glimmix data= step4_&yr._formod_2  METHOD=LAPLACE;
title2 "model: DEATH30DAY_R model with AGE, PALL (indicator for palliative care), FEMALE, APR_SOI indicators ";
by Service_Line_New;
 class HOSPID;
 model DEATH30DAY_R (event="1") = age_yrs pall female &APR_MORT_inds.
		/ dist=binary link=logit solution;
 XBETA=_XBETA_;
 LINP=_LINP_;

 random intercept / subject=HOSPID solution;

 output out=model&yr.Out&yr. pred( blup ilink)=PREDProb
					   pred(noblup ilink)=EXPProb;
 NLOPTIONS MAXITER = 10000 /*TECH = NMSIMP */TECH = CONGRA INSTEP = 1E-4; /*LSP=0.02*/ 
 ods output ParameterEstimates=model&yr.params&yr. ;
 ods output FitStatistics=model&yr.FIT&yr.;
run;
Sometimes orthopedic regression converges (e.g., 2018) and sometimes does not (e.g., 2019). It may be appropriate to not include service lines that fail to reach convergence (instead of drastically compromising the regression model so the cases can be included).
Task 1.1
1)	Macrotize proc glimmix – good option going forward for more flexibility in running code and having possibility of different optimization procedures for each service line if needed to achieve convergence
a)	Will try line search methods until convergence achieved
b)	HSCRC will outline which optimization techniques to try and the ordering
i)	NMSIMP
ii)	Parameter statement
iii)	Run with overdispersion
iv)	Last option is for all hospitals to have the same effect for the given condition -- to lead to convergence - observed equals expected, which is similar to throwing out
v)	Start with three or four parameters to tweak and then the SAS code cycles through different combinations.
 2） Add warnings if any of the 15 service line regressions do not converge.


