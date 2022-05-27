[![DOI](https://zenodo.org/badge/340710848.svg)](https://zenodo.org/badge/latestdoi/340710848)  

# Interpreting CNN-LSTMs for streamflow modelling across glacial, nival, and pluvial regimes in southwestern Canada

This repository contains the code used in the study:  
Anderson, Sam, and Radic, Valentina. "Interpreting deep machine learning for streamflow modelling across glacial, nival, and pluvial regimes in southwestern Canada".  Frontiers in Water (submitted 2022).  

Contact: Sam Anderson  
Email: anderson.sam.lucas@gmail.com
___  
## Overview  
The code in this repository can reproduce all figures and findings in the study.  All data used is publicly accessable.  The code in this repository uses the CNN-LSTM models as trained in the paper ["Evaluation and interpretation of convolutional long short-term memory networks for regional hydrological modelling"](https://hess.copernicus.org/articles/26/795/2022/hess-26-795-2022.html), with [associated code provided provided here](https://github.com/andersonsam/cnn_lstm_era).  This repository contains the following files:

* main.ipynb: Defines functions, loads preprocessed data, carries out four interpretation experiments, creates figures

___
## How to run code  
1. Set up directory structure.
    * It is best to run main.ipynb on a GPU for faster processing.  This code is set up to run on Google Colab, which can access files stored in Google Drive and Github.  Organize files as described below.

2. Download required data.
    * Follow steps 1 - 8 as [outlined here](https://github.com/andersonsam/cnn_lstm_era).
    * Note: The CNN-LSTM models can be trained as [outlined here](https://github.com/andersonsam/cnn_lstm_era) if desired, OR the pre-trained models can simply be loaded.  In main.ipynb, the pre-trained models are loaded in rather than trained.

3. Run main.ipynb

___  
## Summary of code 

We use the models as trained [here](https://github.com/andersonsam/cnn_lstm_era).  The models have a sequencial CNN-LSTM structure, where daily temperature and precipitation fields are passed through a convolutional network that outputs feature vectors for each day.  The series of feature vectors is then passed through an LSTM network that predicts daily streamflow at multiple stream gauge stations.  

<img src= "https://github.com/andersonsam/cnn_lstm_interpret/blob/main/Figures/model_architecture.png" width=100% >

### Experiment 1: Model sensitivity through space/time  
Here we investigate if the model has learned to focus on physically relevant areas of the input domain.  The temporal evolution of sensitivity maps through time, as derived for each cluster, reveals two distinct spatial patterns of sensitivity.  One spatial pattern of sensitivity occurs during high flow periods, while the other occurs during low flow periods.  We derive these patterns for each subregional cluster of stream gauge stations.  

<img src= "https://github.com/andersonsam/cnn_lstm_interpret/blob/main/Figures/heat_vision_cluster_0.gif" width=50% >
<img src= "https://github.com/andersonsam/cnn_lstm_interpret/blob/main/Figures/heat_vision_cluster_5.gif" width=50% >

### Experiment 2: Input variable importance through time  
Here we determine how strongly the model output is linked to temperature and precipitation separately, and to reveal how the strength of those links change over a year.  These links are different across streamflow regimes and change through the year since the physical drivers of flow change through the year.  In this experiment we perturb the input temperature and precipitation channels independently to determine when, where, and if the model is sensitive to perturbations of the input weather channels.  

<img src= "https://github.com/andersonsam/cnn_lstm_interpret/blob/main/Figures/channel_sensitivity.png" width=75% >

### Experiment 3: Streamflow-driving temperature and precipitation  
Here we explore how well the model has learned the concept that the weather conditions that drive runoff generation vary by streamflow regime and season.  We start by identifying the temperature and precipitation anomalies that drive modelled daily streamflow to increase from one day to the next during each season.  To do so, we identify the input weather fields that are associated with the maximum single-day increase in output neuron values.  

<img src= "https://github.com/andersonsam/cnn_lstm_interpret/blob/main/Figures/0antecedent_328top.png" width=75% >

### Experiment 4: Representation of glacier runoff within LSTM cell states  
Here we rely on the assumption that some cell states in LSTM models can be found to represent water storage or flux terms (e.g. Kratzert et al. 2018).  Since glacier melt is an important contributor to streamflow in glaciated rivers, we expect to find a representation of glacier melt within the set of cell states in the ensemble of models.  Our goal here is to design an approach to identify and interpret the LSTM cell states that represent glacier runoff, without a priori estimation of glacier runoff itself. We identify a set of cell states that act as a temperature-dependent streamflow source that is most strongly related to temperature during the glacier melt season.  

<img src= "https://github.com/andersonsam/cnn_lstm_interpret/blob/main/Figures/cell_state_panels.png" width=75% >

___  
## Directory structure  
Google Drive organization (for Colab access):

* My Drive/  
	* Colab Notebooks/  
		* cnn_lstm_era/   
			* models/  
			* output/  
			* heat_maps/ 
			* data/
				* province_borders/  
				* RGI/

___  
## 
