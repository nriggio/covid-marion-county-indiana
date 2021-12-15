# COVID-19 in Marion County, IN
Data 512: A4-7 Final Project

<!-- ABOUT THE PROJECT -->
## About the Project:
The goal of this assignment is to explore the impact of COVID-19 in Marion County, IN by first investigating how masking policies changed the progression of confirmed COVID-19 cases from February 1, 2020 - October 15, 2021 before expanding on this to see how COVID-19 deaths and vaccinations were impacted by hospital occupancy.

- __A4: Common Analysis:__ base analysis regarding how masking policies influenced the spread of COVID-19
- __A5: Extension Plan:__ proposal of a human-centered data science question that extends the work in A4
- __A6: Presentation:__ PechaKucha-style presentation of this continued analysis
- __A7: Final Report:__ reproducible github repository & final report detailing this analysis

<!-- PREREQUISITES -->
## Prerequisites:

* python3
* pandas
* numpy
* matplotlib
* statsmodels
* scipy
* sklearn

<!-- PROJECT STRUCTURE -->
## Project Structure:

Any data is stored in the `data` directory (see Data header below for description), analysis is done in a jupyter notebook (`marion-county-COVID`), the timeseries plot for A4 is stored in `infection_rate`, any commentary on A4 is stored in `A4 - Reflection Statement` or `A4 - Visualization Explanation`, the extension plan for A5 is in `A5 - Extension Plan`, the PechaKucha style presentation for A6 is in `A6 - Presentation`, and the final report is in `A7 - Final Report`.
```
.
├── LICENSE
├── README.md
├── data
│   ├── kaggle
│     ├── RAW_us_confirmed_cases.csv
│     ├── RAW_us_deaths.csv
│   ├── U.S._State_and_Territorial_Public_Mask_Mandates_From_April_10__2020_through_August_15__2021_by_County_by_Day.zip
│   ├── mask-use-by-county.csv
│   ├── hospitalizations.csv
│   ├── covid_report_bedvent_date.csv
│   ├── county-vaccinations-by-date.csv
├── marion-county-COVID.ipynb
├── infection_rate.png
├── A4 - Reflection Statement.pdf
├── A4 - Visualization Explanation.pdf
├── A5 - Extension Plan.pdf
├── A6 - Presentation.pdf
└── A7 - Project Report.pdf
```


<!-- SPECIAL CONSIDERATIONS -->
## Special Considerations:

Any special considerations regarding the dataset or simplfying assumptions made for the analysis are detailed in the `notes` in the __Data__ section or in the analysis itself (marion-county-COVID.ipynb).

<!-- DATA -->
## Data:

The data is contained in 7 CSV files formatted as follows:

* Filename: `RAW_us_confirmed_cases.csv` & `RAW_us_deaths.csv`
* Source: https://www.kaggle.com/antgoldbloom/covid19-data-from-john-hopkins-university
* Data Structure:

| Column         | Description                                              |
|----------------|----------------------------------------------------------|
| Province_State | U.S. state name                                          |
| Admin2         | U.S. county name                                         |
| UID            |                                                          |
| iso2           | 2-digit country code                                     |
| iso3           | 3-digit country code                                     |
| code3          | 3-digit area code                                        |
| FIPS           | County FIPS code                                         |
| Country_Region | country name                                             |
| Lat            | Latitude                                                 |
| Long_          | Longitude                                                |
| Combined_Key   | County, State, Country                                   |
| Date           | One column per date from 1/22/20 - today (updated daily) |

* Filename: `U.S._State_and_Territorial_Public_Mask_Mandates_From_April_10__2020_through_August_15__2021_by_County_by_Day.zip`
* Source: https://data.cdc.gov/Policy-Surveillance/U-S-State-and-Territorial-Public-Mask-Mandates-Fro/62d6-pm5i
* Data Structure: note that `public masking` is defined as a requirement for individuals operating in a personal capacity to wear masks 1) anywhere outside their homes or 2) both in retail businesses and in restaurants/food establishments. This file is stored in a ZIP & must be extracted to view.

| Column                        | Description                                    |
|-------------------------------|------------------------------------------------|
| State_Tribe_Territory         | U.S. state, tribe, and territory names         |
| County_Name                   | U.S. county names                              |
| FIPS_State                    | U.S. state FIPS codes                          |
| FIPS_County                   | U.S. county FIPS codes                         |
| date                          |                                                |
| order_code                    |                                                |
| Face_Masks_Required_in_Public | Are masks required in public?                  |
| Source_of_Action              | Source where order was found                   |
| URL                           | URL of order language used to complete dataset |
| Citation                      | Citation for the order                         |

