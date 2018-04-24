Intratumoral heterogeneity
----------------------------------------------------------
<img src="images/jamal-hanjani2015_1ab.png" width=60%/ style="margin-bottom: 0px; display:block">
<div style="margin-bottom: 20px; font-size: .5em; text-align: center">Image from Jamal-Hanjani *et al.*, Clin. Canc. Res., 2015</div>

- Cells within the same tumor vary:
  - variation in environment may cause difference in phenotype
  - variation in genotype/epigenetics may cause difference in phenotype  
- Different clones respond differently to treatment


Source of intratumoral heterogeneity
-----------------------------------------------
<div style="position:relative; width:100%;  margin-left: auto; margin-right: auto; text-align: center; margin-top: 30px" >
  <div style="position:absolute;background: white;width:100%;height:600px">
  <img src="images/CSC_vs_stochastic_vert.svg" width="100%"/>
  <div style="font-size: .5em; text-align: center; margin-bottom: 20px">Image adapted from https://en.wikipedia.org/wiki/Tumour_heterogeneity</div>
  </div>
  <div class="fragment" style="position:absolute;width:100%;background: white;height:600px">
  <img src="images/CSC_vs_stochastic_vert.svg" width="80%"/>
  <div style="font-size: .5em; text-align: center; margin-bottom: 20px">Image adapted from https://en.wikipedia.org/wiki/Tumour_heterogeneity</div>

  <div style="text-align: left; margin-top: 10px; margin-bottom: -10px;">How to identify the *correct* hypothesis?</left>
  <ul>
  <li> Build computational model for each hypothesis </li>
  <li> Compare: </li>
    <ul>
    <li> *in vitro* development of tumor cell population (published data) </li>
    <li> *in silico* development of tumor cell population in matching experiment </li>
    </ul>
  </ul>
  </div>  
</div>


Iterated growth & passage experiment
-----------------------------------------------------------
<img src="images/setup.svg" height="250" style="display:block"/>
<div style="text-align: left; font-size: 80%; margin-bottom: -20px"/>
Experimental setup as described in Porter *et al.* (Gen. Biol., 2014):
</div>
- Preparation
  - Barcodes are inserted in the DNA using a lentiviral vector
  - Infected cells are selected (using a GFP tag) and grown
  - Three cell populations, each containing 3&#x22C5;10&#x2075;, cells are taken
- Experiment (three biological replicates)
  - Each population grows for 3 days, after which 4&#x22C5;10&#x2076; are present
  - 3&#x22C5;10&#x2075; cells are passed on to the next generation


Iterated growth & passage experiment
-----------------------------------------------------------
<div style="text-align: left; font-size: 80%;"/>
We re-analyzed the experiments from Porter *et al.* (Gen. Biol., 2014), using the FASTQ files in the NIH Sequence Read Archive.
</div>

<img width="100%" src="images/K562_popstats_1.svg" style="display:block"/>
* K562 cell (chronic myelogenous leukemia cell line)
* Clones disappear and clonal dominance increases



Computational model of simple growth & passage
------------------------------------------------------------------
<img data-src="images/setup.svg" height="250" style="display:block;"/>
* Initialization
  * ~12.000 clones with size $c_i$ and $\sum \_i c_i = 3 \cdot 10^5$.
  * Clone sizes assigned too fit the experimental data.
* Growth
  * Each cell grows with a given rate $r_i$
  * Growth continues until $\sum \_i c_i = 4 \cdot 10^6$
* Passage
  * $3 \cdot 10^5$ cells are taken randomly and passed to the next generation


Simulations with stochastic growth & passage
------------------------------------------------------------------
* All cells growth with rate $r$
  * deterministic: $c_i(t+\Delta t) = c_i(t) e^{r \Delta t}$
  * stochastic: $c_i$ evolves with &#x03C4;-leaping Gillespie algorithm
