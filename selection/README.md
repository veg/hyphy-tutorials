Selection detection.
====================

__Data sources__

All the alignment files used here are included in the `data` directory or, alternatively, in [this .zip file](http://github.com/veg/hyphy). 

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

1. Select the appropriate analysis to run
  * **_GUI_** Choose *Analysis:Standard Analyses:Basic Analyses:AnalyzeCodonData.bf*    
  * **_CLI_** When presented with the list of standard analysis options upon launch, choose *Basic Analyses*, then option 1 (*Analyse codon data with a variery of standard models using given tree.*)
2. **Universal** genetic code option
3. The file to process
  * **_GUI_** In the file dialog, navigate to and select `WestNileVirus_NS3.fas`
  * **_CLI_** Input the full path name to the file (make sure there is no trailing space), e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data/WestNileVirus_NS3.fas`
4. **MG94CUSTOMCF3X4** model; the Muse Gaut 94 model with the CF3x4 frequency estimator.
5. **Global** model parameter option; estimate rate parameters jointly from all sites and branches.
6. **012345** nucleotide substitution rates; estimate the REV (5 rates) model.
7. Confirm that the tree included in the file will be used
  * **_GUI_** Type **y** into the bottom box of the console window and hit Enter
  * **_CLI_** Type **y** and hit Enter
8. **Estimate** branch lengths directly 

The output should look like this

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

The `R` parameter denotes the global &omega; ratio and is the object of this analysis.

Running alignment-wide tests for episodic diversification (BUSTED).
------------------------------------------------------------------

We will perform branch-site model-based tests for episodic selection affecting a proportion of sites in the alignment along a proportion of branches in the tree (i.e. is there evidence of selection **somewhere** in the alignment). The data set in question is one from [Zhang et al MBE 2005](http://www.ncbi.nlm.nih.gov/pubmed/16107592).

1. Select the appropriate analysis to run
  * **_GUI_** Choose *Analysis:Standard Analyses:Positive Selection:BUSTED.bf*    
  * **_CLI_** When presented with the list of standard analysis options upon launch, choose *Positive Selection*, then option 4 (*Run the Branch-site Unrestricted Statistical Test for Episodic Diversification to test for evidence of episodic alignment-wide selective pressure.*)
2. **Universal** genetic code option
3. The file to process
  * **_GUI_** In the file dialog, navigate to and select `brca1-chimp-human-ann.nex'`
  * **_CLI_** Input the full path name to the file (make sure there is no trailing space), e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data/brca1-chimp-human-ann.nex`
4. Confirm that the tree included in the file will be used
  * **_GUI_** Type **y** into the bottom box of the console window and hit Enter
  * **_CLI_** Type **y** and hit Enter
5. Choose all branches to include in the test (**All**)
  * **_CLI_** You will need to type **d** and hit Enter after selecting the **All** option to exit the selection dialog.

The analysis will now run for a few minutes and produce the following output

```
[BUSTED] Selected 17 branches as the test (foreground) set: Homo_sapiens,Pan_troglodytes,Node7,Gorilla_gorilla,Node6,Pongo_pygmaeus,Node5,Macaca_mulatta,Node4,Alouatta_seniculus,Node3,Otolemur_crassicaudatus,Node2,Cynocephalus_variegatus,Node1,Mus_musculus,Rattus_norvegicus 
[BUSTED] Obtaining initial branch lengths under the GTR model 
[BUSTED] Log(L) = -13512.64885365356 
[BUSTED] Fitting the unconstrained branch-site model 
```

For example, in this case the analysis inferred that 

1. A proportion of sites () is evolving with dN/dS > 1 along some of the branches
2. Forcing dN/dS = 1 provides a significantly worse (p = ) fit to the data, i.e. rejects the hypothesis of no positive selection in the alignmnent.

In addition to this output, HyPhy will also generate a [JSON](http://json.org) file with a more detailed analysis output. You can visualize the results by uploading the file to this [web app (experimental)](http://octamonkey.ucsd.edu/BUSTED/ui/busted.html).



