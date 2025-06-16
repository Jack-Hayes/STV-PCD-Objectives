# :airplane: :rocket: :alien: STV-PCD-Objectives :alien: :rocket: :airplane:

## Index
- [What have people done already](#what-have-people-done-already)
  - [In-House UW Shean Lab](#in-house-uw-shean-lab)
  - [NASA ASP](#nasa-asp)
  - [Pietro Milillo's Lab (UH)](#pietro-milillos-lab-uh)
  - [Similar work external to STV](#similar-work-external-to-stv)
- [What questions do we have](#what-questions-do-we-have)
  - [Stereo photogrammetry and canopy heterogeneity](#1-stereo-photogrammetry-and-canopy-heterogeneity)
  - [Volcanoes and lava flows: DEM requirements for mapping extent & thickness over time](#2-volcanoes-and-lava-flows-dem-requirements-for-mapping-extent--thickness-over-time)
- [Earth Science Objectives](#earth-science-objectives)
- [Earth Science Objectives](#earth-science-objectives)
  - [2017 Decadal Survey SATM](#2017-decadal-survey-satm)
  - [2021 STV Study Team Report](#2021-stv-study-team-report)

---

## What have people done already

### In-House UW Shean Lab
- **Coincident**  
  - Conveniently search across different data providers for coincident elevation measurements.  
  - Utilities to efficiently load measurements into GeoPandas and Xarray for intercomparison.  
  - Repo / docs: https://coincident.readthedocs.io/en/latest/
  - First dataset: USGS 3DEP 4-way overlaps with Maxar stereo, GEDI, and ICESat-2 (private as of 06/13/2025).
  - Other datasets: NCALM, NOAA, NEON data (less accessible).
- **lidar_tools**  
  - CLI scripts to process LiDAR data: get EPT metadata or download LAZ via ‘coincident’, then process DSM/DTM/intensity maps.  
  - Note: separate environments for lidar_tools and ‘coincident’ due to PDAL dependencies.  
  - Repo: https://github.com/uw-cryo/lidar_tools
- **DeepDEM**  
  - Deep learning as intelligent post-processing filter to refine DSMs from stereo satellite imagery.  
  - Repo: https://github.com/uw-cryo/DeepDEM
- **3D CRS Transformation Resources**  
  - Centralized repository for resources, documentation, and code samples for 3D CRS transformations when combining datasets for precise geodetic analysis.  
  - Repo: https://github.com/uw-cryo/3D_CRS_Transformation_Resources
- **Sliderule**  
  - Public web service with APIs for efficiently processing GEDI and ICESat-2 data.  
  - Website / API docs: https://slideruleearth.io/

### NASA ASP
- **StereoPipeline**  
  - Cloud-based processing for STV (Surface Topography and Volcanology) workflows.  
  - Docs: https://stereopipeline.readthedocs.io/en/latest/introduction.html

### Pietro Milillo's Lab (UH)
- Tools for estimating trend accuracy and miss probabilities for altimetry missions.
- **AI-Driven TanDEM-X Penetration Bias Estimation in Antarctica Using ICESat-2 and ECMWF Data**  
  - Approaches to quantify bias in radar altimetry using ICESat-2 as reference.
- Repo: https://github.com/Milillo-lab

### Similar work external to STV
- **Centre National d’Études Spatiales (CNES) Bulldozer**  
  - Pipeline to extract a Digital Terrain Model (DTM) from a Digital Surface Model (DSM), supporting both noisy satellite DSMs and high-quality LiDAR DSMs.  
  - Repo: https://github.com/CNES/bulldozer  
- **GEDTM30 (Europe OpenGeoHub)**  
  - Global 1-arc-second (~30 m) Digital Terrain Model built via ML-based data fusion using ICESat-2 and GEDI (~30 billion points).  
  - Generates 15 land surface parameters at scales 30–960 m.  
  - Repo: https://github.com/openlandmap/GEDTM30  
  - Publication in review: https://www.researchsquare.com/article/rs-6280607/v1  
- **EarthScape (University of Kentucky)**  
  - Open-source, AI-ready geospatial dataset for surficial geologic mapping and Earth surface analysis.  
  - Integrates high-resolution aerial imagery, DEM tiles, multi-scale DEM-derived terrain features, and ancillary vector data.  
  - Repo: https://github.com/masseygeo/earthscape  
  - Dataset portal: https://uknowledge.uky.edu/kgs_data/16/
- **GStatSim (University of Florida Glacier Group)**  
  - Statistical interpolations of sparse topography observations (point → grid).  
  - Repo: https://github.com/GatorGlaciology/GStatSim

---
## What Questions Do We Have

Below are key high-level questions around STV-science proposals, gaps from the Decadal Survey/Solicitation, and examples (e.g., canopy heterogeneity, lava-flow mapping)

### 1. Stereo photogrammetry and canopy heterogeneity

#### Question
Why does stereo photogrammetry fall short for canopy structure, and what sensor/modalities can fill this gap?

#### Background & Limitations
- Stereo DEMs provides the canopy “top surface” but lacks internal vertical detail (e.g., multiple canopy layers, understory).
- It often misses sub-canopy relief and cannot retrieve vertical distribution of foliage or strata.
- In dense or complex forests (multi-layered, tall tropical canopies), stereo shadows and occlusions reduce quality.

#### Complementary Data
1. **Lidar**  
   - Spaceborne (e.g., GEDI) or airborne waveform or discrete-return lidar yields vertical profiles of canopy (height distribution, layering).  
   - Provides precise canopy height metrics (e.g., RH metrics from waveform), gap fraction, vertical foliage distribution.
2. **Radar**  
   - Lower-frequency radar (e.g., P-band) can penetrate canopy to some extent, offering information on larger-scale biomass or structure—but typically coarser horizontal resolution and more complex inversion.
   - SAR interferometry can track canopy height change indirectly (e.g., by monitoring ground vs. canopy phase), but vertical detail is limited.
3. **Imaging Spectroscopy / Hyperspectral**  
   - Tracks biochemical or biochemical–structural proxies (e.g., leaf chemistry) but does not directly measure vertical structure.
   - Useful in combination with lidar: structure + chemistry.

#### Example Studies / Citations
- 

---

### 2. Volcanoes and lava flows: DEM requirements for mapping extent & thickness over time

#### Question
For monitoring active lava flows, what DEM resolution, revisit frequency, and complementary datasets are required to capture extent and thickness evolution?

#### Key Requirements
1. **Horizontal resolution**  
   - Aim <5 m to delineate flow margins, narrow channels, lobes.  
   - Airborne/UAV lidar can reach sub-meter to 1 m resolution over targeted zones.  
   - Satellite stereo (e.g., WorldView) ~5–10 m may miss small features; useful for broader context.
2. **Vertical accuracy/precision**  
   - Target <0.5 m vertical precision to detect flow thickness changes and infer effusion rates.  
   - DEM differencing noise must be substantially below expected thickness change (e.g., if thickness change ~1 m, DEM error <0.25 m).
3. **Revisit frequency**  
   - Active eruptive phases: ideally daily to weekly DEM updates.  
   - Satellite optical (e.g., Sentinel-2) can track areal extent daily if clear; stereo DEM likely less frequent (tasking needed).  
   - SAR (e.g., InSAR or SAR tomography) for cloud-penetrating DEM, revisit depends on orbit (e.g., TanDEM-X, Sentinel-1).  
   - Airborne/UAV campaigns: targeted during eruption onset or when rapid change expected.
4. **Complementary data**
   - **Thermal infrared imagery**: identifies active flow front, temperature anomalies; can help prioritize DEM acquisitions.  
   - **Gas emissions / thermal flux measurements**: to relate volume changes from DEM differencing to effusion rates and energetics.  
   - **Time-lapse optical or thermal cameras**: continuous monitoring of front advance, used alongside DEM snapshots.

#### Example Studies / Citations
- The Volcano Remote Sensing Bible https://pubs.usgs.gov/publication/sir20225116 (https://doi.org/10.3133/sir20225116)

---

## Earth Science Objectives

### 2017 Decadal Survey SATM

From the NASA 2017 Decadal Survey Science and Applications Traceability Matrix

https://nap.nationalacademies.org/read/24938/chapter/17

This drives development of processing pipelines (e.g., coincident, lidar_tools, DeepDEM) and integration frameworks for multi-source data.

> **Summary:**  
> The prioritized objectives emphasize high-resolution topographic and elevation measurements primarily in Solid Earth (volcanic deformation, tectonics, landslides, tsunami run-up, coastal motion) and Cryosphere (ice-sheet elevation/bed mapping) domains. Horizontal resolutions often target ~1 m for bare-earth models, with some broader missions at 30–100 m for ice-sheet mapping. Vertical accuracies range from **10 cm to 1 m** for detailed studies, up to **30 m** for bed/elevation mapping. Temporal needs span **once** (global baselines) to **weekly to daily** (ice-sheet change, deformation monitoring) and **time scales of days to weeks** (eruption deformation). Methods combine airborne/UAV lidar, spaceborne lidar (ICESat-2, GEDI), SAR interferometry (NISAR, UAVSAR), optical stereo supplements, radar altimetry, and gravity missions.  

| Earth Science/Application Objective | Importance | Geophysical Observable | Measurement Parameters | Recommended Method |
|---|---|---|---|---|
| **C-1c.** *Determine the changes in total ice-sheet mass balance to within 15 Gton/yr over the course of a decade and the changes in surface mass balance and glacier ice discharge with the same accuracy over the entire ice sheets, continuously, for decades to come.* | <span style="background-color:#ccffcc">Most Important</span> | Ice-sheet elevation | Vertical resolution/range: **10–20 cm**; Horizontal resolution/range: **100 m**/pole to pole; Temporal sampling: **weekly to daily**; Precision: **10–20 cm** | Operation IceBridge, ICESat-2, {WorldView satellites}, GLISTIN |
| **C-1c.** *Determine the changes in total ice-sheet mass balance…* | <span style="background-color:#ccffcc">Most Important</span> | Ice-sheet bed elevation, ice-shelf cavity shape | Vertical resolution/range: **30 m**; Horizontal resolution/range: **100 m**/pole to pole; Temporal sampling: **one time**; Precision: **30 m** | Operation IceBridge, EVS-2 OMG, new EVS Antarctica |
| **E-2c.** *Assess ecosystem subsidies from solid Earth.* | <span style="background-color:#ffe5cc">Important</span> | Dust inputs, soil erosion, landslides, black carbon | High spatial resolution (**1 m**), bare-Earth topography at **0.1 m vertical accuracy**; Spectral radiance (10 nm; 380–2500 nm); GSD = 30–45 m | Aircraft lidar; VSWIR; MISR |
| **S-1a.** *Measure the pre-, syn-, and posteruption surface deformation and products of Earth’s entire active land volcano inventory at a **time scale of days to weeks***. | <span style="background-color:#ccffcc">Most Important</span> | Topography | High spatial resolution (**5 m**) bare-Earth topography at **1 m vertical accuracy** over all volcanoes | Spacecraft swath-lidar or radar (e.g., ICESat-2) |
| **S-1b.** *Measure and forecast interseismic, preseismic, coseismic, and postseismic activity over tectonically active areas on **time scales ranging from hours to decades***. | <span style="background-color:#ccffcc">Most Important</span> | Topography | High spatial resolution (**1 m**), bare-Earth topography at **0.1 m vertical accuracy** over selected tectonic areas | Aircraft/UAV lidar (e.g., ICESat-2) |
| **S-1c.** *Forecast and monitor landslides, especially those near population centers.* | <span style="background-color:#ffffcc">Very Important</span> | High-resolution topography | Spatial resolution **1–5 m**, vertical **0.5 m** | Aircraft/UAV lidar (e.g., ICESat-2) |
| **S-1d.** *Forecast, model, and measure tsunami generation, propagation, and run-up for major seafloor events.* | <span style="background-color:#ffe5cc">Important</span> | Topography and shallow bathymetry | High spatial resolution (**1 m**), bare-Earth topography at **0.1 m vertical accuracy** over selected tectonic areas | Aircraft/UAV lidar (e.g., ICESat-2) |
| **S-2c.** *Assess co- and postseismic ground deformation (spatial resolution of 100 m and an accuracy of 10 mm) and damage to infrastructure following an earthquake.* | <span style="background-color:#ffffcc">Very Important</span> | Topography | High spatial resolution (**1 m**), bare-Earth topography at **0.1 m vertical accuracy** over selected tectonic areas | Aircraft/UAV lidar (e.g., ICESat-2) |
| **S-3b.** *Determine vertical motion of land along coastlines at uncertainty <1 mm/yr.* | <span style="background-color:#ccffcc">Most Important</span> | Bare-earth topography | Global measurements made **once** to produce high-resolution (**1 m horizontal, 10 cm vertical**) bare-Earth topographic model. Focused regional surveys at comparable resolution used to image landscape change from the globally established baseline. | Aircraft/UAV lidar, UAV SAR; supplement with high-resolution stereo satellite imagery when unobscured (e.g., ICESat-2) |
| **S-4a.** *Quantify global, decadal landscape change produced by abrupt events and by continuous reshaping of Earth’s surface from surface processes, tectonics, and societal activity.* | <span style="background-color:#ccffcc">Most Important</span> | Bare-earth topography | Global measurements made **once** to produce high-resolution (**1 m horizontal, 10 cm vertical**) bare-Earth topographic model. Focused regional surveys at comparable resolution used to image landscape change from the globally established baseline. | Aircraft/UAV lidar, UAV SAR; supplement with high-resolution stereo satellite imagery when unobscured (e.g., ICESat-2) |
| **S-6a.** *Determine the fluid pressures, storage, and flow in confined aquifers at spatial resolution of 100 m and pressure of 1 kPa (0.1 m head).* | <span style="background-color:#ffffcc">Very Important</span> | Topography | Topography at **10 m resolution** | TerraSAR Tandem-X (radar); negotiated data purchase (commercial) |
| **S-6b.** *Measure all significant fluxes in and out of the groundwater system across the recharge area.* | <span style="background-color:#ffe5cc">Important</span> | Topography | Vertical accuracy **10 cm**, resolution **1 m** | SAR, lidar (suborbital), ICESat-2 |
| **S-7a.** *Map topography, surface mineralogic composition, distribution, thermal properties, soil properties/water content, and solar irradiance for improved development and management of energy, mineral, agricultural, and natural resources.* | <span style="background-color:#ffe5cc">Important</span> | Topography | Topographic data at **30 m** postings, **25 cm vertical** | TerraSAR Tandem-X (commercial) |

Most of these objectives focus on Solid Earth and Cryosphere domains, emphasizing high-resolution topographic and elevation measurements, often at meter to sub-meter horizontal scales and decimeter to centimeter vertical accuracy. Temporal sampling varies—from one-time global baselines for landscape models to frequent (weekly to daily) repeat surveys for dynamic processes (e.g., ice-sheet elevation change, volcanic deformation, coastal vertical motion). These requirements drive use of airborne and spaceborne lidar (e.g., ICESat-2, Operation IceBridge, GEDI), SAR (e.g., NISAR, UAV SAR), and complementary optical stereo for unobscured areas. In summary, the community demands:  
- **Horizontal resolution**: typically ~1 m for bare-earth models, 5–30 m for broader surveys, up to 100 m for ice-sheet mapping.  
- **Vertical accuracy**: often 10 cm–1 m for detailed topography; 10–20 cm precision for ice-sheet elevation; 0.5–1 m for landslide and tsunami studies; up to 30 m for bed elevation mapping.  
- **Temporal sampling**: from “once” (global baselines for decadal landscape change) to **weekly to daily** (ice-sheet elevation/velocity, volcanic deformation, coastal motion), and **time scales of days to weeks** (eruption deformation).  
- **Methods**: airborne/UAV lidar, spaceborne lidar (ICESat-2, GEDI), SAR interferometry (NISAR, UAVSAR), radar altimetry, gravity missions for mass change, plus stereo optical when lidar is infeasible.

### 2021 STV Study Team Report

Combined table for Appendix A Preliminary SATM entries

https://science.nasa.gov/wp-content/uploads/2023/06/STV_Study_Report_20210622.pdf

> **Summary:**  
> Most objectives span Solid Earth, Cryosphere, Hydrology, Coastal, Ecosystem, and Cross-cutting applications. They emphasize horizontal resolutions from sub-meter (0.5–5 m) up to hundreds of meters for broad areas; vertical accuracies from centimeters to meters; temporal sampling from one-time baselines to daily/weekly revisits; coverage aspirational ~80–95%; latencies and durations tailored per application; and rate-of-change accuracy for dynamic monitoring. Products are abbreviated (e.g., topo, DTM, bathy, veg_ht, veg3D, ice_height, water_ht, DSM, built_env).

Columns: 
- Code: Objective code (e.g., S-3b, E-2a)
- Obj: Short objective text
- Prod: Products, e.g. topo, DTM, bathy, veg_ht, veg3D, ice_height, water_ht, DSM, built_env
- CovA% / CovT%: Coverage aspirational / threshold (%)
- H_A_m / H_T_m: Horizontal resolution aspirational / threshold (m)
- V3_A_m / V3_T_m: Vegetation 3D aspirational / threshold (m) or “–”
- V_A_m / V_T_m: Vertical resolution aspirational / threshold (m)
- B_A_m / B_T_m: Bathymetry max depth aspirational / threshold (m)
- GL_A_m / GL_T_m: Geolocation accuracy aspirational / threshold (m)
- VA_A_m / VA_T_m: Vertical accuracy aspirational / threshold (m)
- LatA_d / LatT_d: Latency aspirational / threshold (days)
- RepA_d / RepT_d: Repeat frequency aspirational / threshold (days)
- DurA_mo / DurT_mo: Duration for repeating aspirational / threshold (months)
- RChgA_mpy / RChgT_mpy: Rate-of-change accuracy aspirational / threshold (m/yr)

| Code | Obj                                                | Prod                    | CovA% | CovT% | H_A_m | H_T_m | V3_A_m | V3_T_m | V_A_m | V_T_m | B_A_m | B_T_m | GL_A_m | GL_T_m | VA_A_m | VA_T_m | LatA_d | LatT_d | RepA_d | RepT_d | DurA_mo | DurT_mo | RChgA_mpy | RChgT_mpy |
|------|----------------------------------------------------|-------------------------|-------|-------|-------|-------|--------|--------|-------|-------|-------|-------|--------|--------|--------|--------|--------|--------|--------|--------|---------|---------|-----------|-----------|
| S-3b | vertical motion<br>land coast<br><1 mm/yr         | topo/<br>DTM/<br>bathy  | 90    | 65    | 10    | 100   | –      | –      | 25    | 5     | 1     | 3     | 0.05   | 0.2    | 15     | 30     | 15     | 30     | 72     | 36     | 0.01    | 0.1     |
| S-4a | decadal landscape<br>change                       | topo/<br>DTM/<br>veg_ht | 90    | 65    | 1     | 5     | 1      | 3      | 1     | 3     | –     | –     | 0.1    | 0.3    | 15     | 30     | 90     | 180    | 72     | 36     | 0.10    | 0.3     |
| S-7a | map topo &<br>resources                           | topo/<br>DTM             | 75    | 50    | 5     | 20    | –      | –      | –     | –     | –     | –     | 0.1    | 1.0    | 15     | 30     | 90     | 180    | 72     | 36     | 0.30    | 1.0     |
| S-1a | volcano response:<br>lava dome, eruptive mapping  | topo/<br>DTM/<br>bathy  | 90    | 65    | 1     | 3     | –      | –      | 25    | 10    | 1     | 3     | 0.1    | 0.3    | 0.5    | 1      | 1      | 3      | 4      | 2      | –       | –       |
| S-1a | volcano hazards:<br>topo change flows             | topo/<br>DTM/<br>bathy  | 90    | 65    | 1     | 3     | –      | –      | 25    | 10    | 1     | 3     | 0.1    | 0.3    | 7      | 14     | 7      | 14     | 72     | 36     | –       | –       |
| S-2c | eq rupture/post-seismic<br>mapping               | topo/<br>DTM/<br>bathy  | 90    | 65    | 0.5   | 2     | –      | –      | 25    | 10    | 1     | 3     | 0.1    | 0.3    | 0.5    | 2      | 1      | 3      | 4      | 1      | –       | –       |
| S-1b | eq aseismic creep & risk                         | topo/<br>DTM/<br>bathy  | 90    | 65    | 0.5   | 2     | –      | –      | 25    | 10    | 1     | 3     | 0.1    | 0.3    | 7      | 14     | 7      | 14     | 72     | 36     | 0.10    | 0.5     |
| S-1c | landslide monitoring                              | topo/<br>DTM/<br>bathy  | 90    | 65    | 0.5   | 2     | –      | –      | 25    | 10    | 1     | 3     | 0.1    | 0.3    | 1      | 2      | 1      | 14     | 72     | 36     | 0.10    | 0.5     |
| S-3b | coastal subsidence                                | topo/<br>DTM/<br>bathy  | 90    | 65    | 10    | 100   | –      | –      | 25    | 5     | 1     | 3     | 0.05   | 0.2    | 15     | 30     | 15     | 30     | 72     | 36     | 0.01    | 0.1     |
|      | subsidence:<br>resource extraction                | topo/<br>DTM             | 75    | 50    | 5     | 20    | –      | –      | –     | –     | –     | –     | 0.1    | 1.0    | 15     | 30     | 90     | 180    | 72     | 36     | 0.30    | 1.0     |
|      | subsidence:<br>permafrost thaw                    | topo/<br>DTM             | 75    | 50    | 10    | 100   | –      | –      | –     | –     | –     | –     | 0.1    | 1.0    | 15     | 30     | 90     | 180    | 72     | 36     | 0.30    | 1.0     |
|      | mining ground movement                            | topo/<br>DTM             | 75    | 50    | 3     | 5     | –      | –      | –     | –     | –     | –     | 0.1    | 1.0    | 15     | 30     | 15     | 30     | 72     | 36     | 0.10    | 0.5     |
|      | sinkhole/cavern collapse                          | topo/<br>DTM             | 90    | 65    | 1     | 5     | –      | –      | –     | –     | –     | –     | 0.1    | 0.3    | 7      | 14     | 7      | 14     | 72     | 36     | 0.10    | 0.5     |
|      | space archaeology                                 | topo/<br>DTM             | 90    | 65    | 1     | 5     | –      | –      | –     | –     | –     | –     | 0.1    | 0.3    | 15     | 30     | –      | –      | –      | –      | –       | –       |
| E-2a | ecosystem C flux/<br>biomass dynamics             | veg_ht/<br>veg3D         | 80    | 50    | 50    | 100   | 1      | 2      | 1     | 3     | –     | –     | 1.00   | 2.0    | 5      | 30     | 90     | 180    | 72     | 36     | 1.0     | 2       |
|      | boreal/savanna climate impact<br>on veg structure | veg_ht/<br>veg3D         | 95    | 75    | 10    | 30    | 0.5    | 2      | –     | –     | –     | –     | 1.0    | 2.0    | 30     | 365    | –      | –      | –      | –      | –       | –       |
| E-1  | ecosystem structure &<br>biodiversity             | topo/<br>DTM/<br>veg_ht/<br>veg3D | 80 | 50 | 30 | 50 | 1 | 2 | 1.00 | 1.5 | – | – | – | – | – | – | – | – | – | – | – | – | 0.5 | 1.0 |
| S-3a | sea-level change<br>(mass balance)               | ice_height<br>(gridded) | 95    | 80    | 10    | 50    | –      | –      | –     | –     | –     | –     | 2      | 5      | 30     | 90     | 1      | 5      | 120    | 36     | 0.05    | 0.10    |
|      | fast glacier<br>(>50 m/yr)                       | ice_height<br>(gridded) | 95    | 80    | 10    | 50    | –      | –      | –     | –     | –     | –     | 2      | 5      | 30     | 90     | 5      | 10     | 120    | 36     | 0.05    | 0.10    |
|      | slow glacier<br>(<50 m/yr)                       | ice_height<br>(gridded) | 80    | 50    | 200   | 500   | –      | –      | –     | –     | –     | –     | 2      | 5      | 30     | 90     | 30     | 90     | 120    | 36     | 0.01    | 0.01    |
|      | Antarctic/Greenland<br>ice shelf                 | ice_height<br>(gridded) | 95    | 75    | 10    | 50    | –      | –      | –     | –     | –     | –     | 2      | 5      | 30     | 90     | 5      | 10     | 120    | 36     | 0.01    | 0.01    |
|      | mountain glaciers<br>(>10 km²)                   | ice_height<br>(gridded) | 95    | 50    | 10    | 25    | –      | –      | –     | –     | –     | –     | 2      | 5      | 30     | 90     | 5      | 10     | 120    | 36     | 0.05    | 0.10    |
|      | high-res DEM<br>for ice-sheet init               | ice_height/<br>DSM      | 95    | 90    | 1     | 5     | –      | –      | –     | –     | –     | –     | 2      | 5      | 0.50   | 1.00   | 30     | 90     | –      | –      | –       | –       |
| C-8  | sea-ice thickness                                 | seaice_thick            | 95    | 90    | 10    | 25    | –      | –      | –     | –     | –     | –     | 3      | 6      | 0.30   | 0.40   | 5      | 30     | 5      | 30     | 120     | 36     | –       | –       |
| C-8  | snow depth<br>on sea ice                         | snowsea_depth           | 95    | 90    | 10    | 25    | –      | –      | –     | –     | –     | –     | 3      | 6      | 0.03   | 0.05   | 5      | 30     | 5      | 30     | 120     | 36     | –       | –       |
|      | water cycle &<br>freshwater avail                | topo/<br>DTM/<br>DSM    | 95    | 75    | 3     | 5     | –      | –      | –     | –     | –     | –     | 1      | 2      | 365    | 1825   | 60     | 24     | –      | –      | 0.1     | 0.5     |
|      | veg3D for<br>water/energy cycle                  | veg3D                   | 95    | 75    | 10    | 30    | 0.5    | 2      | –     | –     | –     | –     | 5      | 7      | 1      | 2      | 30     | 365    | 60     | 24     | –       | –       |
|      | shallow-water<br>bathy for water balance         | bathy/<br>DTM           | 95    | 75    | 1     | 10    | –      | –      | –     | –     | 0.1   | 0.25  | 365    | 1825   | 60     | 24     | –      | –      | –      | –      | –       | –       |
|      | snow depth<br>(DSM–DTM)                         | snow_depth              | 95    | 75    | 100   | 10    | –      | –      | –     | –     | 50    | 5     | 1      | 2      | 365    | 1825   | 60     | 24     | –      | –      | –       | –       |
|      | lake/reservoir<br>balances                      | water_ht/<br>DTM/<br>bathy | 95 | 75 | 1     | 10    | –      | –      | 0.05  | 0.2   | –     | –     | 30     | 365    | 60     | 24     | –      | –      | –      | –      | 0.1     | 0.5     |
|      | freshwater &<br>biogeochem processes            | water_ht/<br>DTM/<br>bathy | 95 | 75 | 1     | 30    | –      | –      | 0.05  | 0.2   | –     | –     | 30     | 365    | 60     | 24     | –      | –      | –      | –      | 0.1     | 0.5     |
|      | ecosystem fluxes<br>(wetlands etc.)             | water_ht/<br>bathy/<br>veg3D | 95 | 50 | 10    | 30    | 0.5    | 1      | 0.05  | 0.2   | –     | –     | 7      | 14     | 60     | 24     | –      | –      | –      | –      | 0.1     | 0.5     |
|      | land-use/water-use<br>impacts                   | topo/<br>DTM/<br>bathy/<br>veg3D | 95 | 50 | 3 | 5  | 10    | 30    | 0.5   | 2     | 0.1   | 0.25  | 365    | 1825   | 60     | 24     | –      | –      | –      | –      | –       | –       |
|      | snow in catchments<br>DSM–DTM                   | topo/<br>DTM/<br>snow_depth | 95 | 50 | 3 | 5 | –      | –      | –     | –     | 50    | 500   | 1      | 2      | 365    | 1825   | 60     | 24     | –      | –      | –       | –       |
|      | water cycle ↔ hazards                           | topo/<br>DTM/<br>bathy/<br>veg3D/<br>snow_depth | 95 | 50 | 3 | 5 | 10 | 30 | 0.5 | 2 | 0.1 | 0.25 | 365 | 1825 | 60 | 24 | – | – | – | – | – | – |
|      | cold-region hydro/<br>permafrost response       | veg_ht/<br>topo/<br>DTM/<br>bathy/<br>snow_depth/<br>water_ht | 95 | 50 | 10 | 30 | 1 | 2 | 0.1 | 0.2 | 0.1 | 0.25 | 365 | 48 | 24 | – | 0.1 | 0.5 | – | – | – | – |
|      | coastal hazards & fluxes<br>(land-sea continuum)| topo/<br>bathy            | 80    | 60    | 5     | 15    | –      | –      | 0.2   | 0.3   | 25    | 10    | 2      | 5      | 0.25   | 0.50   | 30     | 30     | 45     | 365    | 90      | 40      | 0.20    | 0.40    |
|      | coastal eco/<br>biodiversity change             | topo/<br>bathy/<br>veg_ht  | 75    | 50    | 3     | 5     | –      | –      | 0.1   | 0.2   | 25    | 10    | 1      | 3      | 0.10   | 0.20   | 30     | 30     | 30     | 150    | 90      | 40      | 0.20    | 0.40    |
|      | coastal junction<br>fluxes                     | topo/<br>bathy/<br>veg_ht  | 95    | 80    | 1     | 5     | –      | –      | 0.20  | 0.50  | –     | –     | 30     | 150    | 90     | 40     | –      | –      | –      | –      | –       | –       | 0.20    | 0.40    |
|      | coastal hazards & sediment<br>transport         | topo/<br>bathy            | 95    | 80    | 1     | 5     | –      | –      | 0.20  | 0.50  | –     | –     | 30     | 150    | 90     | 40     | –      | –      | –      | –      | –       | –       | 0.20    | 0.40    |
|      | shoals/reefs nav<br>hazards                     | topo                     | 95    | 80    | 2     | 5     | –      | –      | 0.3   | 0.5   | 20    | 10    | 2      | 5      | 0.25   | 0.50   | 30     | 30     | 30     | 150    | 90      | 40      | 0.20    | 0.40    |
|      | flood cond & risk                               | topo/<br>DTM/<br>water_ht/<br>veg_ht/<br>veg3D | 90 | 75 | 5 | 30 | – | – | 1 | 3 | – | – | 0.1 | 0.5 | 1 | 3 | 1 | 3 | 2 | 1 | – | – | – | – |
|      | flood forecast                                  | topo/<br>DTM/<br>water_ht/<br>veg_ht/<br>veg3D | 80 | 50 | 10 | 30 | – | – | 1 | 3 | – | – | 0.1 | 0.5 | 3 | 14 | 7 | 14 | 12 | 6 | – | – | – | – |
|      | flood & subsidence/<br>coastal interaction      | topo/<br>DTM/<br>water_ht/<br>veg_ht/<br>veg3D | 80 | 25 | 10 | 50 | 20 | 10 | 1 | 2 | – | – | 0.1 | 0.5 | 30 | 90 | 15 | 30 | 72 | 36 | – | – | – | – |
|      | wildfire risk & spread                          | topo/<br>DTM/<br>veg_ht/<br>veg3D | 80 | 50 | 10 | 100 | 20 | 10 | 1 | 2 | – | – | 0.5 | 1.5 | 1 | 3 | 1 | 3 | 6 | 1 | – | – | – | – |
|      | burn severity/<br>debris-flow risk              | topo/<br>DTM/<br>veg_ht/<br>veg3D | 80 | 50 | 10 | 100 | 20 | 10 | 1 | 2 | – | – | 1.0 | 1.5 | 7 | 14 | 7 | 30 | 6 | 1 | – | – | – | – |
|      | veg structure<br>vs fire risk                   | topo/<br>DTM/<br>veg_ht/<br>veg3D | 80 | 50 | 30 | 100 | 20 | 10 | 1 | 2 | – | – | 1.0 | 1.5 | 7 | 30 | 90 | 365 | 72 | 36 | 0.5 | 1.0 |
|      | fire regime impact<br>on biomass                | topo/<br>DTM/<br>veg_ht/<br>veg3D | 80 | 50 | 30 | 100 | 20 | 10 | 1 | 2 | – | – | 1.0 | 1.5 | 7 | 30 | 90 | 365 | 72 | 36 | 0.5 | 1.0 |
|      | geohazard damage<br>assessment                  | topo/<br>DTM/<br>DSM/<br>built_env/<br>water_ht | 80 | 25 | 3 | 20 | – | – | – | – | – | – | 0.05 | 0.5 | 1 | 7 | 2 | 1 | – | – | – | – | 0.1 | 0.5 |
|      | cascading hazard<br>interrel’ships              | topo/<br>DTM/<br>DSM/<br>built_env/<br>water_ht | 80 | 25 | 3 | 20 | – | – | – | – | – | – | 0.10 | 0.5 | 14 | 60 | 15 | 90 | 72 | 36 | 0.1 | 0.5 |
|      | critical infra<br>monitoring                    | topo/<br>DTM/<br>DSM/<br>veg_ht/<br>built_env/<br>water_ht | 80 | 25 | 3 | 20 | 20 | 10 | 1 | 2 | – | – | 0.05 | 0.2 | 14 | 60 | 15 | 90 | 72 | 36 | 0.01 | 0.10 |
|      | crop health &<br>yield estimation                | topo/<br>DTM/<br>veg_ht/<br>veg3D | 80 | 25 | 10 | 30 | 20 | 10 | 0.5 | 1 | – | – | 0.25 | 1.0 | 7 | 7 | 5 | 14 | 72 | 36 | – | – |
|      | commercial forestry<br>monitoring               | veg_ht/<br>veg3D           | 80    | 25    | 1     | 20    | 20     | 10     | 0.5   | 1   | –     | –     | 0.25   | 0.5    | 7      | 10     | 30     | 90     | 72     | 36     | 0.25    | 1.0     |
|      | deforestation alerting/<br>REDD+ info            | veg_ht/<br>veg3D           | 80    | 50    | 10    | 30    | 20     | 10     | 1     | 2   | –     | –     | 1.0    | 1.5    | 3      | 5      | 3      | 10     | 72     | 36     | –       | –       |
|      | REDD+ emissions<br>estimation                   | veg_ht/<br>veg3D           | 80    | 50    | 30    | 50    | 20     | 10     | 1     | 2   | –     | –     | 1.0    | 1.5    | 7      | 30     | 90     | 365    | 72     | 36     | –       | –       |
|      | maritime ice hazards                            | DSM/<br>water_ht           | 80    | 50    | 10    | 50    | –      | –      | –     | –     | –     | –     | 0.50   | 3.0    | 1      | 7      | 8      | 4      | –      | –      | –       | –       |
|      | coastal resiliency                              | topo/<br>DTM/<br>DSM/<br>veg_ht/<br>veg3D/<br>built_env/<br>bathy/<br>water_ht | 80 | 20 | 5 | 20 | 20 | 10 | 1 | 2 | – | – | 0.05 | 0.5 | 30 | 90 | 15 | 30 | 120 | 36 | 0.1 | 0.5 |


---