* Filename: `mask-use-by-county.csv`
* Source: https://github.com/nytimes/covid-19-data/tree/master/mask-use
* Brief Description: each column represents an answer to the question “How often do you wear a mask in public when you expect to be within six feet of another person?”

* Filename: `hospitalizations.csv`
* Source: https://marionhealth.org/coviddashboard/DR4417-COVID-Public-Information-Dashboard.html
* Brief Description: this is a 2-column dataset with the date & 7-day rolling average COVID-19 hospitalizations in Marion County, IN and was extracted from the dashboard using WebPlotDigitizer. 

* Filename: `covid_report_bedvent_date.csv`
* Source: https://hub.mph.in.gov/dataset/covid-19-bed-and-vent-usage-by-day
* Data Structure:

| Column                                   | Description                                                       |
|------------------------------------------|-------------------------------------------------------------------|
| DATE                                     |                                                                   |
| BEDS_ICU_TOTAL                           | Number of ICU beds in total.                                      |
| BEDS_ICU_OCCUPIED_COVID_19               | Number of ICU beds occupied by COVID-19 patients.                 |
| BEDS_ICU_NO_OCCUPIED_COVID_19            | Number of ICU beds occupied by Non-COVID-19 patients.             |
| BEDS_AVAILABLE_ICU_BEDS_TOTAL            | Number of ICU beds remaining available.                           |
| VENTS_TOTAL                              | Number of ICU ventilators in total.                               |
| VENTS_ALL_USE_COVID_19                   | Number of ICU ventilators occupied by COVID-19 patients.          |
| VENTS_NON_COVID_PTS_ON_VENTS             | Number of ICU ventilators occupied by Non-COVID-19 patients.      |
| VENTS_ALL_AVAILABLE_VENTS_NOT_IN_USE     | Number of ICU ventilators remaining available.                    |
| PCT_BEDS_ICU_OCCUPIED_COVID_19           | Percentage of ICU beds occupied by COVID-19 patients.             |
| PCT_BEDS_ICU_NO_OCCUPIED_COVID_19        | Percentage of ICU beds occupied by Non-COVID-19 patients.         |
| PCT_BEDS_AVAILABLE_ICU_BEDS_TOTAL        | Percentage of ICU beds remaining available.                       |
| PCT_VENTS_ALL_USE_COVID_19               | Percentage of ICU ventilators occupied by COVID-19 patients.      |
| PCT_VENTS_NON_COVID_PTS_ON_VENTS         | Percentage of ICU ventilators occupied by Non-COVID-19 patients.  |
| PCT_VENTS_ALL_AVAILABLE_VENTS_NOT_IN_USE | Percentage of ICU ventilators remaining available.                |

* Filename: `county-vaccinations-by-date.csv`
* Source: https://hub.mph.in.gov/dataset/covid-19-vaccinations-by-date
* Data Structure: any values <5 are suppressed

| Column                        | Description                                                                                       |
|-------------------------------|---------------------------------------------------------------------------------------------------|
| date                          |                                                                                                   |
| county                        |                                                                                                   |
| region                        | ISDH Health District ID                                                                           |
| fips                          | County FIPS code                                                                                  |
| first_dose_administered       | Count of individuals who received their first dose of the COVID-19 vaccine                        |
| second_dose_administered      | Count of individuals who received their second dose of the COVID-19 vaccine                       |
| single_dose_administered      | Count of individuals who received a single dose COVID-19 vaccine                                  |
| all_doses_administered        | Total number of doses administered                                                                |
| fully_vaccinated              | Total number of individuals now considered fully vaccinated                                       |
| booster_dose_administered     | Count of individuals who received a booster dose of the COVID-19 vaccine                          |
| new_first_dose_administered   | During the previous 24 hours, number of individuals who received their first dose                 |
| new_second_dose_administered  | During the previous 24 hours, number of individuals who received their second dose                |
| new_single_dose_administered  | During the previous 24 hours, number of individuals who received a single dose COVID-19 vaccine   |
| new_all_doses_administered    | During the previous 24 hours, total number of doses administered                                  |
| new_fully_vaccinated          | During the previous 24 hours, total number of individuals who are considered fully vaccinated     |
| new_booster_dose_administered | During the previous 24 hours, number of individuals who received a booster dose                   |
| current_as_of                 | Date and time the data was reported to ISDH                                                       |

<!-- LICENSE -->
## License:

