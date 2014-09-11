Selection detection.
====================

__Data files__

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

>BUSTED is a method we are currently preparing for publication. It has been extensively tested and shows better power and accuracy than either ["branch-site" models in PAML](http://mbe.oxfordjournals.org/content/24/5/1219.short), or the ["covarion" style models](http://mbe.oxfordjournals.org/content/early/2013/10/16/molbev.mst198)

We will perform branch-site model-based tests for episodic selection affecting a proportion of sites in the alignment along a proportion of branches in the tree (i.e. is there evidence of selection **somewhere** in the alignment). The data set in we are using includes partial clonal HIV-1 env sequences from epidemiologically linked partners (source and recipient)

1. Select the appropriate analysis to run
  * **_GUI_** Choose *Analysis:Standard Analyses:Positive Selection:BUSTED.bf*    
  * **_CLI_** When presented with the list of standard analysis options upon launch, choose *Positive Selection*, then option 4 (*Run the Branch-site Unrestricted Statistical Test for Episodic Diversification to test for evidence of episodic alignment-wide selective pressure.*)
2. **Universal** genetic code option
3. The file to process
  * **_GUI_** In the file dialog, navigate to and select `HIV.nex'`
  * **_CLI_** Input the full path name to the file (make sure there is no trailing space), e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data/HIV.nex`
4. Confirm that the tree included in the file will be used
  * **_GUI_** Type **y** into the bottom box of the console window and hit Enter
  * **_CLI_** Type **y** and hit Enter
5. Choose all branches to include in the test (**All**)
  * **_CLI_** You will need to type **d** and hit Enter after selecting the **All** option to exit the selection dialog.

The analysis will now run for a few minutes and produce the following output

```
[BUSTED] Selected 26 branches as the test (foreground) set: R20_239,R20_245,Node5,R20_240,R20_238,R20_242,Node4,R20_241,Node3,R20_243,Node2,R20_244,Node1,D20_233,D20_235,D20_236,D20_232,Node17,D20_234,D20_237,Node21,Node16,D20_230,D20_231,Node24,Node15 
[BUSTED] Obtaining initial branch lengths under the GTR model 
[BUSTED] Log(L) = -2114.132336771765 
[BUSTED] Fitting the unconstrained branch-site model 
[BUSTED] Log(L) = -2039.990744000631. Unrestricted class omega = 105.3390132524982 (weight = 0.0202977472726123) 
[BUSTED] Fitting the branch-site model that disallows omega > 1 among foreground branches ```
```

For example, in this case the analysis inferred that 

1. A proportion of sites (0.02) is evolving with dN/dS > 1 (105) along a subset of the branches (it is not known which).
2. Forcing dN/dS = 1 provides a significantly worse (p = ) fit to the data, i.e. rejects the hypothesis of no positive selection in the alignmnent.

In addition to this output, HyPhy will also generate a [JSON](http://json.org) file with a more detailed analysis output. The JSON will be written to same directory as the input alignment file, with `BUSTED.json` appended to the file name, e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data/HIV.nex.BUSTED.json`  You can visualize the results by uploading the file to this [web app (experimental)](http://octamonkey.ucsd.edu/BUSTED/ui/busted.html).

### Testing for selection on an *a priori* specifed background

The tree in the `HIV.fas` is annotated with {} to indicate the set of test (foreground) branches; in this case the branch being tested is the *transmission* branch, i.e. the one separating the source and the recipient in the phylogenetic tree. BUSTED will only constrain &omega; < 1 on these branches (allowing the rest of the tree to have its own &omega; distribution) during testing.

An annotated Newick string looks like this:

>((((((R20_239:0.001179071552709126,R20_245:0.003569393318767422):0.002373643652152119,R20_240:0.00354445225954759,
>R20_238:0,R20_242:0.007143686359514547):0.001169032517101171,R20_241:0.003555888002841892):0.001829250056707198,
>R20_243:0.006486065374683752):0.003845820830922537,R20_244:0.02113434306810657)**{Test}**:0.03269082780807394,
>D20_233:0.02550919363771013,(((D20_235:0,D20_236:0,D20_232:0):0.006433904687642939,
>(D20_234:0,D20_237:0):0.005843978498632621):0.01022675723558638,
>(D20_230:0.02979851732996924,D20_231:0.006905678660095517):0.02444611465196596):0.005946252173834307);

Repeat the analysis from the previous section, choosing option 4 (**Set Test**) in step 5. Note that you could also manually select the set of branches to test in the same dialog. 

The results of this *a priori* analysis are

```
[BUSTED] Selected 1 branches as the test (foreground) set: Node1 
[BUSTED] Obtaining initial branch lengths under the GTR model 
[BUSTED] Log(L) = -2114.132336771765 
[BUSTED] Fitting the unconstrained branch-site model 
[BUSTED] Log(L) = -2031.317686315219. Unrestricted class omega = 509.675292896259 (weight = 0.07817272825843137) 
[BUSTED] Fitting the branch-site model that disallows omega > 1 among foreground branches 
[BUSTED] Log(L) = -2050.106555576094 
[BUSTED] Likelihood ratio test for episodic positive selection, p = 4.392065044989124e-10 
```

Questions.

1. Explain why the log-likelihood for the unconstrained model is higher for the case when *a priori* branches are tested? 
2. Do these results suggest that the transmission branch is evolving differently from the rest of the tree?
3. If the a priori analysis had a negative result (no selection on the transmission branch), might it still be possible to find evidence of selection in the **All** branches analysis?

Using aBSREL to find lineages which have experienced episodic diversification.
----------------------------------

>aBSREL is a method we are currently preparing for publication. It is an extension of our popular [BS-REL model](http://www.ncbi.nlm.nih.gov/pubmed/21670087), which performs a complexity analysis and model selection prior to doing hypothesis testing. It runs much faster than BS-REL and has better statistical properies.

We continue using the `HIV.nex` dataset from the previous example, but now we are interested in scanning the phylogeny for all the branches where selection may have operated.  

1. Select the appropriate analysis to run
  * **_GUI_** Choose *Analysis:Standard Analyses:Positive Selection:BranchSiteREL.bf*    
  * **_CLI_** When presented with the list of standard analysis options upon launch, choose *Positive Selection*, then option 1 (*Use the random effects branch-site model (2010) to find lineages subject to episodic selection.*)
2. **Universal** genetic code option
3. **Yes** to choose the adaptive version of BSREL.
4. **No** to assume that synonymous rates do not vary from site to site
5. The file to process
  * **_GUI_** In the file dialog, navigate to and select `HIV.nex'`
  * **_CLI_** Input the full path name to the file (make sure there is no trailing space), e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data/HIV.nex`
6. Decline to use the tree included in the file (annotation from the previous step conflicts with the current aBSREL implementaton)
  * **_GUI_** Type **n** into the bottom box of the console window and hit Enter
  * **_CLI_** Type **n** and hit Enter
7. Choose the tree file
  * **_GUI_** In the file dialog, navigate to and select `HIV.nwk'`
  * **_CLI_** Input the full path name to the file (make sure there is no trailing space), e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data/HIV.nwk`
8. Choose all branches to test (**All**)
  * **_CLI_** You will need to type **d** and hit Enter after selecting the **All** option to exit the selection dialog.
9. Where to save the analysis results (more than one file, see below)
  * **_GUI_** In the file dialog, find a place to save the result file, naming it `HIV.aBSREL`.
  * **_CLI_** Input the full path name to the file (make sure there is no trailing space), e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data/HIV.aBSREL`

The analysis will now run for several minutes and produce a lot of diagnostic output. 

As the initial phase, aBSREL fits the standard Muse-Gaut 94 model which estimates a single &omega; for each branch and prints out model fit statistics. This is the simplest model that can be selected by aBSREL.

```
[PHASE 0] Fitting the local MG94 (no site-to-site variation) to obtain initial parameter estimates

Log L = -2069.678248355542 with 66 degrees of freedom. IC = 4273.304085347947

Branch omega values

	Count    = 26
	Mean     = 5.015095686511051
	Median   = 1.91176633672278
	Variance = 20.26920614013531
	Std.Dev  = 4.502133509807912
	COV      = 0.8977163729731343
	Sum      = 130.3924878492873
	Sq. sum  = 1160.660956869788
	Skewness = 0.8548558502250386
	Kurtosis = 58.55207161779911
	Min      = 0.1475094738891478
	2.5%     = 0.1475094738891478
	97.5%    = 10
	Max      = 10
	```

Next, aBSREL sorts all the branches by length (longest first), and tries to greedily add &omega; categories to one branch at a time, until the addition is no longer justified by AIC-c scores. For example, for *Node1*

```
[PHASE 1] Fitting Branch Site REL models to one branch at a time

[PHASE 1] Branch Node1 log(L) = -2048.441, IC = 4234.950
	2 rate clases
	Node: mixtureTree.Node1
	Length parameter = 0.01897377361517674
	Class 1
		omega = 0.395
		weight = 0.925
	Class 2
		omega = 323.707
		weight = 0.075

[PHASE 1] Branch Node1 log(L) = -2048.446572827957, IC = 4239.084020683465
	3 rate clases
	Node: mixtureTree.Node1
	Length parameter = 0.01917763880438389
	Class 1
		omega = 0.371
		weight = 0.917
	Class 2
		omega = 0.348
		weight = 0.007
	Class 3
		omega = 317.478
		weight = 0.076
```

using two rate classes improves the IC from 4273.3 to 4234.950, but going to three rate classes is not justified; aBSREL will now fix a 2-bin &omega; distribution for Node1 and move to the next branch. When all branches are done, a summary of inferred model complexity will be printed to the screen.