<div style="margin:0 auto; text-align:center">
<img data-src="images/simple_growth_all.svg" width="100%" style="margin-left:-250px"/>
* Clones disappear at a rate similar to that *in vitro*
* Clonal dominance does not develop



Test hypotheses for clonal dominance
------------------------------------------------------------------
<div style="position:relative; width:100%;  margin-left: auto; margin-right: auto; text-align: center; margin-top: 30px" >
  <img data-src="images/CSC_vs_stochastic_1.svg" width="100%"/>
  <div style="font-size: .5em; text-align: center; margin-bottom: 20px">Image adapted from https://en.wikipedia.org/wiki/Tumour_heterogeneity</div>
</div>


Model with cancer stem cells
-------------------------------------------------------------
<div style="text-align: center; font-size: .5em">
<img src="images/csc_model.svg" width="80%" style="display:block"/>
model based on Weekes *et al.*, Bull. Math. Biol., 2014
</div>

<div style="margin-top:60px">
  <div style="float:left; width:58%; margin-top:15px">
    <ul>
      <li>Parameterization based on analytical solution</li>
      <li> Monotonic growth for p&#x2081; > p&#x2083; </li>
      <li> Population growth rate depends on r<sub style="font-size: .8em">DC</sub> and maximum DC age (M)</li>
    </ul>
  </div>
  <div style="float:left;">
  <img src="images/weekes_model_pars_heatmap_YlOrRd_r.svg" width="380px"  style="float:right; margin-top: -60px"/>
  </div>
</div>


Model with cancer stem cells
-------------------------------------------------------------
<img src="images/it_gotl_csc_altpar_all.svg" width="100%"/>
<ul>
  <li>Cancer stem cells do not induce clonal dominance</li>
  <li>Almost all clones disappear</li>
</ul>


Model with cancer stem cells
-------------------------------------------------------------
<img src="images/it_gotl_csc_fleft_heatmaps.svg" width="90%" style="margin-top: -20px;"/>
<img src="images/it_gotl_csc_gini_heatmaps.svg" width="90%" style="margin-top: -20px;"/>



Test hypotheses for clonal dominance
------------------------------------------------------------------
<div style="position:relative; width:100%;  margin-left: auto; margin-right: auto; text-align: center; margin-top: 30px" >
  <img data-src="images/CSC_vs_stochastic_2.svg" width="100%"/>
  <div style="font-size: .5em; text-align: center; margin-bottom: 20px">Image adapted from https://en.wikipedia.org/wiki/Tumour_heterogeneity</div>
</div>
* Clonal evolution: division rate mutation
* Mutation requires tracking of individual cells


Agent based model (ABM) with with clonal evolution
-------------------------------------------------------------
* Cell $i$ has a division rate $r_i$ and a barcode.
* Initial variation to mimic evolution before experiment:
  * $r_i = rY$ with $Y$ taken from &#x1d4a9; (1,&sigma;<sub>r</sub>&#x00B2;)
* Division
  * division rate mutates: $r \_\text{child} = r \_\text{parent} X $ with $X$ taken from &#x1d4a9; (1,&sigma;<sub>m</sub>&#x00B2;)
* Division rate increases during the experiment
    <img src="images/it_abm_sim_mut_vdivrate_0792_divrates.svg" width="60%"/>


Iterated growth & passage with clonal evolution
-------------------------------------------------------------
* Clone loss increases with division rate variation
<img src="images/it_abm_sim_mut_vdivrate_1-120_heatmap_fleft.svg" width="90%" style="margin-bottom: -50px; margin-top: -20px;">

* Gini coefficient increases with division rate variation
<img src="images/it_abm_sim_mut_vdivrate_1-120_heatmap_gini.svg" width="90%" style=" margin-top: -20px;">



Matching ABM to *in vitro* results for K562
------------------------------------------------------------------
- Maximum likelyhood estimation that includes the 3 time points
<img src="images/it_abm_sim_mut_vdivrate_364-484_fit.svg" width="100%" style="float:left"/>