Distributed under the MIT License. See `LICENSE.txt` for more information.


<!-- CONTACT -->
## Contact:

Nicole Riggio - riggionicole@gmail.com

Project Link: [https://github.com/nriggio/data-512-project](https://github.com/nriggio/data-512-project)


<!-- ACKNOWLEDGMENTS -->
## Acknowledgements:

* [A4: Common Analysis](https://docs.google.com/document/d/1q8A0lUeM24cw2AiuQWVlrD4A7MglsPiD1qJclzMl_Bw/edit#)
* [A5: Extension Plan](https://docs.google.com/document/d/1mo8fm0MW_TUk_s7BrHpnFbijpn9vh454SIvynlDCY-A/edit)
* [A6: Project Presentation](https://docs.google.com/document/d/1ljmqpDu7gnsZVaPkrDrxjs3IzIxvjXEr_W0J8ZQ8hY4/edit)
* [A7: Project Report](https://docs.google.com/document/d/1nT1V8I-RLQN3ZxCjpF6Mse9w7-dP1_s1nnW7MfIevgk/edit)
* [Kaggle: RAW_us_confirmed_cases.csv via JHU](https://www.kaggle.com/antgoldbloom/covid19-data-from-john-hopkins-university?select=RAW_us_confirmed_cases.csv)
* [CDC: Mask Mandates by County](https://data.cdc.gov/Policy-Surveillance/U-S-State-and-Territorial-Public-Mask-Mandates-Fro/62d6-pm5i)
* [NYTimes: Mask Compliance](https://github.com/nytimes/covid-19-data/tree/master/mask-use)
* [Marion County COVID-19 Dashboard](https://marionhealth.org/coviddashboard/DR4417-COVID-Public-Information-Dashboard.html)
* [WebPlotDigitizer](https://automeris.io/WebPlotDigitizer/)
* [Kaggle: RAW_us_deaths.csv via JHU](https://www.kaggle.com/antgoldbloom/covid19-data-from-john-hopkins-university?select=RAW_us_deaths.csv)
* [Augmented Dickey-Fuller Test](https://www.machinelearningplus.com/time-series/time-series-analysis-python/)
* [StatsModels ADF Documentation](https://www.statsmodels.org/dev/generated/statsmodels.tsa.stattools.adfuller.html)
* [Stationarity in Time Series](https://machinelearningmastery.com/time-series-data-stationary-python/)
* [Pearson R & Time-Lagged Cross Correlation](https://towardsdatascience.com/four-ways-to-quantify-synchrony-between-time-series-data-b99136c4a9c9)
* [Wikipedia: Case Fatality Ratio](https://en.wikipedia.org/wiki/Case_fatality_rate)
* [Challenges in COVID-19 Case Fatality Ratio Calculation](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7569625/)
* [IndyStar: Indiana Vaccine Eligibility](https://www.indystar.com/story/news/health/2021/03/23/indiana-vaccine-plan-hoosiers-over-16-eligible-vaccines-march-31/4726997001/)
* [IDOH: COVID-19 Bed & Vent Usage by Day](https://hub.mph.in.gov/dataset/covid-19-bed-and-vent-usage-by-day)
* [Statesman Journal: Hospital Capacity by County](https://data.statesmanjournal.com/covid-19-hospital-capacity/facility/indiana-university-health/150056/)
* [CNN: Rationing Healthcare Explainer](https://www.cnn.com/2021/09/13/health/rationing-care-hospital-beds-staff-explainer-wellness/index.html)
* [USNews: Indiana Hospitals at Capacity](https://www.usnews.com/news/best-states/indiana/articles/2021-09-08/covid-19-patients-strain-indiana-hospitals-as-virus-surges)
* [WTHR: Marion County Hospitals on Diversion](https://www.wthr.com/article/news/verify/yes-many-indianapolis-area-hospitals-have-been-turning-away-ambulances-because-their-ers-and-icus-are-too-full-verify/531-28e2216c-dc3f-4b4d-ae3c-f02f30634439)
* [MIT License](https://opensource.org/licenses/MIT)
* [IDOH: COVID-19 Vaccinations by County by Date](https://hub.mph.in.gov/dataset/covid-19-vaccinations-by-date)
* [USNews: Indiana Governor Stymies Vaccine Mandates](https://www.usnews.com/news/best-states/indiana/articles/2021-11-22/indiana-gop-bill-stymies-workplace-covid-19-vaccine-mandates)
* [Wikipedia: PechaKucha](https://en.wikipedia.org/wiki/PechaKucha)
