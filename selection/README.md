Selection detection.
====================

__Data sources__

All the alignment files used here are included in [this .zip file](http://github.com/veg/hyphy). 

__Notation__

 We will use the following notation.

1. `filename` refers to file in the file system.
2. **Option** refers to an analysis option that you will select when prompted by HyPhy
3. *Menu item* refers to a menu option you will select in the Mac OS X or Windows GUI version of HyPhy,
or a command line you will execute in terminal with the command line version of HyPhy.
4. The following formatting refers to HyPhy text output to the screen.

```
[BUSTED] Selected 35 branches as the test (foreground) set: RABENSBURG_ISOLATE,WNFCG,SPU116_89,Node11,Node9,KUNCG,Node8,..
[BUSTED] Obtaining initial branch lengths under the GTR model 
[BUSTED] Log(L) = -7745.475588071066 
[BUSTED] Fitting the unconstrained branch-site model 
``` 

Estimating alignment-wide &omega;.
----------------------------------

1. [**_For command line version (CLI) only_**]. When you launch HyPhy, include the *-p* command line option
to invoke the result processing modules afterwards, as in *$HYPHYMP -p*.
2. Select the appropriate analysis to run
  * **_GUI_** Choose *Analysis:Standard Analyses:Basic Analyses:AnalyzeCodonData.bf*    
  * **_CLI_** When presented with the list of standard analysis options upon launch, choose *Basic Analyses*, then option 1 (*Analyse codon data with a variery of standard models using given tree.*)
3. **Universal** genetic code option
4. The file to process
  * **_GUI_** In the file dialog, navigate to and select `WestNileVirus_NS3.fas`
  * **_CLI_** Input the full path name to the file (make sure there is no trailing space), e.g. `/Users/sergei/Dropbox/Talks/VEME2014/data/WestNileVirus_NS3.fas`
5. **MG94CUSTOMCF3X4** model; the Muse Gaut 94 model with the CF3x4 frequency estimator.
6. **Global** model parameter option; estimate rate parameters jointly from all sites and branches.
7. **012345** nucleotide substitution rates; estimate the REV (5 rates) model.
8. Confirm that the tree included in the file will be used
  * **_GUI_** Type **y** into the bottom box of the console window and hit Enter
  * **_CLI_** Type **y** and hit Enter
9. **Estimate** branch lengths directly 
10. The analysis will run for a few minutes (depending on computer speed), and when done, it will produce
screen output (see below). To get approximate confidence intervals, use the processing results module
  * **_GUI_** Select *Analysis:Results*
  * **_CLI_** Type **y** in response to *Continue with result processing (y/n)*
Then *Variance Estimates*, then *Likelihood Profile*, 
   

, producing the output like this

```
_____________RESULTS______________
Log Likelihood = -6413.50468054519;
Shared Parameters:
R=0.008551668421244748
GT=0.2303049266395047
CT=1.979616959919051
CG=0.02076342133619539
AC=0.2427767402648906
AT=0.305486614391144

Tree givenTree=((((((HNY1999:0.001101810046549539,NY99_EQHS:0.001086758734282518)Node6:0,NY99_FLAMINGO:0)Node5:0,MEX03:0.003273655978248368)Node4:0.001043835131241961,IS_98:0.002238498097897219)Node3:0.010810739226833,PAH001:0.009944571986406506)Node2:0.006482211341279835,AST99:0.01679365520732371,((((RABENSBURG_ISOLATE:1.052567309814534,(WNFCG:0.01055548963353968,SPU116_89:0.005665307241141077)Node19:0.5074246792718854)Node17:0.5771347850262071,KUNCG:0.08762054624013382)Node16:0.06944654080511896,(ETHAN4766:0.02385065624081109,(CHIN_01:0.01206043931478093,EG101:0.0150585435082636)Node25:0.007682130398194246)Node23:0.003443456948139096)Node15:0.01851194522198735,(((ITALY_1998_EQUINE:0.009036520833779711,PAAN001:0.007872692859959647)Node30:0.002694380908937295,(RO97_50:0.001642958230190058,VLG_4:0.001082940442608445)Node33:0.002794297600634446)Node29:0.0007239312494192353,KN3829:0.003057891752907082)Node28:0.01098084206175212)Node14:0.009294085670252797);
```

The `R` parameter denotes the 
