# IRP xm324: From Efficacy to Prediction: A Machine Learning Framework for Forecasting User Engagement in Automated Demand Response

## Introduction

This repository supports the XM324 Individual Research Project at Imperial College London. 
 
It provides preprocessing workflows for **weather data (ERA5, open access)** and **smart-switch trial data (restricted)** collected in Delhi and Mumbai.  

The aim is to produce **clean, feature-rich datasets** that enable modeling of household electricity use, override behavior, and event-level energy savings. 

By integrating environmental and power data at half-hourly resolution, the project builds a foundation for machine learning models that support **demand response analysis** and the development of **Virtual Power Plants (VPPs)**.

---

## Repository Structure

```
code/
    powbal_dataset_preprocess.ipynb      # Main file for preprocessing, clustering, and model training
    weather_dataset_preprocess.ipynb     # Cleans and engineers weather datasets
    weather_grid_to_csv.ipynb            # Converts ERA5 GRIB weather files to CSV
plot/                                    # The Figure and table in report
    Figure 1 to 3, etc.                  # Plots that shown in report
 
deliverables/
    xm324-final-report.pdf               # Final project report
    xm324-project-plan.pdf               # Project plan
    README.md                            # Deliverables documentation
logbook/
    logbook.md                           # Project logbook and progress notes
    README.md                            # Logbook documentation
title/
    README.md                            # Project title and metadata
    title.toml                           # Project metadata in TOML format
.github/
    workflows/                           # GitHub Actions for CI and documentation
requirements.txt                         # Python package requirements for running notebooks
LICENSE                                  # MIT License for code and documentation
README.md                                # Main project README

```
## Workflow Overview

### 1. Weather Data Conversion (`weather_grid_to_csv.ipynb`)
- Converts ERA5 GRIB weather files (2023–2024) for Delhi and Mumbai into CSV format.  
- Extracts key variables (temperature, cloud cover, solar radiation, wind, precipitation).  
- Merges variables into a single DataFrame per city/year, handling missing or corrupted files.

### 2. Weather Data Preprocessing (`weather_dataset_preprocess.ipynb`)
- Integrates ERA5 CSVs with internal station datasets.  
- Applies unit conversions (e.g., Kelvin → Celsius, wind vectors → speed/direction).  
- Imputes missing values and removes highly correlated variables.  
- Performs spatial interpolation to align ERA5 grid points with customer locations.  
- Resamples to half-hourly intervals to produce a consistent dataset.

### 3. Power Data Preprocessing (`powbal_dataset_preprocess.ipynb`)
- **Main notebook for smart-switch trial data** (`powbal_clean`, `power-data`).  
- Cleans and integrates power data with customer metadata and weather features.  
- Engineers event-level variables (switch-off events, rewards, durations, energy measures).  
- Handles structurally missing values using zero/mode/median imputation.  
- Encodes cyclical time features and compresses sequential event indicators.  
- Applies PCA and clustering for customer segmentation.  
- Outputs leak-safe and full-feature datasets for machine learning (override prediction, energy savings).

---

## Dataset Access

- **Weather Data:**  
  The weather dataset (ERA5) used in this project is open-access and can be downloaded from the [Copernicus Climate Data Store](https://cds.climate.copernicus.eu/).  
  - ERA5 weather data is originally provided in `.grib` format.  
  - These `.grib` files are converted to `.csv` format using the `code/weather_grid_to_csv.ipynb` notebook for easier processing and analysis.  
  Please review and comply with the [ERA5 data license](https://cds.climate.copernicus.eu/cdsapp#!/terms/licence).

- **Power Data (`powbal_clean`, `power-data` files):**  
  These datasets are proprietary and not publicly available. They are provided to project members only and are not distributed in this repository.  
  If you wish to access the Power Data, please contact the **supervisor of this project** for further guidance.

---

## Deliverables

- **xm324-final-report.pdf**: Final report detailing methodology, results, and conclusions.
- **xm324-project-plan.pdf**: Project planning document.
- **Processed datasets**: Cleaned CSV files ready for analysis (see `../power-data/` after running notebooks).
- **Logbook**: Ongoing project notes and progress (`logbook/logbook.md`).

---

## How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/mikebo250/academic-project.git
   cd academic-project
   ```

2. **Install dependencies**  
   Install all required Python packages:
   ```bash
   pip install -r requirements.txt
   ```

3. **Prepare datasets**
   - Download ERA5 GRIB weather files from the [Copernicus Climate Data Store](https://cds.climate.copernicus.eu/).
   - Place them inside the `../power-data/` folder (relative to the notebooks).

4. **Run preprocessing notebooks**
   - Open the following notebooks in Jupyter Notebook or JupyterLab, and run all cells in order:
     - `code/weather_grid_to_csv.ipynb` → Convert ERA5 GRIB files to CSV.
     - `code/weather_dataset_preprocess.ipynb` → Clean and engineer the weather dataset.
     - `code/powbal_dataset_preprocess.ipynb` Clean and preprocess the power balance dataset, model training (main file)
   - **Update file loading paths as necessary** to match your local environment.

5. **Outputs**
   - Processed weather datasets are saved in `../power-data/` (e.g., `weather_full.csv`).
   - Processed power datasets are saved as cleaned CSV files (e.g., `smart_switch_data_cleaned.csv`).
   - These outputs are ready for downstream machine learning and analysis.

> **Note:** Make sure your computer has enough memory to process large
---

## Notes

> ⚠️ **Note:**  
> The Jupyter notebooks (`.ipynb` files) were originally developed in Google Colab.  
If you wish to run them in a different environment, please install the required packages listed in `requirements.txt` and update file loading paths as necessary.
- All code is written in Python and designed for use in Jupyter Notebooks.
- See individual notebook headers for detailed workflow steps and explanations.
- For questions or issues, refer to the logbook or contact Xiangbo Mai (mikebomai250@gmail.com).

---

## License

- **Code and documentation**: Released under the MIT License (see [LICENSE](LICENSE)).  
- **Weather data**: Openly available from the [Copernicus Climate Change Service (ERA5)](https://cds.climate.copernicus.eu/).  
- **Power data**: Proprietary and not shared in this repository. For access requests, please contact the project supervisor.

---

## Acknowledgements

I would like to thank my supervisors — Dr. Mirabelle Muûls, Dr. Jorge Avalos Patino, and Dr. Shefali Khanna — for their guidance and feedback throughout this project. I also acknowledge the Department of Earth Science and Engineering at Imperial College London for providing the resources and support that made this work possible.  

Weather data were provided by the Copernicus Climate Change Service (C3S, ERA5), and smart-switch trial data originate from the POWBAL randomized control trial (Khanna, Martin, & Muûls, 2025).  

### AI Acknowledgement
I used **OpenAI’s ChatGPT-4o** (https://chat.openai.com/) and **Google Gemini 2.5 Pro** (https://gemini.google.com/app) to assist with debugging Python code and improving the clarity of written text. These generative AI tools supported my learning process, but the submitted work is my own and reflects my own understanding and effort, as I have declared in the Academic Integrity Declaration.

---

*This project is part of the xm324 Individual Research Project at Imperial College London.*