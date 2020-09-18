




# Results

<!-- Exploratory Data Analysis
child doc is loaded in-line -->

## Explororatory Data Analysis of Shetland BBS survey data

Where relevant a protocol for exploratory data analysis was followed [@Zuur2010-kp] to ensure that before any problems in the structure of the data are identified prior to undertaking any statistical analysis.

### Survey effort over time

The spatial location of surveyed squares are shown in Figure \@ref(fig:spatSum). It seems that there has been ongoing surveying effort in the south  mainland and on the islands of Unst, Bressay and Noss, but less coverage elsewhere. In particular bog and upland heathland have significantly less survey effort. This finding is also seen in the bootstrap of surveyed habitat versus  overall Shetland habitat (see Section \@ref(bootstrap)).

![(\#fig:spatSum)Locations and sampling effort of Shetland Breeding Bird Survey, for farmland wader species. Number of years a SBBS 1km square was survyered (n), between 2002 and 2019](03-results_files/figure-docx/spatSum-1.png)
### Status of population change at survey sites between 2002 and 2019



Before any detailed statistical modelling was undertaken a simple analysis into how the population changed between 2002-2011 and 2012-2019, in each surveyed 1km square (n=139). This gives an initial view as to potential population trends between the two analysis periods.The 1 km squares included were those surveyed in both periods and where farmland waders colonized, increased, remained stable, declined or went extinct. Figure \@ref(fig:popStatusChg) shows the status changes between the two analysis periods.

![(\#fig:popStatusChg)Population status change per Shetland BBS square - between 2002-10 and 2011-19](03-results_files/figure-docx/popStatusChg-1.png)

Figure \@ref(fig:aggPopChg) below shows an aggregation of certain categories whereby extinct and decreased are grouped, and colonised and increased are grouped. It can be seen that only Lapwing show a net decline over the two analysis periods.

![(\#fig:aggPopChg)Aggregate population status change per Shetland BBS square - between 2002-10 and 2011-19](03-results_files/figure-docx/aggPopChg-1.png)

### Outliers

The *Cleveland dot plot* [@Zuur2010-kp] is a chart in which the row number of an observation is plotted versus the observation variable, thereby providing a more detailed view of individual observations than a boxplot. Points that stick out on the right-hand side, or on the left-hand side, are observed values that are considerably larger, or smaller, than the majority of the observations. Figure \@ref(fig:countDotPlot) appears to show that there are no significant outliers across all species, but that there are many counts equal to zero indicating that the count data might be zero-inflated.

![(\#fig:countDotPlot)Cleveland dot plot of species counts in Shetland BBS data from 2002 to 2019 ](03-results_files/figure-docx/countDotPlot-1.png)

### Testing for normality

A large number of statistical regression techniques assume normality. Visualising the Shetland BBS count data as a histogram can help assess if it is normally distributed. This is shown in the plot in Figure \@ref(fig:normality).

![(\#fig:normality)Histogram of SBBS count data across all years, by species](03-results_files/figure-docx/normality-1.png)

Clearly the count data are not normally distributed. In-order to validate the outcome of the plots in Figure \@ref(fig:normality) a Shapiro-Wilks normality significance test was undertaken and the results are shown in Table \@ref(tab:normSig).

<!--Table: (\#tab:normSig) Results for Shaprio-Wilks test for normality -->


Table: (\#tab:normSig)Shapiro-Wilks normality test for count data of breeding waders

Species            W   p-value
--------  ----------  --------
OC         0.8628058         0
L          0.7546102         0
CU         0.8327195         0
RK         0.6995970         0
SN         0.8000661         0

The p-value for each species in \@ref(tab:normSig) is << 0.05. This suggests that the count data for all species are significantly different from the normal distribution.

### Poisson distribution and zero inflation

The histograms of species counts in Figure \@ref(fig:normality) suggest that count data is a poisson distribution. Also there are a significant number of zeros in the count data, across all species count data. This suggests that the zero-inflation poisson distribution describes the data. Table \@ref(tab:zipTest) below shows the results of a significance test [@Van_den_Broek1995-ml] for data zero inflation that follow a poisson distribution.


Table: (\#tab:zipTest)Zero inflation poisson distribution test for Shetland SBBS count data, across all years and species

Species    Expected zeros   Zeros observed   Chi squared   p-value
--------  ---------------  ---------------  ------------  --------
CU               223.9173              433      384.2445         0
L                323.5230              585      547.5071         0
OC               119.1142              309      446.9641         0
RK               520.3458              694      271.6801         0
SN               134.4406              359      577.9990         0

All results have a significant statistical significance (p<0.05) and therefore the count distribution across species data are assumed to be a zero-inflated poisson process. The statistical modelling methods used on the data must support a poisson distribution and zero inflation where possible.

### Homogeniety of variance

Homogeneity of variance within the data is an important assumption in analysis of variance (ANOVA) and other regression-related models. The series of boxplots in Figure \@ref(fig:homoVariance) show how counts across all surveyed BBS squares vary across years 2002 to 2019, for each breeding wader species.

![(\#fig:homoVariance)Box plot showing variance of counts across all surveyed Shetland BBS squares and all years, by species](03-results_files/figure-docx/homoVariance-1.png)

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
variance is to transform the response variable to stabilize the variance year-on-year, or applying statistical regression techniques that do not require homogeneity, such as a generalised additive model. 

### Survey Bootstrap {#bootstrap}

Shetland BBS volunteers were able to choose which squares they surveyed. As a result of this non-randomised allocation there could be potential bias in the habitat types surveyed; for example, in-by is closer to roads and housing than upland habitats. To test this a bootstrap of percentage cover of EUNIS habitat categories D, E and F (see \@ref(tab:eunisTable)) across all Shetland 1km squares was undertaken, and then compared to a bootstrap of the same data, but only those squares surveyed by volunteers as part of the Shetland BBS.


![(\#fig:bootstrap)Mean % cover per 1km$^2$ of EUNIS habitat types D, E and F, bootstrap sample of OSGB squares v boostrap of surveyed squares. R=1000](03-results_files/figure-docx/bootstrap-1.png)

This shows that grassland and heathland are significantly oversampled within the Shetland BBS surveys, but bog habitats appear to be sampled proportionally.

##  Detectability

The `r` package `unmarked` was used to generate an estimate for the probability of detection, or *detectability*. Table \@ref(tab:detectabilityTab) shows the average *detectability* across all survey years, for each species.


Table: (\#tab:detectabilityTab)Average detectability of breeding wader species on Shetland 2002-2019

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

The results below detail how remotely sensed satellite data was processed using the Support Vector Machine (SVM) machine learning algorithm to generate a classification for improved grassland across Shetland.

### Shetland Sentinel 2 satelitte dataset

A Sentinel 2 Level 2A spatial dataset was clipped using the Integrated Administration And Control System (IACS) [@Oesterle2003-zb] field boundary shapefile for Shetland. This gave a spatial dataset comprising of land-based habitat only, excluding built areas and roads. The RGB composite of the clipped image is shown in Figure \@ref(fig:plotSentRGB)  



![(\#fig:plotSentRGB)Clipped Sentinel 2 RGB composite of Shetland](03-results_files/figure-docx/plotSentRGB-1.png)






### Habitiat classification training data

In order to classify improved grassland, five other distinctive habitat types were also classified: unimproved grassland, crops, bare peat, cliffs and upland. A number of areas representative of each habitat type were selected as shown in Figure \@ref(fig:habitatTraining). 

![(\#fig:habitatTraining)Habitat classification training areas](03-results_files/figure-docx/habitatTraining-1.png)

### Sampling of habitat training classes

Each habitat training dataset was randomly sampled in order to train the SVM habitat classifier. Distributions for the sampled data for each training set are shown in Figure \@ref(fig:plotSampleDistributions). 

![(\#fig:plotSampleDistributions)Sampled distributions for each training class, from the Sentinel-2 Level 2A dataset of the Shetland archipelago](03-results_files/figure-docx/plotSampleDistributions-1.png)

There are a number of distinguishing observations that can be made from Figure \@ref(fig:plotSampleDistributions). Firstly a visual inspection of the bare peat, cliff, upland and crop classes show a clearly different spectral finger-print for each habitat type. Perhaps unsurprisingly improved and unimproved grassland are relatively similar. On closer inspection it can be seen that the shape of the near infra-red (NIR) spectral histogram appears significantly different for improved grassland. A significant proportion of NIR light is reflected by green vegetation, therefore greener "improved" vegetation is likely to have a strong NIR spectral response [@Pettorelli2014-ad].   

### Support vector machine classifier training

In order to undertake supervised training of an SVM, optimal values for for so-called *hyper-parameters* must be selected. The type of SVM tuned for classifying improved grassland was a radial basis SVM, and two key hyper-parameters must be tuned for when selecting the best model fit. A so-called *search grid* is used to specify all permutations of hyper-parameters that will be utilised to find the optimum fit. For the improved grassland classification, the specific search parameters used are shown in Table \@ref(tab:searchGrid).

















Table: (\#tab:searchGrid)Search parameters used for model fitting of support vector machine

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







### Best model results by classification accuracy

The best SVM model hyper-parameters, as measured by classification accuracy, are shown in Table \@ref(tab:modelResults). It can be seen that when the best model is used to make classification predictions using the training, it achieved an accuracy of 82% with a standard error of 1%.


Table: (\#tab:modelResults)SVM model parameters from best fitting models

 Cost   RBF sigma    Accuracy          se
-----  ----------  ----------  ----------
   20        0.13   0.8233010   0.0094407
   19        0.13   0.8208738   0.0093362
   18        0.13   0.8194175   0.0093179
   19        0.12   0.8194175   0.0091478
   20        0.12   0.8194175   0.0090903







### Model performance using the test dataset

Having selected the best model fit, the same model was used to make predictions against the test dataset. The SVM classifier accuracy was shown to be 85% as shown in Table \@ref(tab:evalPerf).


Table: (\#tab:evalPerf)Classifier performance using test data set

Metric     Estimate  
---------  ----------
accuracy   0.8534091 
kap        0.8240900 

The confusion matrix in Figure \@ref(fig:confusionMatrix) shows the results of the model prediction for each habitat class against those of the test data set. The most incorrectly classified habitat is unimproved grassland (class 2) versus upland (class 3), followed by improved grassland (class 1) versus unimproved grassland. This gives an accuracy for improved grassland classification of c.85% over the test dataset.

![(\#fig:confusionMatrix)Confusion Matrix from classificaton of test dataset](03-results_files/figure-docx/confusionMatrix-1.png)




### Classification across all Shetland habitat

The best fitting model was used across the entire raster dataset for Shetland, to enable classification of all habitat according to the chosen six habitat classes. The results are shown in \@ref(fig:plotPredictionShet). It can be seen that the improved grassland and crop habitat classes are predominantly in the south of the islands; this was validated by a local expert. It can be seen that the main middle island, Yell, is predominantly upland and bare peat.



![(\#fig:plotPredictionShet)Classification of Shetland habitat in order to determine the location of improved grassland](03-results_files/figure-docx/plotPredictionShet-1.png)

<!-- Environmental Covariate Analysis
child doc is loaded in-line -->

## Environmental covariate analysis

Each of the covariates described in Section \@ref(environmental-covariates) were generated for each OS 1km Shetland square (n=3992). 

### Histogram of environmental covariates 

Figure \@ref(fig:covarHisto) shows histograms for all environmental covariates across the Shetland archipelago, at 1km resolution. It can be seen that bog type habitat predominates across Shetland, and that majority of the landscape is at less than 100m elevation. The mode for the pH is around 4, which is typical for acidic peatland [@Paterson2011-ky]. The topsoil carbon content shows that the majority of the Shetland soils have a high organic carbon content; again this is typical of peatland [@Paterson2011-ky]. In contrast a typical mineral rich soil in southern England would have c.3-5% organic carbon content. Note that the percentage landcover of improved grassland is relatively low compared to the more general grassland classification. This shows that agricultural intensification is relatively low in Shetland.

![(\#fig:covarHisto)Histograms of environmental covariates across all of Shetland](03-results_files/figure-docx/covarHisto-1.png)

### Histogram of environmental covariates for Shetland BBS squares only {#bbs-env-cov}

This can be contrasted with covariate histograms for only those OS squares (n=139) that were surveyed as part of the Shetland BBS, as seen in Figure \@ref(fig:sbbsHisto). If these data are indicative of general breeding wader habitat preferences, it would seem that across all surveyed nesting wader species, there is a preference for wet but not water-logged habitat as seen in the AWC histogram. Also, the majority of breeding waders that were surveyed appear to nest within 1km of the coast. It appears that surveyed breeding waders also have a preference for grassland (both improved and unimproved) presents the majority of the habitat cover, over heathland.

![(\#fig:sbbsHisto)Histograms of environmental covariates across only those squares surveyed as part of the Shetland BBS](03-results_files/figure-docx/sbbsHisto-1.png)

### Density plots of environmental covariates

Density plots of all environmental covariates across Shetland BBS squares (n=139) are shown in Figure \@ref(fig:densityPlot). These figures provide an overlay to the histograms in Section \@ref(bbs-env-cov), and represent a smoothed version of a histogram to show the probability density function of the variable. Some distributions are highly skewed, such as distance to sea and elevation. Whilst other covariates like topsoil organic carbon and bog cover are largely a uniform distributed. None of the covariates appear to be normally distributed.

![(\#fig:densityPlot)Density plots of environmental covariates against breeding wader count data](03-results_files/figure-docx/densityPlot-1.png)

<!-- Environmental Covariate Response
child doc is loaded in-line -->

## Breeding wader abundance response to environmental covariates {#abun-resp-gam}

Generalised Additive Models (GAMs) for breeding wader abundance response across the five different species were generated from 2002–10 and 2011-19. A GAM was produced for each of the 10 environmental covariates (predictor variables), and for each of the two analysis periods.






Appendix \@ref(gam-abun-response-params) details the GAM parameter results from the model fitting process, for the two periods where the abundance response (density) was modelled against environmental covariates. The associated plots showing breeding wader density response against each environmental covariate are shown in Appendix \@ref(gam-abun-response-plots). Note those models that result in a parametric term (an environmental covariate) that is statistically significant (p<0.05) have plots that are coloured red. The statistically significant correlations between breeding wader density and environmental covariates are summarised for each species in heatmaps; Figure \@ref(fig:heatMap200210) for 2002-10 and Figure \@ref(fig:heatMap201119) for 2011-2019. 

![(\#fig:heatMap200210)Summary of associations between breeding wader density and environmental covariate, between 2002 and 2010 inclusive](03-results_files/figure-docx/heatMap200210-1.png)
For the 2002-10 survey period in Figure \@ref(fig:heatMap200210), it can be seen that pH is only statistically significant for one species (Snipe), whilst topsoil organic carbon and grassland are oppositely correlated. Distance to sea is perhaps the most interesting covariate in that Lapwing show a greater association at the coast whilst Curlew, Oystercatcher and Snipe show greater densities inland. Notable results are that all nesting species are negatively associated with higher percentages of carbon within the topsoil per km$^2$, and all nesting species are positively associated with increased grassland coverage per km$^2$.

![(\#fig:heatMap201119)Summary of associations between breeding wader density and environmental covariate, between 2011 and 2019 inclusive](03-results_files/figure-docx/heatMap201119-1.png)

In Figure \@ref(fig:heatMap201119) we can see that there are fewer associations that are not statistically significant. Again all species are positively associated with increased grassland coverage per km$^2$, and in the second analysis period this is true for increased heathland coverage per km$^2$. All species are now negatively associated with increased bog coverage per km$^2$ and increased bare peat coverage per km$^2$. It can also be seen that all species, apart from Snipe, are positively associated with increased improved grassland coverage per km$^2$. Where as the exact opposite is true for available water capacity per km$^2$.

For Curlew it is seen that all covariate associations are now statistically significant (versus 2002-2010 where pH and Heathland cover were not significant). Oystercatcher also have all covariates with statistically significant associations. Note that for Oystercatcher, for the second analysis period, results for the distance to sea association show a negative association with increasing distance. Lapwing only have one covariate, pH, that is not statistically significant, and otherwise show identical results to Oystercatcher. For Redshank the main change in the later analysis period is that Heathland percentage cover is now statistically significant, and has a positive association. Snipe now have a positive association with available water capacity and a negative association with percentage bog cover.

## Population change response against environmental covariates {#pop-chg-abun-plot}

A third model was generated by using the abundance response from the first two GAMs in Section \@ref(abun-resp-gam). By using the response of the 2002-2010 wader densities as the offset for the 2011-19 densities, a third series of GAMs were fitted to show the ratio of population change as a function of environmental covariates. The population change model will give an indication of how breeding wader densities have changed over time for a given environmental covariate. For example, are species decreasing over time in habitats that are thought to offer lower food availability for chicks, such as heathland.. The results of the analysis are shown in Figure \@ref(fig:heatMapPopChg).

![(\#fig:heatMapPopChg)Summary of population change ratio associations between breeding wader density and environmental covariate, between 2002 and 2019 inclusive](03-results_files/figure-docx/heatMapPopChg-1.png)

Figure \@ref(fig:heatMapPopChg) suggests that the environmental covariates that have had the most positive associations with breeding wader population changes over the two analysis periods are heathland percentage cover and available water capacity. The percentage of bare peatland has had no statistical significance, followed by the percentage grassland cover that has only one negative association with the population change ratio of Redshank. The model parameters and associated plots for population change ratio modelling are shown in Appendix \@ref(gam-pop-chg-params) and Appendix \@ref(gam-pop-chg-plots) respectively.


<!-- Information Theory Response
child doc is loaded in-line -->

## Information Theory (IT) covariates 

GAMs for breeding wader abundance response across the five different species were generated from 2002–10 and 2011-19. In addition to the environmental covariates, they included five IT covariates. The model parameter results for all species across the two analysis periods can be seen in Appendix \@ref(gam-it-resp-params). A third model was generated by taking the abundance response from the first two models to generate the ratio of population change between the two response periods, the model parameters for this model can be seen in Appendix \@ref{#gam-it-pop-chg-params}.

### Histograms of Information theory covariates

Histograms of IT covariates using the EUNIS landscape categorisation, across all of Shetland are shown in figure \@ref(fig:itHisto). The *marginal entropy* for the Shetland landscape is approximately normally distributed, indicating that habitat within the Shetland landscape is spatially diverse but that very low and highly diverse habitat within Shetland are relatively rare. The mode of the *conditional entropy* is relatively low with a distribution that shows significant positive skew; this suggests that the Shetland landscape has relatively low geometric intricacy. This arises when cells of one category within a landscape raster are predominantly adjacent to cells of the same category. The overall spatio-thematic complexity is measured by the *joint entropy*. This can be thought of as quantifying the uncertainty in determining the habitat type of a focus cell and an adjacent cell. For Shetland, joint entropy appears to be approximately normally distributed. This indicates that habitat with very high or low spatio-thematic complexity is relatively rare on Shetland. Due to the spatial autocorrelation, the value of *mutual information* tends to grow with a diversity of the landscape (marginal entropy). To adjust this tendency, it is possible to calculate *relative mutual information* by dividing the mutual information by the marginal entropy. Relative mutual information always has a range between 0 and 1, and quantifies the degree of aggregation of spatial habitat. It can be seen that for Shetland, relative mutual information is distributed with significant negative skew. This implies that habitat types across Shetland are predominantly aggregated - small relatively information values indicate significant fragmentation in landscape habitat patterns.

![(\#fig:itHisto)Histograms of Information Theory covariates across all Shetland OS 1km squares](03-results_files/figure-docx/itHisto-1.png)

### Histograms of Information Theory covariates for surveyed squares only

1km squares surveyed as part of the Shetland BBS were used to generate IT covariates histograms using the EUNIS landscape categorisation, as shown in Figure \@ref(fig:itSBBSHisto). Here we can see that the *conditional entropy* and the *marginal entropy* across all surveyed squares had a mode that was significantly higher than the Shetland wide values shown in Figure \@ref(fig:itHisto). There is also significantly less negative negative skew in the *relative mutual information* of the surveyed squares. 

![(\#fig:itSBBSHisto)Histograms of Information Theory covariates across SBBS surveyed sqaures only ](03-results_files/figure-docx/itSBBSHisto-1.png)

### Information Theory covariates abundance response model



GAMs were fitted for each of the two analysis periods using IT metrics as covariates against breeding wader abundance. Figures \@ref(fig:itHeatMap200210) and \@ref(fig:itHeatMap201119) summarise the associations between the abundance response and IT covariates used in the univariate GAMs, for the periods 2002-10 and 2011-19 respectively.

![(\#fig:itHeatMap200210)Summary of associations between breeding wader density and IT covariates, between 2002 and 2010 inclusive](03-results_files/figure-docx/itHeatMap200210-1.png)

![(\#fig:itHeatMap201119)Summary of associations between breeding wader density and IT covariates, between 2011 and 2019 inclusive](03-results_files/figure-docx/itHeatMap201119-1.png)
Appendix \@ref(gam-it-resp-params) shows the GAM parameter results generated by fitting the model to the data when information theory metrics are used as covariates. Plots showing the abundance response against IT covariates are shown in Appendix \@ref(gam-it-resp-plots).

It seems that the response for Snipe abundance to IT covariates is identical for the two periods. Snipe have a positive association with *relative mutual information*, or habitats that have a high degree of aggregation, such as heathland. *Relative mutual information* has no statistically significant association for any other species in the second analysis period, although it appears to be statistically significant and positively associated for all species in the first analysis period. This indicates that breeding waders, apart from Snipe, may have moved from areas comprising habitat that is highly aggregated to areas that are less so. This hypothesis is partially supported by the fact that the second analysis period shows increase in wader species, apart from Snipe, that are positively associated with *marginal entropy*; a measure of habitat thematic diversity.

### Population change model against IT covarirates

By using the response of the 2002-2010 wader densities as the offset for the 2011-19 densities, a third series of GAMs were fitted to show the ratio of population change in response to IT covariates. This is summarised in Figure \@ref(fig:itHeatMapPopChg). It can be seen that there are no statistically significant results for Redshank or Snipe, or for marginal entropy as a covariate.

![(\#fig:itHeatMapPopChg)Summary of associations between breeding wader density and IT covariates, between 2011 and 2019 inclusive](03-results_files/figure-docx/itHeatMapPopChg-1.png)
Perhaps the most significant result is that which supports the idea that breeding wader densities have declined in habitats that exhibit a large spatial aggregation. This is shown by the fact that Lapwing and Oystercatcher populations are negativelty associated over time, with increased *relative mutual information*. Appendix \@ref(gam-it-pop-chg-params) shows the GAM parameters generated by fitting the population change model to the data. Plots for population change response against IT covariates are shown in Figure \@ref(gam-it-pop-chg-plots).


<!-- Abundance over time and spatial distribution
child doc is loaded in-line -->

## Wader abundance trends

A random forest regression model was used to fit an abundance response using all 10 environmental covariates. The parameterisation and results are outlined below.



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



### Tuning the model hyper parameters

A search grid over 10 different folds gave initial results for various permutations of hyper parameters as shown in Appendix \@ref(hyp-params). Each figure shows the results for a particular species. Each hyper-parameter permutation is plotted against the resulting root mean squared error (rmse). 

### Further model hyper parameter tuning

Given the initial results in \@ref(hyp-params) the initial range over which the hyper-parameter search was conducted, was refined further by searching over a revised range according by selecting upper and lower limits for hyper-parameters that gave the lowest rmse as indicated by the initial results. The range used was that which gave the lowest rmse as given in Appendix \@ref(hyp-params). The results of the revised search grid range can be seen in Appendix \@ref(final-fit). Again each plot is for a separate species.

<!-- Now refine the tuning per species -->




From the plots in Appensix \@ref(final-fit) we can see which hyper parameters give the best fit, when using root mean squared error as an evaluation metric. It can be seen that the model fit for Snipe has the largest RMSE. whilst Redshank has the lowest. For each species the minimum rmse result for the best model fit, together with the associated hyper parameters (`trees`= 1000 for all models) is shown in Table \@ref(tab:bestByRMSE).


Table: (\#tab:bestByRMSE)Lowest RMSE for best fitting model, for each species of breeding wader

Species    mtry   min_n       rmse
--------  -----  ------  ---------
CU            4       6   1.448835
L             5       4   1.672523
OC            4      10   1.845994
RK            7       3   1.429948
SN            2       6   2.718174



### Variable importance in model fit

Having selected the best model fit the variable importance for each species was assessed. The `r` package `vip` [@vip] was used to explore the relative importance of different covariates in the model fit. The results are shown in Appendix \@ref(vip-plots).



It can be seen that pH, X (longitude) and grassland percentage coverage for a given OS 1km square appear to be the most important covariates for predicting abundance in Curlew. For Lapwing, pH, heathland percentage coverage and topsoil organic carbon content are the most important variables. Whilst for Oystercatcher, grassland and heathland percentage cover are almost equivalent in their importance followed by longitude. For Redshank and Snipe, available water capacity and heathland are the most important covariates in predicting abundance.



### Breeding wader population estimates from 2002 to 2019 {#pop-estimates}

The random forest regression model was used to predict species abundance over *all* (n=3992) Shetland BBS 1km squares. The model gave a mean estimate together with lower and upper confidence intervals (5% and 95% percentiles respectively), across every year the survey was run (2002 to 2019). The population estimate results are shown in Appendix \@ref(pop-results) and plotted in Figure \@ref(fig:plotAbunResults)




![(\#fig:plotAbunResults)Breeding wader population estimates - number of pairs of breeding waders by species, 2002 to 2019. Grey shaded area indicates upper and lower confidence intervals](03-results_files/figure-docx/plotAbunResults-1.png)

Across the years 2002 to 2019 the abundance of breeding wader pairs across all species appear to have decreased, with the exception of Snipe. The most significant decline was for Lapwing. Note that the confidence intervals for Snipe are highly variable in certain years. Table \@ref(tab:popChgTable) shows the change in breeding wader abundance by species between 2002 and 2019.


Table: (\#tab:popChgTable)Change in breeding wader abundance across all species, between the years 2002 and 2019

Species    2002   2019   % Change
--------  -----  -----  ---------
CU         4597   4088      -11.1
L          3474   2638      -24.1
OC         5269   4760       -9.7
RK         2390   2248       -5.9
SN         6043   7391       22.3

### Lapwing abundance association with grassland holdings {#lapwing-grassland}

Data from 2002 to 2017 for grassland holdings in hectares categorised as: tillage, grassland less than five years old (reseeded grassland), grassland five years or greater and private grazing were tested for normality, and found to be log-normally distributed. A linear regression was plotted for Lapwing abundance versus each grassland categorisation (in Hectares) as shown in Figure \@ref(fig:lapwingGrasslandPlot).




![(\#fig:lapwingGrasslandPlot)Association between the size of grassland categories on Shetland and Lapwing population abundancebetween 2002 and 2017. Agricultural statistics taken from Scottish Agricultural Survey](03-results_files/figure-docx/lapwingGrasslandPlot-1.png)
Figure \@ref(fig:lapwingGrasslandPlot) shows that Lapwing population size is positively associated with the size of grassland that is less than five years old (that grassland which has been reseeded) and tillage (land prepared for spring crops). Figure \@ref(fig:lapwingGrasslandPlot) also shows that Lapwing population abundance is negatively associated with grassland that is not reseeded (Grass >= 5y).

The `r` package `gamlss` [@gamlss] was used to fit a log-normal model for Lapwing population abundance with grassland less than 5 years old as a covariate. The grassland < 5 years old was a statistically significant covariate (p<0.0001), and the residuals of the model were approximately normally distributed as shown in Figure \@ref(fig:fitLapwingModel).


```
## GAMLSS-RS iteration 1: Global Deviance = 192.9757 
## GAMLSS-RS iteration 2: Global Deviance = 192.9757
```

![(\#fig:fitLapwingModel)Residuals for model fit of Lapwing population estimates to Shetland improved grassland less than five years old. Agricultural statistics taken from Scottish Agricultural Survey](03-results_files/figure-docx/fitLapwingModel-1.png)

## Spatial abundance distriution of breeding waders

The population estimates results in \@ref(pop-estimates) are based on a spatial prediction. As such they can be plotted to show how species abundance is spatially distributed across Shetland. Figure \@ref(fig:spatialDistributions) shows the abundance distribution, per 1km$^2$ (density) for each species in 2019. 

![(\#fig:spatialDistributions)Spatial abundance distribution of breeding waders for 2019](03-results_files/figure-docx/spatialDistributions-1.png)

It can be seen that Snipe are widespread, and that Curlew and Oystercatcher are significantly present on the western side of Shetland, as suggested by the variable importance plots in Appendix \@ref(vip-plots). Lapwing and Redshank have the lowest population densities and seem to be concentrated in the south west of Shetland.

### Net spaital abundance change by species, between 2002 and 2019 

Given the spatial abundance distribution for 2002 and 2019, it is possible to plot the net change in breeding wader abundance, for each 1km$^2$, between the two years. This is shown in Figure \@ref(fig:netChgPlot).

![(\#fig:netChgPlot)Change in breeding wader density (count/km2) between 2002 and 2019 on Shetland](03-results_files/figure-docx/netChgPlot-1.png)

It can be seen that the drop in abundance as shown in Appendix \@ref(pop-results) is reflected in the net change plots in Figure \@ref(fig:netChgPlot). 

The initial analysis of the status of surveyed 1km squares (see Figure \@ref(fig:aggPopChg)) suggested that Lapwing had undergone a decline, and Figure \@ref(fig:netChgPlot) shows that this has occurred in the south west and north east over the two analysis periods. Oystercatcher appear to have undergone a significant decline in the north east of Shetland (the islands of Unst and Fetlar). Where as Snipe appear to have increased in most upland areas of  Shetland, and in particular on the Fetlar RSPB reserve.

<!-- Predict improve grassland and then work
out if strength of connectivity with wader breeder 
territories are significant -->





