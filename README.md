# Hydrological Modeling for Streamflow Using ATS: Performance Comparison with USGS NHM and Observed Data
This repository contains the data, model inputs, and scripts necessary to reproduce the hydrological simulations conducted with the Advanced Terrestrial Simulator (ATS) and to compare its performance against the calibrated USGS National Hydrologic Model (NHM-PRMS) and observed USGS gage data.

## Summary
This study evaluates the performance of the Advanced Terrestrial Simulator (ATS) (Bhanja et al., 2023) and the USGS National Hydrologic Model-Precipitation Runoff Modeling System (NHM-PRMS) (Hay et al., 2023) in simulating streamflow and evapotranspiration (ET) in the Flat Brook Basin, New Jersey. ATS was configured at coarse and fine mesh resolutions without calibration, while NHM-PRMS applied a calibrated semi-distributed setup. Simulation outputs were compared against USGS gage observations and MODIS ET data for the 2014–2015 hydrologic year using R², NSE, RMSE, and KGE metrics. Results show that increasing ATS mesh resolution improved hydrologic realism, with the fine mesh simulation substantially reducing peak flow overpredictions and maintaining higher baseflows compared to the coarse mesh. Notably, the ATS Fine Mesh outperformed NHM-PRMS during moderate to high flow conditions (30%–80% exceedance probabilities), better capturing storm recession and seasonal flow patterns. However, both ATS configurations still severely overestimated extreme peak discharges and underestimated low flows. NHM-PRMS produced overall stronger performance across all flows, maintaining positive NSE and KGE values and more realistic low-flow behavior. Runtime analysis indicated that mesh refinement significantly increased ATS computational cost, but not strictly proportionally. For ET simulation, ATS demonstrated closer agreement with MODIS observations throughout the year, particularly during spring and summer, whereas NHM-PRMS consistently overpredicted ET during warmer seasons. These findings highlight that while uncalibrated ATS models can be easier to set up and perform reasonably well under certain flow conditions and offer advantages for ET modeling, calibration and structural refinement are necessary to achieve reliable full-spectrum streamflow prediction. Future work should explore extended calibration strategies and multi-watershed evaluation. 

## Methods
- Modeling tool
ATS will be used due to its capability to integrate surface and subsurface hydrological processes in a physically based manner. ATS is particularly useful for catchments with complex hydrological interactions, allowing for a more detailed representation of soil moisture and groundwater-surface water interactions (Molins et al., 2022; Xu et al., 2022). The USGS NHM, which provides large-scale streamflow simulations, will be used as a benchmark for comparison. Two catchments in Northern Utah will be selected for this study due to data availability and the importance of streamflow modeling in this region for integrated water management. Climatic, topography and soil data will be used for the ATS model. NHM output data and observed values from USGS gages will be retrieved for comparison and benchmarking. 

- Study Area
The study area is the Flat Brook Basin, located in northern New Jersey, part of the Delaware River system, upstream of USGS gage 01440000 (FLAT BROOK NEAR FLATBROOKVILLE, NJ). The basin covers approximately 165 km², with perennial baseflow conditions supported by year-round precipitation.

## Repository Structure
```
|-- data
|-- model
|   |-- inputs
|   `-- outputs
|-- scripts
`-- results
|   |-- figures
```
- `data`: provides data needed to run the model (e.g., meshes, meterological forcing, observation, etc.)
- `model`: provides input files and essential model outputs (e.g., observation points, mass balance)
- `scripts`: provides the scripts or jupyter notebooks for pre- and post- processing model files
- `results`: provides any results generated from the model analysis (e.g., figures associated with report)

## Usage Instructions

There are two options for reproducing the ATS simulations:

* Option 1: Direct Reproduction
    Pre-generated input files, computational meshes, and forcing datasets are available in the data and model/inputs folders. These can be directly used to rerun the ATS model without re-generating the setup.

* Option 2: Regenerate Model Inputs
    To regenerate ATS model inputs from scratch, use the Jupyter notebooks provided in the scripts folder:

    1. Clone or download this repository.

    2. Navigate to the scripts directory.

    3. Run the notebooks in order:

        * 1-mesh.ipynb: Generates triangular meshes for the watershed and Maps land cover, soil, and geological parameters to the mesh.

        * 2-daymet.ipynb: Processes and maps meteorological forcings from DAYMET data.

        * 3-ats_input_file.ipynb: Assembles all input datasets into ATS-compatible format.

    4. The generated files will match the structure found in the data and model/inputs folders and can be used to reproduce the simulations.

The ATS model can then be executed using the prepared XML input files following standard ATS run procedures.

**_NOTE:_** Mesh generation and forcing processing require access to Watershed Workflows (Coon & Shuai, 2022) and associated Python libraries.

## Citation

Bhanja, S. N., Coon, E. T., Lu, D., & Painter, S. L. (2023). Evaluation of distributed process-based hydrologic model performance using only a priori information to define model inputs. Journal of Hydrology, 618, 129176. https://doi.org/10.1016/j.jhydrol.2023.129176

Coon, E. T., & Shuai, P. (2022). Watershed Workflow: A toolset for parameterizing data-intensive, integrated hydrologic models. Environmental Modelling & Software, 157, 105502. https://doi.org/10.1016/j.envsoft.2022.105502

Hay, L. E., LaFontaine, J. H., Beusekom, A. E. V., Norton, P. A., Farmer, W. H., Regan, R. S., Markstrom, S. L., & Dickinson, J. E. (2023). Parameter estimation at the conterminous United States scale and streamflow routing enhancements for the National Hydrologic Model infrastructure application of the Precipitation-Runoff Modeling System (NHM-PRMS). In Techniques and Methods (Nos. 6-B10). U.S. Geological Survey. https://doi.org/10.3133/tm6B10

Molins, S., Svyatsky, D., Xu, Z., Coon, E. T., & Moulton, J. D. (2022). A Multicomponent Reactive Transport Model for Integrated Surface-Subsurface Hydrology Problems. Water Resources Research, 58(8), e2022WR032074. https://doi.org/10.1029/2022WR032074

Xu, Z., Molins, S., Özgen-Xian, I., Dwivedi, D., Svyatsky, D., Moulton, J. D., & Steefel, C. (2022). Understanding the Hydrogeochemical Response of a Mountainous Watershed Using Integrated Surface-Subsurface Flow and Reactive Transport Modeling. Water Resources Research, 58(8), e2022WR032075. https://doi.org/10.1029/2022WR032075


