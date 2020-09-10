




# Results

<!-- Exploratory Data Analysis
child doc is loaded in-line -->

## Explororatory Data Analysis of SBBS survey data

Where relevant a protocol for exploratory data analysis was followed [@Zuur2010-kp] to ensure that before any problems in the structure of the data are identified prior to undertaking any statistical analysis.

### Survey effort over time

The spatial location of surveyed squares is shown in Figure \@ref(fig:spatSum). It seems that there has been ongoing surveying effort in the south and central mainland and on the islands of Unst, Bressay and Noss, but less coverage elsewhere.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/spatSum-1.png" alt="Number of years a SBBS 1km square was survyered (n) between 2002 and 2019" width="768" />
<p class="caption">(\#fig:spatSum)Number of years a SBBS 1km square was survyered (n) between 2002 and 2019</p>
</div>

### Outliers

The *Cleveland dot plot* [@Zuur2010-kp] is a chart in which the row number of an observation is plotted versus the observation variable, thereby providing a more detailed view of individual observations than a boxplot. Points that stick out on the right-hand side, or on the left-hand side, are observed values that are considerably larger, or smaller, than the majority of the observations. Figure \@ref(fig:countDotPlot) appears to show that there are no major outliers across all species, but that there are many counts equal to zero indicating that the data might be zero-inflated.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/countDotPlot-1.png" alt="Cleveland dot plot of species counts in Shetland BBS data from 2002 to 2018 " width="672" />
<p class="caption">(\#fig:countDotPlot)Cleveland dot plot of species counts in Shetland BBS data from 2002 to 2018 </p>
</div>

### Testing for normality

A large number of statistical regression techniques assume normality. Visualising the SBBS count data as a histogram can help assess if it is normally distributed. This is shown in the plot in Figure \@ref(fig:normality).

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/normality-1.png" alt="Histogram of SBBS count data across all years, by species" width="672" />
<p class="caption">(\#fig:normality)Histogram of SBBS count data across all years, by species</p>
</div>

Inorder to validate the outcome of the plots in Figure \@ref(fig:normality) a significance test was undertaken and the results are shown in Table \@ref(tab:normSig).


Species            W   p-value
--------  ----------  --------
OC         0.8628058         0
L          0.7546102         0
CU         0.8327195         0
RK         0.6995970         0
SN         0.8000661         0

The p-value for each species in \@ref(tab:normSig) is << 0.05. This suggests that the count data for all species are significantly different from the normal distribution.

### Poisson distribution and zero inflation

The histograms of species counts in Figure \@ref(fig:normality) suggest that count data is poisson distribution. Also there are a significant number of zeros in the count data, for all species. This suggests that the zero-inflation poisson distribution describes the data. Table \@ref(tab:zipTest) below shows the results of a significance test [@Van_den_Broek1995-ml] for zero inflation in a poisson distribution.


Species    Expected zeros   Zeros observed   Chi squared   p-value
--------  ---------------  ---------------  ------------  --------
CU               223.9173              433      384.2445         0
L                323.5230              585      547.5071         0
OC               119.1142              309      446.9641         0
RK               520.3458              694      271.6801         0
SN               134.4406              359      577.9990         0

All results have a significant statistical significance (p<0.05) and therefore the count distribution across species is assumed to be a zero-inflated poisson process. The statistical modelling methods used on the data must support a poisson distribution and zero inflation where possible.

### Homogeniety of variance

Homogeneity of variance within the data is an important assumption in analysis of variance (ANOVA) and other regression-related models. The series of boxplots in Figure \@ref(fig:homoVariance) show how counts across all surveyed BBS squares vary across years 2002 to 2018, for each breeding wader species.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/homoVariance-1.png" alt="Box plot showing variance of counts across all surveyed Shetland BBS squares and all years, by species" width="672" />
<p class="caption">(\#fig:homoVariance)Box plot showing variance of counts across all surveyed Shetland BBS squares and all years, by species</p>
</div>

To test the homogeneity of variance of species counts between years, for each species, we can apply the Fligner-Killeen test. This is used as the count data are shown to be non-normal. Table \@ref(tab:fKTest) shows the results of the test applied to the Shetland BBS data. For p-values > 0.05 the data variance are homogeneous.


Table: (\#tab:fKTest)Fligner-Killeen test of homogeneity of variance for Shetland SBBS species counts, across all years

Species    Chi-squared     p-value   df
--------  ------------  ----------  ---
OC            18.11614   0.3171401   16
L             29.11514   0.0231712   16
CU            18.36325   0.3030590   16
RK            26.72879   0.0445979   16
SN            47.40824   0.0000588   16


Lapwing, Redshank and Snipe variances are heterogeneous according to the test results in Table \@ref(tab:fKTest). The solution to heterogeneity of
variance is to transform the response variable to stabilize the variance year-on-year, or applying statistical regression techniques that do not require homogeneity. 

### Status of surveys between 2002 and 2019



Before any detailed statistical modelling was undertaken a simple analysis into how the population changed in each surveyed 1km square between 2002-2011 and 2012-2019. The 1 km squares shown (n=139) were those surveyed in both periods and where farmland waders colonized, increased, remained stable, declined or went extinct. This gave an initial view as to potential population trends between the two stated periods. Figure \@ref(fig:popStatusChg) shows the state changes between the two analysis periods.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/popStatusChg-1.png" alt="Population status change per Shetland BBS square - between 2002-10 and 2011-19" width="672" />
<p class="caption">(\#fig:popStatusChg)Population status change per Shetland BBS square - between 2002-10 and 2011-19</p>
</div>
Figure \@ref(fig:aggPopChg) below shows an aggregation of certain categories; whereby extinct and decreased are grouped, and colonised and increased are grouped.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/aggPopChg-1.png" alt="Aggregate population status change per Shetland BBS square - between 2002-10 and 2011-19" width="672" />
<p class="caption">(\#fig:aggPopChg)Aggregate population status change per Shetland BBS square - between 2002-10 and 2011-19</p>
</div>
### Survey  Bootstrap

Shetland BBS volunteers were able to choose which squares they surveyed. The survey squares are therefore not randomly allocated across the Shetland archipelago. As a result of this non-randomised allocation there could be potential bias in the habitat types surveyed; for example, in-bye is closer to roads and housing than upland habitats. To test this a bootstrap of percentage cover of EUNIS habitat categories D, E and F (see \@ref(tab:eunisTable)) across all OS 1km squares was undertaken, and then compared to a bootstrap of the same data, but only those OS squares surveyed by volunteers as part of the Shetland BBS.


<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/bootstrap-1.png" alt="Mean % cover per 1km$^2$ of EUNIS habitat types D, E and F, bootstrap sample of OSGB squares v boostrap of surveyed squares. R=1000" width="672" />
<p class="caption">(\#fig:bootstrap)Mean % cover per 1km$^2$ of EUNIS habitat types D, E and F, bootstrap sample of OSGB squares v boostrap of surveyed squares. R=1000</p>
</div>

This shows that grassland and heathland are significantly oversampled within the Shetland BBS surveys.

##  Detectability

The `r` package `unmarked` was used to generate an estimate for the probability of detection, or *detectability*. Table \@ref(tab:detectabilityTab) shows the average *detectability* across all survey years, for each species.


Species    Detectability
--------  --------------
OC                 0.803
L                  0.723
RK                 0.667
CU                 0.831
SN                 0.723

<!-- Improved grassland classification
child doc is loaded in-line -->



## Improved grassland classification

The results below detail how remotely sensed satellite data was processed using a Support Vector Machine to generate a classification for improved grassland across the various islands of Shetland.

### Shetland Sentinel 2 satelitte dataset

A Sentinel 2 satellite spatial dataset was clipped using the Integrated Administration And Control System (IACS) field boundary shapefile for Shetland. This gave a spatial dataset comprising of land-based habitat only, excluding built areas and roads, as shown in Figure \@ref(fig:plotSentRGB)  



<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/plotSentRGB-1.png" alt="Clipped Sentinel 2 RGB composite of Shetland" width="672" />
<p class="caption">(\#fig:plotSentRGB)Clipped Sentinel 2 RGB composite of Shetland</p>
</div>






### Sentinel 2 spectral bands used in habitat classification

The Sentinel dataset is represented as a layered set of images (a raster) known as a `RasterBrick` [@raster]. Each raster layer is a spatial representation of one of 11 different spectral sensor readings. The sensors used within the Shetland sentinel dataset are shown in Table \@ref(tab:satBands). 


Band ID   Name         Wavelength(micrometer)
--------  ----------  -----------------------
1         Aerosol                       0.443
2         Blue                          0.490
3         Green                         0.560
4         Red                           0.655
5         Veg Red 1                     0.705
6         Veg Red 2                     0.865
7         Veg Red 3                     0.740
8         NIR                           0.783
8A        Veg Red 4                     0.842
11        SWIR 1                        1.610
12        SWIR 2                        2.190

### Habitiat classification training data

In order to classify improved grassland, four other distinctive and closely associated habitat types were classified: unimproved grassland, crops, bare peatland and upland. A number of areas representative of each habitat type were selected as can be seen in Figure \@ref(fig:habitatTraining). 


```
## Reading layer `Training_samples' from data source `/Users/anthony/Documents/GitHub/shetlandwaders/data/training_data_classification/Training_samples.shp' using driver `ESRI Shapefile'
## Simple feature collection with 161 features and 2 fields
## geometry type:  POLYGON
## dimension:      XY
## bbox:           xmin: 415800.5 ymin: 1108793 xmax: 466132.7 ymax: 1217616
## CRS:            EPSG:27700
```

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/habitatTraining-1.png" alt="Habitat classification training areas" width="672" />
<p class="caption">(\#fig:habitatTraining)Habitat classification training areas</p>
</div>

### Sampling of habitat training classes

Each habitat training dataset was randomly sampled in order to train a support vector machine classifier. Distributions for the sampled data for each training set are shown in Figure \@ref(fig:plotSampleDistributions). The NIR and red vegetation spectra appear to be the most distinct across different habitat types. 

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/plotSampleDistributions-1.png" alt="Sampled distributions for each training class, from the Sentinel 2 dataset of the Shetland landmass" width="672" />
<p class="caption">(\#fig:plotSampleDistributions)Sampled distributions for each training class, from the Sentinel 2 dataset of the Shetland landmass</p>
</div>
### Support vector machine classifier training

The SVM was trained to classify the five target habitat classes so that improved grassland can be separated and used as a covariate in wader response modelling.















### Search grid parameterisation

The SVM parameters used to create a number of different models are shown in Table \@ref(tab:searchGrid).


RBF sigma   Cost 
----------  -----
0.11        18   
0.12        18   
0.13        18   
0.11        19   
0.12        19   
0.13        19   
0.11        20   
0.12        20   
0.13        20   







### Best model results by root mean squared error

The best SVM model parameters, as measured by classification accuracy, are shown in Table \@ref(tab:modelResults). Root-mean squared error (RMSE) was used to select the best fitting model. 


 Cost   RBF sigma    Accuracy          se
-----  ----------  ----------  ----------
   20        0.13   0.8233010   0.0094407
   19        0.13   0.8208738   0.0093362
   18        0.13   0.8194175   0.0093179
   19        0.12   0.8194175   0.0091478
   20        0.12   0.8194175   0.0090903

Figure \@ref(fig:viewMetrics) shows the parameters associated with each model fit and the resulting rmse used in the 10-fold cross validation against the trading data. 

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/viewMetrics-1.png" alt="RMSE for each model fit, as a function of model parameters `mtry` cost and `rbf_sigma`" width="672" />
<p class="caption">(\#fig:viewMetrics)RMSE for each model fit, as a function of model parameters `mtry` cost and `rbf_sigma`</p>
</div>




### Evaluate model performance using test data

A training data set was tested against the best model fit. The results of classifier accruracy are shown in Table \@ref(tab:evalPerf).


Metric     Estimate  
---------  ----------
accuracy   0.8534091 
kap        0.8240900 

The confusion matrix in Figure \@ref(fig:confusionMatrix) shows the results of the model prediction for each habitat class against thsoe of the test data set. The most incorrectly classified habitat is improved grassland versus crop, followed by Upland versus Bare Peatland. Both of these inaccuracies are not significant to the objective of producing an overall classification for improved grassland, in that crop habitat is often reseeded impproved grassland.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/confusionMatrix-1.png" alt="Confusion Matrix from classificaton of test dataset" width="672" />
<p class="caption">(\#fig:confusionMatrix)Confusion Matrix from classificaton of test dataset</p>
</div>




### Classification across all Shetland habitat

The best fit model was then used across the raster dataset for all of Shetland, to enable classification of all habitat. The results are shown in \@ref(fig:plotPredictionShet). The improved grassland and crop habitat is predominantly in the south of the island. It can be seen that the main middle island, Yell, is predominantly upland and bare peat.



<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/plotPredictionShet-1.png" alt="Classification of Shetland habitat in order to determine the location of improved grassland" width="672" />
<p class="caption">(\#fig:plotPredictionShet)Classification of Shetland habitat in order to determine the location of improved grassland</p>
</div>

<!-- Environmental Covariate Analysis
child doc is loaded in-line -->

## Environmental covariate analysis

Each of the covariates described in {#environmental-covariates} was generated for each Shetland BBS squares (n=3992). 

### Histogram of environmental covariates 

Figure \@ref(fig:covarHisto) shows histograms of for these covariates for data taken across all Shetland OS GB 1km squares. It can be seen that bog type habitat predominates across Shetland, and that majority of the landscape is at less than 100m elevation. The mode for the pH is around 4, which is typical for acidic peatland [@Paterson2011-ky]. The topsoil carbon content shows that the majority of the Shetland soils have a high organic carbon content, that is typical of peatland [@Paterson2011-ky]. In contrast a typical mineral rich soil in England would have c.3-5% organic carbon content.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/covarHisto-1.png" alt="Histograms of environmental covariates across all of Shetland" width="672" />
<p class="caption">(\#fig:covarHisto)Histograms of environmental covariates across all of Shetland</p>
</div>

### Histogram of environmental covariates for Shetland BBS squares only

This can be contrasted with covariate histograms for only those OS squares (n=139) that were surveyed as part of the Shetland BBS, as seen in Figure \@ref(fig:sbbsHisto). It seems across all nesting wader species, there is a preference for wet but not water-logged habitat as seen in the AWC histogram. Also, the majority of breeding waders appear to nest within 1km of the coast. It appears that breeding waders also have a preference for grassland (both improved and unimproved) presents the majority of the habitat cover, over heathland.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/sbbsHisto-1.png" alt="Histograms of environmental covariates across only those squares surveyed as part of the Shetland BBS" width="672" />
<p class="caption">(\#fig:sbbsHisto)Histograms of environmental covariates across only those squares surveyed as part of the Shetland BBS</p>
</div>

### Density plots

Density plots of all environmental covariates across Shetland BBS squares (n=139) are shown in Figure \@ref(fig:densityPlot). These figures provide an overlay to the histogramsin {#histogram-of-environmental-covariates-for-shetland-bbs-squares-only}, and represent a smoothed version of a histogram to show the probability density function of the variable. Some distributions are highly skewed, such as distance to sea and elevation. Whilst other covariates like topsoil organic carbon and bog cover are largely a uniformly distributed. None of the covariates appear to be normally distributed.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/densityPlot-1.png" alt="Density plots of environmental covariates against breeding wader count data" width="672" />
<p class="caption">(\#fig:densityPlot)Density plots of environmental covariates against breeding wader count data</p>
</div>

<!-- Environmental Covariate Response
child doc is loaded in-line -->

## Environmental covariate response

GAMs for breeding wader abundance response across the five different species were generated from 2002–10 and 2011-19. They included 10 environmental predictor variables (covariates), and the model parameters for all species across the two response periods can be seen in Table \@ref(tab:tableGamParamsAbundance). A third model was generated by taking the abundance response from the first two models to generate the ratio of population change between the two response periods.






### Environmental covariate GAM model parameters

Table \@ref(tab:tableGamParamsAbundance) shows the GAM model parameters for the model fits for the two periods where abundance response (density) was modelled, and the associated plots showing breeding wader density against each environmental covariate are shown in Figure \@ref(fig:responsePlots). The statistically significant correlations between breeding wader density and environmental covariate are summarised for each species in heatmaps; Figure \@ref(fig:heatMap200210) for 2002-10 and Figure \@ref(fig:heatMap201119) for 2011-2019. 

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/heatMap200210-1.png" alt="Summary of associations between breeding wader density and environmental covariate, between 2002 and 2010 inclusive" width="672" />
<p class="caption">(\#fig:heatMap200210)Summary of associations between breeding wader density and environmental covariate, between 2002 and 2010 inclusive</p>
</div>
For the 2002-10 survey period in Figure \@ref(fig:heatMap200210), it can be seen that pH is only statistically significant for one species (Snipe), whilst topsoil organic carbon and grassland are oppositely correlated. Distance to sea is perhaps the most interesting covariate in that Lapwing show greater density at the coast whilst Curlew, Oystercatcher and Snipe show greater densities inland. 

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/heatMap201119-1.png" alt="Summary of associations between breeding wader density and environmental covariate, between 2011 and 2019 inclusive" width="672" />
<p class="caption">(\#fig:heatMap201119)Summary of associations between breeding wader density and environmental covariate, between 2011 and 2019 inclusive</p>
</div>

In Figure \@ref(fig:heatMap201119) we can see that there are fewer associations that are not statistically significant. For Curlew it is seen that all covariate associations are now statistically significant (versus 2002-2010 where pH and Heathland cover were not significant). Oystercatcher also have all covariates with statistically significant associations, but for the later survey period the distance to association is now negative with increase distance. Lapwing only have one covariate, pH, that is not statistically significant. For Redshank the main change in the later survey period is that Heathland percentage cover is now statistically significant, and has a positive association. Snipe now have a positive association with available water capacity and a negative association with percentage bog cover.

### Environmental covariate GAM model plots 

Figures \@ref(fig:responsePlots)show the response of wader density to each environmental covariate, for the survey periods 2002-10 and 2011-19.

## Population change model against environmental covariates

By using the response of the 2002-2010 wader densities as the offset for the 2011-19 densities, a third series of GAMs were fitted to show the ratio of population change in response to environmental covariates. This is shown in Figure \@ref(fig:heatMapPopChg).

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/heatMapPopChg-1.png" alt="Summary of population change ratio associations between breeding wader density and environmental covariate, between 2002 and 2019 inclusive" width="672" />
<p class="caption">(\#fig:heatMapPopChg)Summary of population change ratio associations between breeding wader density and environmental covariate, between 2002 and 2019 inclusive</p>
</div>

Figure \@ref(fig:heatMapPopChg) suggests that the environmental covariates with that have had the most positive associations with breeding wader density are heathland percentage cover and available water capacity, whilst the percentage of bare peatland has had no statistical significance, followed by the percentage grassland cover that has only one negative association with the population change ratio of Redshank.

The model parameters and associated plots for population change ratio modelling are shown in Figures \@ref(popChgPlots) and Table \@ref(tab:tableGamParamsPopChg) respectively.


<!-- Information Theory Response
child doc is loaded in-line -->

## Information Theory (IT) covariates 

GAMs for breeding wader abundance response across the five different species were generated from 2002–10 and 2011-19. They included 5 IT predictor variables (covariates), and the model parameters for all species across the two response periods can be seen in Table \@ref(tab:tableGamParamsIT). A third model was generated by taking the abundance response from the first two models to generate the ratio of population change between the two response periods.

### Histograms of Information theory covariates

Histograms of IT covariates using the EUNIS landscape categorisation, across all of Shetland are shown in figure \@ref(fig:itHisto). The *marginal entropy* for the Shetland landscape is approximately normally distributed, indicating that habitat within the Shetland landscape is spatially diverse but that very low and highly diverse habitat within Shetland are relatively rare. The mode of the *conditional entropy* is relatively low with a distribution that shows significant positive skew; this suggests that the Shetland landscape has relatively low geometric intricacy. This arises when cells of one category within a landscape raster are predominantly adjacent to cells of the same category. The overall spatio-thematic complexity is measured by *joint entropy*. This can be thought of as quantifying the uncertainty in determining the habitat type of a focus cell and an adjacent cell. For Shetland, joint entropy appears to be approximately normally distributed. This indicates that habitat with very high or low spatio-thematic complexity is relatively rare on Shetland. Due to the spatial autocorrelation, the value of *mutual information* tends to grow with a diversity of the landscape (marginal entropy). To adjust this tendency, it is possible to calculate *relative mutual information* by dividing the mutual information by the marginal entropy. Relative mutual information always has a range between 0 and 1, and quantifies the degree of aggregation of spatial habitat. It can be seen that for Shetland, relative mutual information is distributed with significant negative skew. This implies that habitat types across Shetland are predominantly aggregated - small relatively information values indicate significant fragmentation in landscape habitat patterns.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itHisto-1.png" alt="Histograms of Information Theory covariates across all Shetland OS 1km squares" width="672" />
<p class="caption">(\#fig:itHisto)Histograms of Information Theory covariates across all Shetland OS 1km squares</p>
</div>

### Histograms of Information Theory covariates for surveyed squares only

1km squares surveyed as part of the Shetland BBS were used to generate IT covariates histograms using the EUNIS landscape categorisation, as shown in Figure \@ref(fig:itSBBSHisto). Here we can see that the *conditional entropy* and the *marginal entropy* across all surveyed squares had a mode that was significantly higher than the Shetland wide values shown in Figure \@ref(fig:itHisto). There is also significantly less negative negative skew in the *relative mutual information* of the surveyed squares. 

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itSBBSHisto-1.png" alt="Histograms of Information Theory covariates across SBBS surveyed sqaures only " width="672" />
<p class="caption">(\#fig:itSBBSHisto)Histograms of Information Theory covariates across SBBS surveyed sqaures only </p>
</div>

### Information Theory covariates abundance response model



Here we generate GAMs using IT metrics as covariates against breeding wader abundance data. Figures \@ref(fig:itHeatMap200210) and \@ref(fig:itHeatMap201119) summarise the associations between the abundance response and IT covariates used in the univariate GAMs, for the periods 2002-10 and 2011-19 respectively.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itHeatMap200210-1.png" alt="Summary of associations between breeding wader density and IT covariates, between 2002 and 2010 inclusive" width="672" />
<p class="caption">(\#fig:itHeatMap200210)Summary of associations between breeding wader density and IT covariates, between 2002 and 2010 inclusive</p>
</div>

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itHeatMap201119-1.png" alt="Summary of associations between breeding wader density and IT covariates, between 2011 and 2019 inclusive" width="672" />
<p class="caption">(\#fig:itHeatMap201119)Summary of associations between breeding wader density and IT covariates, between 2011 and 2019 inclusive</p>
</div>
Table \@ref(tab:tableGamParamsITAbundance) shows the GAM parameters generated by fitting the model to the data.

<table class="table" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Species </th>
   <th style="text-align:left;"> Response </th>
   <th style="text-align:left;"> Covariate </th>
   <th style="text-align:center;"> Estimate </th>
   <th style="text-align:center;"> se </th>
   <th style="text-align:center;"> z </th>
   <th style="text-align:center;"> p-value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;font-weight: bold;vertical-align: top !important;" rowspan="10"> CU </td>
   <td style="text-align:left;vertical-align: top !important;" rowspan="5"> 2002-2010 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.0146677 </td>
   <td style="text-align:center;"> 0.0536137 </td>
   <td style="text-align:center;"> 0.2735805 </td>
   <td style="text-align:center;"> 0.7844071 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> -0.2421870 </td>
   <td style="text-align:center;"> 0.1329494 </td>
   <td style="text-align:center;"> -1.8216484 </td>
   <td style="text-align:center;"> 0.0685084 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> -0.0136522 </td>
   <td style="text-align:center;"> 0.0394730 </td>
   <td style="text-align:center;"> -0.3458625 </td>
   <td style="text-align:center;"> 0.7294461 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> 0.1084873 </td>
   <td style="text-align:center;"> 0.0763370 </td>
   <td style="text-align:center;"> 1.4211618 </td>
   <td style="text-align:center;"> 0.1552697 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> 0.8447465 </td>
   <td style="text-align:center;"> 0.3850731 </td>
   <td style="text-align:center;"> 2.1937304 </td>
   <td style="text-align:center;"> 0.0282548 </td>
  </tr>
  <tr>
   
   <td style="text-align:left;vertical-align: top !important;" rowspan="5"> 2011-2019 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.1236513 </td>
   <td style="text-align:center;"> 0.0511373 </td>
   <td style="text-align:center;"> 2.4180282 </td>
   <td style="text-align:center;"> 0.0156049 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> 0.2407611 </td>
   <td style="text-align:center;"> 0.1185323 </td>
   <td style="text-align:center;"> 2.0311847 </td>
   <td style="text-align:center;"> 0.0422363 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> 0.0903451 </td>
   <td style="text-align:center;"> 0.0374825 </td>
   <td style="text-align:center;"> 2.4103258 </td>
   <td style="text-align:center;"> 0.0159383 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> 0.1565311 </td>
   <td style="text-align:center;"> 0.0711833 </td>
   <td style="text-align:center;"> 2.1989866 </td>
   <td style="text-align:center;"> 0.0278789 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> 0.2041695 </td>
   <td style="text-align:center;"> 0.3598637 </td>
   <td style="text-align:center;"> 0.5673522 </td>
   <td style="text-align:center;"> 0.5704749 </td>
  </tr>
  <tr>
   <td style="text-align:center;font-weight: bold;vertical-align: top !important;" rowspan="10"> L </td>
   <td style="text-align:left;vertical-align: top !important;" rowspan="5"> 2002-2010 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.1844326 </td>
   <td style="text-align:center;"> 0.0642893 </td>
   <td style="text-align:center;"> 2.8687910 </td>
   <td style="text-align:center;"> 0.0041204 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> -0.2714342 </td>
   <td style="text-align:center;"> 0.1466646 </td>
   <td style="text-align:center;"> -1.8507130 </td>
   <td style="text-align:center;"> 0.0642109 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> 0.0694717 </td>
   <td style="text-align:center;"> 0.0458718 </td>
   <td style="text-align:center;"> 1.5144770 </td>
   <td style="text-align:center;"> 0.1299049 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> 0.4851591 </td>
   <td style="text-align:center;"> 0.0940679 </td>
   <td style="text-align:center;"> 5.1575411 </td>
   <td style="text-align:center;"> 0.0000003 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> 2.1152313 </td>
   <td style="text-align:center;"> 0.4586081 </td>
   <td style="text-align:center;"> 4.6122854 </td>
   <td style="text-align:center;"> 0.0000040 </td>
  </tr>
  <tr>
   
   <td style="text-align:left;vertical-align: top !important;" rowspan="5"> 2011-2019 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.3855698 </td>
   <td style="text-align:center;"> 0.0646452 </td>
   <td style="text-align:center;"> 5.9643991 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> 0.6048805 </td>
   <td style="text-align:center;"> 0.1352258 </td>
   <td style="text-align:center;"> 4.4731131 </td>
   <td style="text-align:center;"> 0.0000077 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> 0.2633951 </td>
   <td style="text-align:center;"> 0.0457607 </td>
   <td style="text-align:center;"> 5.7559285 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> 0.5368301 </td>
   <td style="text-align:center;"> 0.0929781 </td>
   <td style="text-align:center;"> 5.7737260 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> -0.4699113 </td>
   <td style="text-align:center;"> 0.4405284 </td>
   <td style="text-align:center;"> -1.0666993 </td>
   <td style="text-align:center;"> 0.2861077 </td>
  </tr>
  <tr>
   <td style="text-align:center;font-weight: bold;vertical-align: top !important;" rowspan="10"> OC </td>
   <td style="text-align:left;vertical-align: top !important;" rowspan="5"> 2002-2010 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.0363394 </td>
   <td style="text-align:center;"> 0.0497067 </td>
   <td style="text-align:center;"> 0.7310776 </td>
   <td style="text-align:center;"> 0.4647317 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> -0.3181738 </td>
   <td style="text-align:center;"> 0.1232162 </td>
   <td style="text-align:center;"> -2.5822400 </td>
   <td style="text-align:center;"> 0.0098161 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> -0.0086856 </td>
   <td style="text-align:center;"> 0.0365371 </td>
   <td style="text-align:center;"> -0.2377214 </td>
   <td style="text-align:center;"> 0.8120972 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> 0.1749038 </td>
   <td style="text-align:center;"> 0.0706402 </td>
   <td style="text-align:center;"> 2.4759798 </td>
   <td style="text-align:center;"> 0.0132871 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> 1.8040401 </td>
   <td style="text-align:center;"> 0.3825695 </td>
   <td style="text-align:center;"> 4.7155885 </td>
   <td style="text-align:center;"> 0.0000024 </td>
  </tr>
  <tr>
   
   <td style="text-align:left;vertical-align: top !important;" rowspan="5"> 2011-2019 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.1642554 </td>
   <td style="text-align:center;"> 0.0447858 </td>
   <td style="text-align:center;"> 3.6675732 </td>
   <td style="text-align:center;"> 0.0002449 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> 0.1749297 </td>
   <td style="text-align:center;"> 0.1017500 </td>
   <td style="text-align:center;"> 1.7192100 </td>
   <td style="text-align:center;"> 0.0855761 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> 0.1051199 </td>
   <td style="text-align:center;"> 0.0324920 </td>
   <td style="text-align:center;"> 3.2352543 </td>
   <td style="text-align:center;"> 0.0012153 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> 0.2598414 </td>
   <td style="text-align:center;"> 0.0630789 </td>
   <td style="text-align:center;"> 4.1193060 </td>
   <td style="text-align:center;"> 0.0000380 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> 0.2962538 </td>
   <td style="text-align:center;"> 0.3213465 </td>
   <td style="text-align:center;"> 0.9219141 </td>
   <td style="text-align:center;"> 0.3565734 </td>
  </tr>
  <tr>
   <td style="text-align:center;font-weight: bold;vertical-align: top !important;" rowspan="10"> RK </td>
   <td style="text-align:left;vertical-align: top !important;" rowspan="5"> 2002-2010 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.3370049 </td>
   <td style="text-align:center;"> 0.0787904 </td>
   <td style="text-align:center;"> 4.2772304 </td>
   <td style="text-align:center;"> 0.0000189 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> -0.0155368 </td>
   <td style="text-align:center;"> 0.1723386 </td>
   <td style="text-align:center;"> -0.0901526 </td>
   <td style="text-align:center;"> 0.9281660 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> 0.1727040 </td>
   <td style="text-align:center;"> 0.0555448 </td>
   <td style="text-align:center;"> 3.1092762 </td>
   <td style="text-align:center;"> 0.0018755 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> 0.7005377 </td>
   <td style="text-align:center;"> 0.1156684 </td>
   <td style="text-align:center;"> 6.0564291 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> 1.7594285 </td>
   <td style="text-align:center;"> 0.5220999 </td>
   <td style="text-align:center;"> 3.3699075 </td>
   <td style="text-align:center;"> 0.0007519 </td>
  </tr>
  <tr>
   
   <td style="text-align:left;vertical-align: top !important;" rowspan="5"> 2011-2019 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.3837114 </td>
   <td style="text-align:center;"> 0.0748693 </td>
   <td style="text-align:center;"> 5.1250799 </td>
   <td style="text-align:center;"> 0.0000003 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> 0.4635703 </td>
   <td style="text-align:center;"> 0.1550127 </td>
   <td style="text-align:center;"> 2.9905322 </td>
   <td style="text-align:center;"> 0.0027849 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> 0.2460470 </td>
   <td style="text-align:center;"> 0.0525811 </td>
   <td style="text-align:center;"> 4.6793848 </td>
   <td style="text-align:center;"> 0.0000029 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> 0.5947576 </td>
   <td style="text-align:center;"> 0.1088624 </td>
   <td style="text-align:center;"> 5.4633912 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> -0.1561187 </td>
   <td style="text-align:center;"> 0.5017587 </td>
   <td style="text-align:center;"> -0.3111429 </td>
   <td style="text-align:center;"> 0.7556920 </td>
  </tr>
  <tr>
   <td style="text-align:center;font-weight: bold;vertical-align: top !important;" rowspan="10"> SN </td>
   <td style="text-align:left;vertical-align: top !important;" rowspan="5"> 2002-2010 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> -0.4583426 </td>
   <td style="text-align:center;"> 0.0420378 </td>
   <td style="text-align:center;"> -10.9031085 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> -1.3051528 </td>
   <td style="text-align:center;"> 0.1232023 </td>
   <td style="text-align:center;"> -10.5935739 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> -0.3616883 </td>
   <td style="text-align:center;"> 0.0321375 </td>
   <td style="text-align:center;"> -11.2544093 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> -0.5476632 </td>
   <td style="text-align:center;"> 0.0583563 </td>
   <td style="text-align:center;"> -9.3848097 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> 1.2271535 </td>
   <td style="text-align:center;"> 0.3580540 </td>
   <td style="text-align:center;"> 3.4272858 </td>
   <td style="text-align:center;"> 0.0006096 </td>
  </tr>
  <tr>
   
   <td style="text-align:left;vertical-align: top !important;" rowspan="5"> 2011-2019 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> -0.3989068 </td>
   <td style="text-align:center;"> 0.0397469 </td>
   <td style="text-align:center;"> -10.0361788 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> -0.9562571 </td>
   <td style="text-align:center;"> 0.1131197 </td>
   <td style="text-align:center;"> -8.4534968 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> -0.3025560 </td>
   <td style="text-align:center;"> 0.0303087 </td>
   <td style="text-align:center;"> -9.9824711 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> -0.5133646 </td>
   <td style="text-align:center;"> 0.0552080 </td>
   <td style="text-align:center;"> -9.2987274 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> 1.0307061 </td>
   <td style="text-align:center;"> 0.3369643 </td>
   <td style="text-align:center;"> 3.0587992 </td>
   <td style="text-align:center;"> 0.0022223 </td>
  </tr>
</tbody>
</table>

Plots for abundance response against IT covariates are shown in Figure \@ref(fig:itResponsePlots).


```
## [[1]]
```

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itResponsePlots-1.png" alt="Plots show abundance response to information theory covariates for a GAM" width="672" />
<p class="caption">(\#fig:itResponsePlots1)Plots show abundance response to information theory covariates for a GAM</p>
</div><div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itResponsePlots-2.png" alt="Plots show abundance response to information theory covariates for a GAM" width="672" />
<p class="caption">(\#fig:itResponsePlots2)Plots show abundance response to information theory covariates for a GAM</p>
</div><div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itResponsePlots-3.png" alt="Plots show abundance response to information theory covariates for a GAM" width="672" />
<p class="caption">(\#fig:itResponsePlots3)Plots show abundance response to information theory covariates for a GAM</p>
</div>

```
## 
## [[2]]
```

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itResponsePlots-4.png" alt="Plots show abundance response to information theory covariates for a GAM" width="672" />
<p class="caption">(\#fig:itResponsePlots4)Plots show abundance response to information theory covariates for a GAM</p>
</div><div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itResponsePlots-5.png" alt="Plots show abundance response to information theory covariates for a GAM" width="672" />
<p class="caption">(\#fig:itResponsePlots5)Plots show abundance response to information theory covariates for a GAM</p>
</div><div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itResponsePlots-6.png" alt="Plots show abundance response to information theory covariates for a GAM" width="672" />
<p class="caption">(\#fig:itResponsePlots6)Plots show abundance response to information theory covariates for a GAM</p>
</div>

### Population change model against IT covarirates

By using the response of the 2002-2010 wader densities as the offset for the 2011-19 densities, a third series of GAMs were fitted to show the ratio of population change in response to environmental covariates. This is summarised in Figure \@ref(fig:itHeatMapPopChg). It can be seen that there are no statistically significant results for Redshank or Snipe, or for marginal entropy as a covariate.

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itHeatMapPopChg-1.png" alt="Summary of associations between breeding wader density and IT covariates, between 2011 and 2019 inclusive" width="672" />
<p class="caption">(\#fig:itHeatMapPopChg)Summary of associations between breeding wader density and IT covariates, between 2011 and 2019 inclusive</p>
</div>
Table \@ref(tab:tableGamParamsITPopChg) shows the GAM parameters generated by fitting the population change model to the data.

<table class="table" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Species </th>
   <th style="text-align:left;"> Period </th>
   <th style="text-align:left;"> Covariate </th>
   <th style="text-align:center;"> Estimate </th>
   <th style="text-align:center;"> se </th>
   <th style="text-align:center;"> z </th>
   <th style="text-align:center;"> p-value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;font-weight: bold;vertical-align: top !important;" rowspan="5"> CU </td>
   <td style="text-align:left;vertical-align: top !important;" rowspan="25"> 2002-2019 </td>
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.1118467 </td>
   <td style="text-align:center;"> 0.0675516 </td>
   <td style="text-align:center;"> 1.6557234 </td>
   <td style="text-align:center;"> 0.0977779 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> 0.5590287 </td>
   <td style="text-align:center;"> 0.1909809 </td>
   <td style="text-align:center;"> 2.9271438 </td>
   <td style="text-align:center;"> 0.0034209 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> 0.1073756 </td>
   <td style="text-align:center;"> 0.0520611 </td>
   <td style="text-align:center;"> 2.0624910 </td>
   <td style="text-align:center;"> 0.0391610 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> 0.0753227 </td>
   <td style="text-align:center;"> 0.0903742 </td>
   <td style="text-align:center;"> 0.8334540 </td>
   <td style="text-align:center;"> 0.4045887 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> 0.1498643 </td>
   <td style="text-align:center;"> 0.5677852 </td>
   <td style="text-align:center;"> 0.2639455 </td>
   <td style="text-align:center;"> 0.7918219 </td>
  </tr>
  <tr>
   <td style="text-align:center;font-weight: bold;vertical-align: top !important;" rowspan="5"> L </td>
   
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.1462746 </td>
   <td style="text-align:center;"> 0.0912263 </td>
   <td style="text-align:center;"> 1.6034268 </td>
   <td style="text-align:center;"> 0.1088405 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> 0.8672945 </td>
   <td style="text-align:center;"> 0.2439751 </td>
   <td style="text-align:center;"> 3.5548492 </td>
   <td style="text-align:center;"> 0.0003782 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> 0.1563824 </td>
   <td style="text-align:center;"> 0.0696562 </td>
   <td style="text-align:center;"> 2.2450618 </td>
   <td style="text-align:center;"> 0.0247642 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> 0.0398334 </td>
   <td style="text-align:center;"> 0.1222759 </td>
   <td style="text-align:center;"> 0.3257667 </td>
   <td style="text-align:center;"> 0.7446009 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> -3.0830321 </td>
   <td style="text-align:center;"> 0.8224450 </td>
   <td style="text-align:center;"> -3.7486180 </td>
   <td style="text-align:center;"> 0.0001778 </td>
  </tr>
  <tr>
   <td style="text-align:center;font-weight: bold;vertical-align: top !important;" rowspan="5"> OC </td>
   
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> 0.0984170 </td>
   <td style="text-align:center;"> 0.0671045 </td>
   <td style="text-align:center;"> 1.4666221 </td>
   <td style="text-align:center;"> 0.1424789 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> 0.7690937 </td>
   <td style="text-align:center;"> 0.1853413 </td>
   <td style="text-align:center;"> 4.1496065 </td>
   <td style="text-align:center;"> 0.0000333 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> 0.1217885 </td>
   <td style="text-align:center;"> 0.0524607 </td>
   <td style="text-align:center;"> 2.3215185 </td>
   <td style="text-align:center;"> 0.0202589 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> -0.0049392 </td>
   <td style="text-align:center;"> 0.0855585 </td>
   <td style="text-align:center;"> -0.0577294 </td>
   <td style="text-align:center;"> 0.9539642 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> -2.1515689 </td>
   <td style="text-align:center;"> 0.5307584 </td>
   <td style="text-align:center;"> -4.0537632 </td>
   <td style="text-align:center;"> 0.0000504 </td>
  </tr>
  <tr>
   <td style="text-align:center;font-weight: bold;vertical-align: top !important;" rowspan="5"> RK </td>
   
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> -0.0295331 </td>
   <td style="text-align:center;"> 0.1291955 </td>
   <td style="text-align:center;"> -0.2285920 </td>
   <td style="text-align:center;"> 0.8191861 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> 0.2382062 </td>
   <td style="text-align:center;"> 0.2970304 </td>
   <td style="text-align:center;"> 0.8019590 </td>
   <td style="text-align:center;"> 0.4225767 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> 0.0080518 </td>
   <td style="text-align:center;"> 0.0953466 </td>
   <td style="text-align:center;"> 0.0844475 </td>
   <td style="text-align:center;"> 0.9327007 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> -0.1371250 </td>
   <td style="text-align:center;"> 0.1766698 </td>
   <td style="text-align:center;"> -0.7761657 </td>
   <td style="text-align:center;"> 0.4376512 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> -1.1267983 </td>
   <td style="text-align:center;"> 0.9416540 </td>
   <td style="text-align:center;"> -1.1966161 </td>
   <td style="text-align:center;"> 0.2314562 </td>
  </tr>
  <tr>
   <td style="text-align:center;font-weight: bold;vertical-align: top !important;" rowspan="5"> SN </td>
   
   <td style="text-align:left;"> Marginal entropy </td>
   <td style="text-align:center;"> -0.0266655 </td>
   <td style="text-align:center;"> 0.0594140 </td>
   <td style="text-align:center;"> -0.4488075 </td>
   <td style="text-align:center;"> 0.6535705 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Conditional entropy </td>
   <td style="text-align:center;"> 0.1340918 </td>
   <td style="text-align:center;"> 0.1667186 </td>
   <td style="text-align:center;"> 0.8042999 </td>
   <td style="text-align:center;"> 0.4212238 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Joint entropy </td>
   <td style="text-align:center;"> -0.0056983 </td>
   <td style="text-align:center;"> 0.0453185 </td>
   <td style="text-align:center;"> -0.1257393 </td>
   <td style="text-align:center;"> 0.8999383 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Mutual information </td>
   <td style="text-align:center;"> -0.0813365 </td>
   <td style="text-align:center;"> 0.0813280 </td>
   <td style="text-align:center;"> -1.0001037 </td>
   <td style="text-align:center;"> 0.3172603 </td>
  </tr>
  <tr>
   
   
   <td style="text-align:left;"> Relative mutual informaton </td>
   <td style="text-align:center;"> 0.2789059 </td>
   <td style="text-align:center;"> 0.4576770 </td>
   <td style="text-align:center;"> 0.6093947 </td>
   <td style="text-align:center;"> 0.5422629 </td>
  </tr>
</tbody>
</table>

Plots for population change response against IT covariates are shown in Figure \@ref(fig:itPopChgPlots).


```
## [[1]]
```

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itPopChgPlots-1.png" alt="Plots show population change to information theory covariates for a GAM, across all wader species" width="672" />
<p class="caption">(\#fig:itPopChgPlots1)Plots show population change to information theory covariates for a GAM, across all wader species</p>
</div><div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itPopChgPlots-2.png" alt="Plots show population change to information theory covariates for a GAM, across all wader species" width="672" />
<p class="caption">(\#fig:itPopChgPlots2)Plots show population change to information theory covariates for a GAM, across all wader species</p>
</div><div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/itPopChgPlots-3.png" alt="Plots show population change to information theory covariates for a GAM, across all wader species" width="672" />
<p class="caption">(\#fig:itPopChgPlots3)Plots show population change to information theory covariates for a GAM, across all wader species</p>
</div>

<!-- Abundance over time and spatial distribution
child doc is loaded in-line -->

## Wader abundance trends

A random forest regression model was used to fit abundance response, given a set of 10 environmental covariates. The number of trees in the model hyper-parameters was set to 1000, and the number of predictors sampled at each split (`mtry`) together the minimum number of data points that cause a node to split furthter (`min_n`) were tuned using a search grid containing ten points in the hyper plane.



<!-- 
Code to generate Random Forest regression model to estimate 
population abundance for each wader species.

Method is as follows:

1 - Load data and generate suitable format
2 - Split into training and test data sets
3 - Preprocess data
-->





<!-- Create a model specification for a random forest where we will tune mtry (the number of predictors to sample at each split) and min_n (the number of observations needed to keep splitting nodes). -->



<!-- Now we can tune the hyperparameters for a random forest model. First, let’s create a set of cross-validation resamples to use for tuning. Then run a model for each sample dataset. -->



### Tuning model  hyper parameters

The tuning grid over 10 different folds gave the results for the different hyper parameter permutations as shown in Figure \@ref(fig:showTuneResults) - each figure show the results for a particular species. Each parameter is plotted against the resulting root mean squared error (rmse). 


```
## [[1]]
```

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/showTuneResults-1.png" alt="Root mean squared evaluation of hyper parameters across all species" width="672" />
<p class="caption">(\#fig:showTuneResults1)Root mean squared evaluation of hyper parameters across all species</p>
</div>

```
## 
## [[2]]
```

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/showTuneResults-2.png" alt="Root mean squared evaluation of hyper parameters across all species" width="672" />
<p class="caption">(\#fig:showTuneResults2)Root mean squared evaluation of hyper parameters across all species</p>
</div>

```
## 
## [[3]]
```

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/showTuneResults-3.png" alt="Root mean squared evaluation of hyper parameters across all species" width="672" />
<p class="caption">(\#fig:showTuneResults3)Root mean squared evaluation of hyper parameters across all species</p>
</div>

```
## 
## [[4]]
```

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/showTuneResults-4.png" alt="Root mean squared evaluation of hyper parameters across all species" width="672" />
<p class="caption">(\#fig:showTuneResults4)Root mean squared evaluation of hyper parameters across all species</p>
</div>

```
## 
## [[5]]
```

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/showTuneResults-5.png" alt="Root mean squared evaluation of hyper parameters across all species" width="672" />
<p class="caption">(\#fig:showTuneResults5)Root mean squared evaluation of hyper parameters across all species</p>
</div>

### Further model hyper parameter tuning

The model fit was refined further by searching over a revised hypergrid range for each species. The range used was that which gave the lowest rmse as given in Figure \@ref(fig:showTuneResults). The results of the revised tuning grid can be seen in Figure \@ref(fig:plotRetuneResults).

<!-- Now refine the tuning per species -->





```
## [[1]]
```

<img src="03-results_files/figure-html/plotRetuneResults-1.png" width="672" />

```
## 
## [[2]]
```

<img src="03-results_files/figure-html/plotRetuneResults-2.png" width="672" />

```
## 
## [[3]]
```

<img src="03-results_files/figure-html/plotRetuneResults-3.png" width="672" />

```
## 
## [[4]]
```

<img src="03-results_files/figure-html/plotRetuneResults-4.png" width="672" />

```
## 
## [[5]]
```

<img src="03-results_files/figure-html/plotRetuneResults-5.png" width="672" />

From the plot above we can see which hyper parameters give the best fit, when using root mean squared error as an evaluation metric. It can be seen that the model fit for Snipe has the largest RMSE and Redshank, the lowest. For each species the minimum rmse given by the best model fit, together with the associated hyper parameters (`trees`= 1000 for all models) is shown in Table \@ref(tab:bestByRMSE).

<table>
 <thead>
  <tr>
   <th style="text-align:left;"> Species </th>
   <th style="text-align:right;"> mtry </th>
   <th style="text-align:right;"> min_n </th>
   <th style="text-align:right;"> rmse </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> CU </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 1.448835 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 1.672523 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> OC </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:right;"> 1.845994 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> RK </td>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 1.429948 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> SN </td>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 2.718174 </td>
  </tr>
</tbody>
</table>

### Variable importance in model fit

Having selected the best model fit the variable importance for each species was assessed. The `r` `vip` package can be used to explore the relative importance of different covariates in the model fit. The results are shown in Figure \@ref(fig:variableImportance).


```
## [[1]]
```

<div class="figure">
<img src="03-results_files/figure-html/variableImportance-1.png" alt="Variable importance in model fit" width="672" />
<p class="caption">(\#fig:variableImportance1)Variable importance in model fit</p>
</div>

```
## 
## [[2]]
```

<div class="figure">
<img src="03-results_files/figure-html/variableImportance-2.png" alt="Variable importance in model fit" width="672" />
<p class="caption">(\#fig:variableImportance2)Variable importance in model fit</p>
</div>

```
## 
## [[3]]
```

<div class="figure">
<img src="03-results_files/figure-html/variableImportance-3.png" alt="Variable importance in model fit" width="672" />
<p class="caption">(\#fig:variableImportance3)Variable importance in model fit</p>
</div>

```
## 
## [[4]]
```

<div class="figure">
<img src="03-results_files/figure-html/variableImportance-4.png" alt="Variable importance in model fit" width="672" />
<p class="caption">(\#fig:variableImportance4)Variable importance in model fit</p>
</div>

```
## 
## [[5]]
```

<div class="figure">
<img src="03-results_files/figure-html/variableImportance-5.png" alt="Variable importance in model fit" width="672" />
<p class="caption">(\#fig:variableImportance5)Variable importance in model fit</p>
</div>

It can be seen that pH, X (longitude) and grassland percentage coverage for a given OS 1km square are the most important covariates for predicting abundance in Curlew. For Lapwing, pH, heathland percentage coverage and topsoil organic carbon content are the most important variables. Whilst for Oystercatcher, grassland and heathland percentage cover are almost equivalent in their importance followed by longitude. For Redshank and Snipe, available water capacity and heathland are the most important covariates in predicting abundance.




### Generate population estimate over time

The random forest regression model was used to predict species abundance over *all* (n=3992) Shetland BBS 1km squares. The model gave a mean estimate together with lower and upper confidence intervals (5% and 95% percentiles respectively), across every year the survey was run (2002 to 2019). The results are shown in Table \@ref(tab:abundanceResults) and plotted Figure \@ref(fig:plotAbunResults)






<div class="figure" style="text-align: centre">
<img src="03-results_files/figure-html/plotAbunResults-1.png" alt="Shetland breeding wader abundance by year" width="672" />
<p class="caption">(\#fig:plotAbunResults)Shetland breeding wader abundance by year</p>
</div>
Across the years 2002 to 2019 the abundance of breeding waders across all species appear to have decreased, with the exception of Snipe. The most significant decline was breeding Lapwing abundance. Note that the confidence intervals for Snipe are highly variable in certain years. Table \@ref(tab:popChgTable) shows the change in breeding wader abundance by species between 2002 and 2019.

<table>
 <thead>
  <tr>
   <th style="text-align:left;"> Species </th>
   <th style="text-align:right;"> 2002 </th>
   <th style="text-align:right;"> 2019 </th>
   <th style="text-align:right;"> % Change </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> CU </td>
   <td style="text-align:right;"> 4597 </td>
   <td style="text-align:right;"> 4088 </td>
   <td style="text-align:right;"> -11.1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L </td>
   <td style="text-align:right;"> 3474 </td>
   <td style="text-align:right;"> 2638 </td>
   <td style="text-align:right;"> -24.1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> OC </td>
   <td style="text-align:right;"> 5269 </td>
   <td style="text-align:right;"> 4760 </td>
   <td style="text-align:right;"> -9.7 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> RK </td>
   <td style="text-align:right;"> 2390 </td>
   <td style="text-align:right;"> 2248 </td>
   <td style="text-align:right;"> -5.9 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> SN </td>
   <td style="text-align:right;"> 6043 </td>
   <td style="text-align:right;"> 7391 </td>
   <td style="text-align:right;"> 22.3 </td>
  </tr>
</tbody>
</table>

### Lapwing abundance association with grassland holdings

Data from 2002 to 2017 for grassland holdings in hectares categorised as: tillage, grassland less than five years old (reseeded grassland), grassland five years or greater and private grazing were tested for normality, and found to be log-normally distributed. A linear regression was plotted for Lapwing abundance versus each grassland categorisation (in Hectares) as shown in Figure \@ref(fig:lapwingGrasslandPlot).




<div class="figure">
<img src="03-results_files/figure-html/lapwingGrasslandPlot-1.png" alt="Association between the size of grassland categories on Shetland and Lapwing population abundance" width="672" />
<p class="caption">(\#fig:lapwingGrasslandPlot)Association between the size of grassland categories on Shetland and Lapwing population abundance</p>
</div>
Figure \@ref(fig:lapwingGrasslandPlot) show's that Lapwing population size is clearly positively associated with the size of grassland that is less than five years old (that grassland which has been reseeded) and tillage (land prepared for spring crops). Futhermore, Figure \@ref(fig:lapwingGrasslandPlot) shows that Lapwing population abundance is negatively associated with grassland that is not reseeded (Grass >= 5y).

The `r` package `gamlss`  was used to fit a log-normal model for Lapwing population abundance with grassland less than 5 years old as a covariate. The grassland < 5 years old was statistically significant covariate (p<0.0001), and the residuals of the model were approximately normally distributed as shown in Figure \@ref(fig:fitLapwingModel).


```
## GAMLSS-RS iteration 1: Global Deviance = 192.9757 
## GAMLSS-RS iteration 2: Global Deviance = 192.9757
```

<img src="03-results_files/figure-html/fitLapwingModel-1.png" width="672" />

```
## ******************************************************************
## 	      Summary of the Quantile Residuals
##                            mean   =  4.67573e-15 
##                        variance   =  1.066667 
##                coef. of skewness  =  -0.3010934 
##                coef. of kurtosis  =  2.375124 
## Filliben correlation coefficient  =  0.9630635 
## ******************************************************************
```

### Spatial abundance distriution

The abundance prediction created above is spatial and so can be plotted to show how species abundance is spatially distributed across Shetland. Figure \@ref(fig:spatialDistributions) shows abundance distribution for each species in 2019. 

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/spatialDistributions-1.png" alt="Spatial abundance distribution of breeding waders for 2002 and 2019" width="672" />
<p class="caption">(\#fig:spatialDistributions)Spatial abundance distribution of breeding waders for 2002 and 2019</p>
</div>

### Net abundance change by species between 2002 and 2019

Given the spatial abundance distribution for 2002 and 2019, it is possible to plot the net change in breeding wader abudnance between the two years. This is shown in Figure \@ref(fig:netChgPlot).

<div class="figure" style="text-align: center">
<img src="03-results_files/figure-html/netChgPlot-1.png" alt="Change in breeding wader density (count/km2)" width="672" />
<p class="caption">(\#fig:netChgPlot)Change in breeding wader density (count/km2)</p>
</div>

It can be seen that the drop in abundance as shown in Table \@ref(tab:popChgTable) is reflected in the net change plots. Significant increases for Snipe, but significant Lapwing density declines in the south mainland, and Oystercatcher across Unst and Fetlar.

<!-- Predict improve grassland and then work
out if strength of connectivity with wader breeder 
territories are significant -->