- Results for best fit for Gini coefficient
<img src="images/it_abm_sim_mut_vdivrate_364-484_best_fit.svg" width="100%" style="float:left"/>


Model does not reproduce clonal overlap
------------------------------------------------------------------
<img src="images/it_abm_sim_mut_vdivrate_364-484_major_clones.svg" width="70%" style="display: block;"/>

* No clonal overlap in the simulation because of initialization:
  * Simulation initialization: large population with clones distributed based on data at P0
  * Actual initialization: cells growth for 7-8 days after barcodes are inserted
* **There should be correlation between division rates for cells of the same clone**



*In vitro* results for clonal K562
-------------------------------------------
* clonal K562 cell line is derived from a single cell

<img src="images/K562_VS_clonalK562.svg" width="75%"/>

* Less clone loss compared to K562 cell line
* No development of clonal dominance


Matching ABM to clonal K562 results
---------------------------------------------
* Expectations:
  * Less initial variation &#x21d2; lower &sigma;<sub>r</sub> than for K562
  * Same cell type &#x21d2; similar &sigma;<sub>m</sub> as with K562

<div class="fragment">
  <ul><li>Changes as expected:</li></ul>
  <div style="width:50%; float:left">
  <img src="images/it_abm_sim_mut_vdivrate_fit_clonalK562.svg" width="100%"
  style="margin-top:0px; margin-bottom:-20px; margin-left:0px"/>
  </div>
  <div style="width:49%; float:left; font-size:65%; margin-top:20px">
  <table>
    <tr><th></th><th>clonal K562</th><th>K562</th></tr>
    <tr><td>&sigma;<sub>r</sub></td><td>0</td><td>0.036</td></tr>    
    <tr><td>&sigma;<sub>m</sub></td><td>0.002</td><td>0.0018</td></tr>
    <tr><td>min(MLE)</td><td>~2000</td><td>~5</td></tr>
  </table>
  </div>  
</div>


Matching ABM to clonal K562 results
----------------------------
<img src="images/it_abm_sim_mut_vdivrate_fit_clonalK562_metrics.svg" width="100%"
style="margin-left=50px; margin-top:-20px; margin-bottom:-20px"/>

* Both clone loss is hard to match (min(MLE) = ~2000)
* Gini coefficient matches better (min(MLE) = ~5)

<img class="fragment" src="images/it_abm_sim_mut_vdivrate_best_fit_clonalK562.svg" width="100%" style="margin-left:50px; margin-top:-20px"/>



*In vitro* results for HeLa cells
--------------------------------------------
<img src="images/K562_VS_HeLa.svg" width="75%"/>

* Clone loss starts late
* Clonal dominance develops similar to K562 cell line


Matching ABM to HeLa results
------------------------------------------
<img src="images/it_abm_sim_mut_vdivrate_fit_HeLa_metrics.svg" width="100%" style="float:left"/>
<img src="images/it_abm_sim_mut_vdivrate_best_fit_HeLa.svg" width="100%"/>
<div style="text-align:center">Better fit for Gini coefficient</div>



Conclusion
------------------------------
* Model based on cancer stem cells does not match *in vitro* iterated growth and passage
* Model based on clonal evolution can match *in vitro* iterated growth and passage
  * Model fits well to changes in clone size distribution observed *in vitro*
  * Model predicts same mutation dynamics for polyclonal and monoclonal K562 cells
  * Model fails to predict correct clone loss for monoclonal K562 and HeLa cells
  * Model fails to reproduce major clone overlap



Publication
------------------------------------------
[Palm MM, Elemans M, Beltman JB (2018) Heritable tumor cell division rate heterogeneity induces clonal dominance. PLoS Comput Biol 14(2): e1005954. https://doi.org/10.1371/journal.pcbi.1005954](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005954)
