Selection detection.
====================

__Data files__

All the alignment files used here are included in the [data directory](data); you may find it convenient to download the [zip file](https://github.com/veg/hyphy-tutorials/blob/master/selection/data/files.zip?raw=true) with all the files from that directory and unpack it on your machine.

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

Estimate alignment-wide &omega;.
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

Run alignment-wide tests for episodic diversification (BUSTED).
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

Use aBSREL to find lineages which have experienced episodic diversification.
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

```
[INFERRED MODEL COMPLEXITY]
	mixtureTree.R20_239 has 1 site rate classes
	mixtureTree.R20_245 has 1 site rate classes
	mixtureTree.Node5 has 1 site rate classes
	mixtureTree.R20_240 has 1 site rate classes
	mixtureTree.R20_238 has 1 site rate classes
	mixtureTree.R20_242 has 1 site rate classes
	mixtureTree.Node4 has 1 site rate classes
	mixtureTree.R20_241 has 1 site rate classes
	mixtureTree.Node3 has 1 site rate classes
	mixtureTree.R20_243 has 1 site rate classes
	mixtureTree.Node2 has 1 site rate classes
	mixtureTree.R20_244 has 1 site rate classes
	mixtureTree.Node1 has 2 site rate classes
	mixtureTree.D20_233 has 2 site rate classes
	mixtureTree.D20_235 has 1 site rate classes
	mixtureTree.D20_236 has 1 site rate classes
	mixtureTree.D20_232 has 1 site rate classes
	mixtureTree.Node17 has 1 site rate classes
	mixtureTree.D20_234 has 1 site rate classes
	mixtureTree.D20_237 has 1 site rate classes
	mixtureTree.Node21 has 1 site rate classes
	mixtureTree.Node16 has 2 site rate classes
	mixtureTree.D20_230 has 2 site rate classes
	mixtureTree.D20_231 has 1 site rate classes
	mixtureTree.Node24 has 2 site rate classes
	mixtureTree.Node15 has 1 site rate classes
```

Note that only a few branches support 2 &omega; classes and the majority are well-explained without any site-to-site variation. In the next phase, aBSREL optimizes all parameters in the just inferred model model, and when that is done

```
[PHASE 2] Fitting the full LOCAL alternative model (no constraints)

Log L = -2010.311681036163 with 76 degrees of freedom, IC = 4175.206456312008
((((((R20_239:0.001181905234412956,R20_245:0.003572863589321294)Node5:0.002382159141280985,R20_240:0.003554675856702284,R20_238:0,R20_242:0.00717131672360257)Node4:0.001174549675528636,R20_241:0.003575241391516638)Node3:0.001572673086346462,R20_243:0.006743813724935903)Node2:0.00414957933238273,R20_244:0.02083895650824434)Node1:0.3137837876935897,D20_233:1.824910162480461,(((D20_235:0,D20_236:0,D20_232:0)Node17:0.00691709620521831,(D20_234:0,D20_237:0)Node21:0.005338269529420897)Node16:0.2914940662473469,(D20_230:1.412974779777337,D20_231:0.007818737526001249)Node24:0.04659201750116307)Node15:0.003377490873425993)

```

the analysis will proceed to test all the branches we selected (in step 8, which is *All*) to see if there is a proportion of sites with &omega; > 1 at that site, and whose removal would cause a significant drop in log-likelihood. As a shortcut, if the branch has no sites with &omega; > 1, it will not be tested (one can just set the p-value to 0.5). This is the most time consuming phase of the analysis. As the tests are done, aBSREL will print out a running tally to the screen, including the rate distribution inferred for a particular branch under the null (&omega; &le; 1) model, and the p-value for the branch. For example, the snippet below shows the alternative and null distributions of &omega; along Node1 (the same branch we tested with BUSTED previously), and reports the *uncorrected* p-value for the test of selection at this branch.

```
Node: mixtureTree.Node1
	Length parameter = 0.03081004564682778
	Class 1
		omega = 0.938
		weight = 0.936
	Class 2
		omega = 839.713
		weight = 0.064
...Testing for selection at this branch

Node: mixtureTree.Node1
	Length parameter = 0.0944430255269139
	Class 1
		omega = 1.000
		weight = 1.000
	Class 2
		omega = 0.960
		weight = 0.000
p-value = 6.891154313848347e-13
```

Once all the tests have been done, aBSREL will print out the list of all branches with p-values below 0.05 **after** applying th e [Holm-Bonferroni multiple testing correction](http://en.wikipedia.org/wiki/Holm–Bonferroni_method).

```
Summary of branches under episodic selection (26 were tested) :
	Node1 p = 1.860611664739054e-11
	D20_233 p = 2.454597539780501e-05
	Node16 p = 5.601789156706172e-05

```

Output files generated by aBSREL will all be of the form `PREFIX.extension` where PREFIX is whatever you chose in selection step 9 above. 

* `PREFIX.mglocal.fit` : a HyPhy batch file containing the model fit (including all parameter estimates) of PHASE 0 (only branch variation). This is a NEXUS file with a private NEXUS HYPHY block.
* `PREFIX.fit` : a HyPhy batch file containing the model fit (including all parameter estimates) of PHASE 2 (unconstrained branch-site model). This is a NEXUS file with a private NEXUS HYPHY block.
* `PREFIX.json`: a JSON file storing all the relevant analysis output, it can be visualized with this [web app](http://octamonkey.ucsd.edu/datamonkey-js-ui/aBSREL/ui/bsrel.html)
* `PREFIX`: a CSV file containing branch-by-branch output (similar to what is shown in the 'Table' tab of the web app)

Questions.

1. Which model (aBSREL or BUSTED) provides a better fit to the data, based on c-AIC?
2. Compare the &omega; distributions inferred for Node1 (the transmission branch) by BUSTED with the *a priori* branch selection, and by aBSREL. If they differ, can you identify some of the key differences between the models that could explain the difference?
3. Use the web-app to compare the list of branches which would have p-values &le; 0.05 without the multiple test correction. Are the lists notably different? 


Use FUBAR to find sites which have experienced pervasive diversification.
----------------------------------

>FUBAR is a [published method](http://mbe.oxfordjournals.org/content/30/5/1196) which is intended to supercede (by dint of its speed and statistical performance), previous REL and FEL methods. 

We continue to use the `WestNileVirus_NS3.fas` dataset from the previous example, to identify individual sites which have exprienced pervasive diversification over the entire tree. An analysis by [Brault et al](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2291521/)  using our older counting method (SLAC), found a single site subject to positive selection (249).

1. Select the appropriate analysis to run
  * **_GUI_** Choose *Analysis:Standard Analyses:Selection/Recombination:FUBAR.bf*    
  * **_CLI_** When presented with the list of standard analysis options upon launch, choose *Selection/Recombination*, then option 1 (*Detect site-specific pervasive diversifying and purifying selection using the FUBAR (Fast Unbiased Bayesian AppRoximate) method on a multiple partition data set, e.g. produced by GARD.*). Note that, as suggested by the text, FUBAR can account for the confounding effect of recombination.
2. **Universal** genetic code option
3. **1** to specify that a single partition is being analyzed (you could specify more to correct for recombination).
4. Confirm that the tree included in the file will be used
  * **_GUI_** Type **y** into the bottom box of the console window and hit Enter
  * **_CLI_** Type **y** and hit Enter
5. The file to process
  * **_GUI_** In the file dialog, navigate to and select `HIV.nex'`
  * **_CLI_** Input the full path name to the file (make sure there is no trailing space), e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data//WestNileVirus_NS3.fas`. The analysis will now begin running (see output below but more propmts await). As BUSTED and aBSREL, FUBAR will write a number of `PREFIX.exention` files to disk. `PREFIX` is the path to the alignment file in this case, and the context of h
6. Choose N to define an NxN grid (use the default 20)
  * **_GUI_** Type **20** into the bottom box of the console window and hit Enter
  * **_CLI_** Type **20** and hit Enter
7. Choose the number of MCMC chains to run (use **3**)
8. Specify Markov chain parameters (use suggested defaults, i.e. **2000000**, **1000000**, **100**, **0.05**)
  * **_GUI_** Type **3** into the bottom box of the console window and hit Enter
  * **_CLI_** Type **3** and hit Enter

  
Output after Step 5
```
FUBAR will write intermediate and result files to
/Users/sergei/Coding/hyphy-tutorials/selection/data/WestNileVirus_NS3.fas.extension

[FUBAR PHASE 1] Optimizing relative branch lengths under the nucleotide REV model
[FUBAR PHASE 1 FINISHED] log(L) = -7745.475529583914
	Length of tree 1 (substitutions/site) = 0.672169357304808
[DIAGNOSTIC] FUBAR wrote the self-contained nucleotide fit file to /Users/sergei/Coding/hyphy-tutorials/selection/data/WestNileVirus_NS3.fas.gtr_fit
```
Output after Step 6
```
[DIAGNOSTIC] FUBAR will use a 20X20 grid
[FUBAR PHASE 2] Determining appropriate branch scaling using the 20X20 grid points.
Computing the likelihood function on grid points 400/400 00:00:37	Best scaling achieved for dN/dS =  0.03.
	Computing site-by-site likelihoods at 20X20 grid points
Computing the likelihood function on grid points 400/400 00:00:42	Finished with likelihood calculations. Achieved throughput of  5.06 calculations/second
[DIAGNOSTIC] FUBAR wrote the self-contained codon fit file to /Users/sergei/Coding/hyphy-tutorials/selection/data/WestNileVirus_NS3.fas.codon_fit
[DIAGNOSTIC] FUBAR wrote the the site likelihoods file to /Users/sergei/Coding/hyphy-tutorials/selection/data/WestNileVirus_NS3.fas.grid_info
```
Output after Step 8

```
[FUBAR PHASE 3] Running an MCMC chain (ID 0) to obtain a posterior sample of grid point weights: 2000000 total steps, of which 1000000 will be discarded as burn-in, and sampling every 10000 steps. Dirichlet prior concentration parameter = 0.5.
Running MCMC chain ID 0. Current step: 2000000/2000000. Mean sampled log(L) = -6611.055623328417. Acceptance rate = 0.03164501582250791
[FUBAR PHASE 3] Running an MCMC chain (ID 1) to obtain a posterior sample of grid point weights: 2000000 total steps, of which 1000000 will be discarded as burn-in, and sampling every 10000 steps. Dirichlet prior concentration parameter = 0.5.
Running MCMC chain ID 1. Current step: 2000000/2000000. Mean sampled log(L) = -6612.133042793967. Acceptance rate = 0.02588501294250647
[FUBAR PHASE 3] Running an MCMC chain (ID 2) to obtain a posterior sample of grid point weights: 2000000 total steps, of which 1000000 will be discarded as burn-in, and sampling every 10000 steps. Dirichlet prior concentration parameter = 0.5.
Running MCMC chain ID 2. Current step: 2000000/2000000. Mean sampled log(L) = -6615.957107890772. Acceptance rate = 0.03453851726925863
[FUBAR PHASE 3 DONE] Finished running the MCMC chains; drew 3x100 samples from chains of length 2000000 after discarding 1000000 burn-in steps. Achieved throughput of  66667 moves/sec.

[DIAGNOSTIC] FUBAR wrote samples from 3 independent chains to /Users/sergei/Coding/hyphy-tutorials/selection/data/WestNileVirus_NS3.fas.samples[0-2]


Tabulating results for site 618/619 00:00:01
[DIAGNOSTIC] FUBAR wrote the results of its analysis to /Users/sergei/Coding/hyphy-tutorials/selection/data/WestNileVirus_NS3.fas.fubar.csv
```

Final results

```
[RESULTS] At posterior probability >= 0.9 there were 1 sites under diversifying positive selection, of which  0.02 [0 - 0] are expected to be false positives.

Codon	Prob[dN/dS>1]	EBF[dN/dS]>1	PSRF	N_eff
249	0.9829078732013796	452.7087197125555	1.038336288242064	36.69553290167204
```

Questions

1. Try the same analysis with different grid sizes (5,10,30). 
  * How do the run times change? 
  * Are the results robust to the choice of N?
2. Run FUBAR with using the same settings on a large HIV RT dataset (>400 sequences) `HIV_RT.nex`, which was previously analyzed by us using a [dedicated method for finding directional selection, MEDS] (http://www.ploscompbiol.org/article/info%3Adoi%2F10.1371%2Fjournal.pcbi.1002507). 
  * How does FUBAR time scale with the number of sequences?
  * How does the list of sites found by FUBAR compare with the MEDS paper?
  * And with the list of sites known for their as resistance associated for [NNRTI](http://hivdb.stanford.edu/DR/NNRTIResiNote.html) and [NRTI](http://hivdb.stanford.edu/DR/NRTIResiNote.html)?

Use MEME to find sites which have experienced episodic diversification.
----------------------------------

>MEME is a [published method](http://www.plosgenetics.org/article/info%3Adoi%2F10.1371%2Fjournal.pgen.1002764) which is our default recommendation for finding individual sites under selection. It is MUCH slower than FUBAR, however, so there's room for both. 

We continue to use the `WestNileVirus_NS3.fas` dataset from the previous example, to find sites where selection operated along a subset of branches, while the rest of the tree may have been strongly conserved (in **addition** to the type of sites found by FUBAR). 

MEME tests each individual site separately; it runs quite slowly on a desktop, but very quickly on a cluster. You may also run MEME on [datamonkey](www.datamonkey.org) to speed up the process. MEME requires a lot of user input (this is a legacy issue and will be addressed in the upcoming HyPhy v3 release).

1. Select the appropriate analysis to run
  * **_GUI_** Choose *Analysis:Standard Analyses:Selection:QuickSelectionDetection.bf*    
  * **_CLI_** When presented with the list of standard analysis options upon launch, choose *Selection/Recombination*, then option 9 (*Quickly test for positive selection using several approaches.*). 
2. **Universal** genetic code option
3. **New analysis** 
4. The file to process
  * **_GUI_** In the file dialog, navigate to and select `HIV.nex'`
  * **_CLI_** Input the full path name to the file (make sure there is no trailing space), e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data/WestNileVirus_NS3.fas`. 
4. **012345** (GTR combined with the codon model)
5. Confirm that the tree included in the file will be used
  * **_GUI_** Type **y** into the bottom box of the console window and hit Enter
  * **_CLI_** Type **y** and hit Enter
6. Save nucleotide model fit to `PREFIX.gtr`. We'll replace PREFIX is somewhere on the file system you wish to save the results to, e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data/WestNileVirus_NS3_meme`
7. **Estimate dN/dS only**
8. **MEME** (HyPhy will start running the analysis now)
9. **0.1** for the p-value (MEME is a conservative test on small alignments)
10. **N** (do not save fit files for individual codons)
11. [This prompt will appear **after** the analysis is finished] Save the CSV file with analysis results to `PREFIX.csv`, e.g. `/Users/sergei/Coding/hyphy-tutorials/selection/data/WestNileVirus_NS3_meme`


Output after step 8

```
Phase 1:Nucleotide Model (012345) Model Fit
-7745.47552958391
Phase 2:MG94x(012345) Model Fit
Phase 3:Estimating dN/dS

Nuc->codon scaling factor:3.091523288871338
Raw scaling factor:3.091523288871338
Tree scaling factor(S): 1

Using dN/dS=0.02681170805062897
Codon model:-6564.66073557536

Phase 4: Ancestral State Reconstruction and Counting
```

After step 10, for each codon, a line like this will be printed (this will also be saved to the final CSV file).

```
| Codon:  249| Beta1:       0.86| P(Beta1):  0.00| Beta2:       2.50| P(Beta2):  1.00| alpha:       0.00| LRT:   7.62| p:  0.01| Log(L): -33.85 *P
```

* &alpha; is the estimate for the synonymous rate at this site shared by all branches 
* &beta;1 is the estimate for the first non-synonymous rate; &beta;1 is always &le; &alpha;
* P(&beta;1) is the proportion of branches at that site which are estimated to evolve with with &beta;1
* &beta;2 is the estimate for the second non-synonymous rate; &beta;2 is unconstrained
* P(&beta;2) is the proportion of branches at that site which are estimated to evolve with with &beta;2
* LRT is the likelihood ratio test statistic obtained relative to the null which sets &beta;2  &le; &alpha;
* p is the p-value for positive selection at this site
* if *P is displayed at the end of the line, the p-value is at or below the threshold chosen in step 9.

Questions

1. Find sites detected as selected by MEME, but not by FUBAR. What makes them different from those which are detected by both methods?
2. Using R (or another data analysis package), plot how LRT (or p-value) varies over sites.
3. Are the p-values of MEME correlated with posterior probabilities of positive selection of FUBAR (use a non-parameteric associaton test, e.g. rank correlation).
