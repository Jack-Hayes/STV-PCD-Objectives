# :airplane: :rocket: :alien: STV-PCD-Objectives :alien: :rocket: :airplane:

## Index
- [What have people done already](#what-have-people-done-already)
  - [In-House UW Shean Lab](#in-house-uw-shean-lab)
  - [NASA ASP](#nasa-asp)
  - [Pietro Milillo's Lab (UH)](#pietro-milillos-lab-uh)
  - [Similar work external to STV](#similar-work-external-to-stv)
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
*(Content to be added)*

---
