# Germanwings Customer Review Analysis
#### Analysis by Evan Yathon

## Overview



## Scripts

Scripts are in the form of python scripts or jupyter notebooks to be ran with [papermill](https://github.com/nteract/papermill), run from the command line and root of the project.  They are presented in the order in which they should be ran.

Reproducibility was one of the qualities that I wanted to emphasize.  If another person runs my analysis as outlined below with the sample usages and matches the requirements file, they should end up with the same results.

### Scraping

When looking at the [original data](data/given_4U_reviews.txt) I noticed that the categories such as 'seat comfort' or 'ground service' were populated with only the value `12345`.  I searched some of the customer reviews and found that the data had come from [www.airlinequality.com](www.airlinequality.com), and saw that these categories should have a single star rating out of 5.  I decided that I would likely have a more comprehensive dataset to play with if these categories were correctly filled, and thus decided to scrape the website for Germanwings reviews.

While the script is built specifically for Germanwings, it could easily be extended to any other airline on the same website with a few tweaks.  If I had more time I would modify it to be modular, but in the interest of time kept it specific to this task.

Note that sleep time is the time to wait between traversal of each page, in order to be polite to the website and not overload it with requests.

Parameters:
`python src/scrape_reviews.py data_save_path sleep_time`

Sample usage:

```
python src/scrape_reviews.py data/scraped_gw_reviews.csv 5
```

Location of the [saved data](data/cleaned_gw_reviews.csv)

### [Verify and Clean](src/verify_and_clean_ran.ipynb)

Verify and Clean is a notebook to be ran with [papermill](https://github.com/nteract/papermill).  Two reasons it is ran with papermill:
1. To be able to view outputs in a nice format
2. Contain markdown formatting for an explanation of logic and code

While I scraped all of the data from before, I wanted to verify that I wasn't missing any reviews in the [original dataset](data/given_4U_reviews.txt).  This notebook verifies that and also does a bit of cleaning and exploration of the data.

Sample usage:

`papermill src/ipynbs/verify_and_clean.ipynb src/verify_and_clean_ran.ipynb -p load_path data/scraped_gw_reviews.csv -p save_path data/cleaned_gw_reviews.csv -p old_data_path data/given_4U_reviews.txt`

### [EDA](src/EDA_ran.ipynb)

EDA is a notebook to be ran with [papermill](https://github.com/nteract/papermill).  It was chosen to be ran with `papermill` to view the plots in sequential order with markdown syntax helping explain each visualization.

The purpose of the EDA notebook is to explore the previously cleaned data. This is done mainly through plots in order to get an idea of what to expect and any pitfalls that can be anticipated.

Sample Usage:
`papermill src/ipynbs/EDA.ipynb src/EDA_ran.ipynb -p load_path data/cleaned_gw_reviews.csv`

### Dependencies

Dependencies live in the [requirements file](requirements.txt).
