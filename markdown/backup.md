Lineage tracing with genetic barcodes
-----------------------------------------------
- construct with random base pair sequence

<img src="images/barcode_vector.svg" width="50%" style="margin-left:80px"/>

- construct is inserted, e.g. with a virus vector

<img src="images/barcoding_diagram.svg" width="100%" style="margin-left:80px"/>



Tau-leaping interval
-----------------------------
<img src="images/it_gotl_sim_tau.svg" width="100%"/>



Model with CSC and division rate heterogeneity
-------------------------------------------------------------
<img src="images/it_gotl_csc_vdivrate_0012.svg" width="100%" style="margin-top: -20px"/>

  <div class=" myblock" style="clear:both; margin: 0 auto; margin-top: 10px; width: 100%">
  Division rate heterogeneity induces clonal dominance, but does not reduce excessive clone loss
  </div>


Model with CSC and division rate heterogeneity
-------------------------------------------------------------

<ul style="margin-top: -10px">
  <li>Division rate standard deviation determines clonal dominance</li>
</ul>
<img src="images/it_gotl_csc_vdivrate_var_sigma.svg" width="60%" style="margin-top: -25px"/>

<div class="fragment fade-up" data-fragment-index="1" style="margin-top: -50px">
  <ul><li>CSC&#x2080; and p&#x2081; determine clone loss</li></ul>
  <img class="fragment fade-up" data-fragment-index="1" src="images/fleft_heatmaps.svg" width="100%" style="margin-top: -20px"/>

  <div class="myblock" style="width:100%; clear:both; font-size:100%; margin: 0 auto; margin-top: -10px">
  Best fit with 100% CSCs that only divide into CSCs.
  </div>
</div>



Alternative division rate distribution
--------------------------------------------------------
<img src="images/it_gotl_sim_vdivrate_lognormal_var_growthrate.svg" width="100%"/>


Clonal K562 clone loss cannot be matched
---------------------------------------------------------------
* Minimal clone loss for a model without any division rate variation
* Clone loss observed with clonak K562 is larger than that in a simulation without division rate variation
<img src="images/cK562_vs_simple_growth.svg" width="100%"/>
