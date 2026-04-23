
# Exploration of Customer Lunacy Across Moon Phases
## ISA 401 Final Project

This repository contains the work for my final project for ISA 401, a data visualization and business intelligence course at Miami University.

---

## Project Setting

Back in high school, I worked as a server at a family-owned restaurant. There were several nights when my coworkers and I noticed that our tables felt a little more unpredictable than usual. One of my coworkers, Sonya, would always say, “It must be a full moon tonight.” Out of curiosity, I started checking, and surprisingly she was sometimes right.

That experience stuck with me. For this project, I wanted to revisit that idea and explore it more systematically. Specifically, I set out to determine whether there is any measurable relationship between lunar phases and customer behavior.

---

## Data Sources

To analyze customer sentiment, I needed a reliable source of restaurant reviews. I initially explored scraping platforms such as Google Reviews, OpenTable, and TripAdvisor, but ran into limitations related to access, structure, and scraping restrictions. Instead, I used the Yelp Open Review and Business Datasets, which are designed for academic use. These datasets provide structured information including review text, timestamps, ratings, and business location data, making it ideal for joining with external data sources.

[Yelp Reviews Open Dataset](https://business.yelp.com/data/resources/open-dataset/)

To incorporate lunar data, I used the United States Naval Observatory’s Moon Phase API. This allowed me to extract the moon phase associated with specific dates in my dataset.

[US Navy Moon Phase API](https://aa.usno.navy.mil/data/api#phase)

Because external factors like weather can influence some people's mood, I included historical weather data using the Open Meteo API. For each date and location, I collected daily maximum and minimum temperature as well as total precipitation.

[Open Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api?hourly=&daily=temperature_2m_max,temperature_2m_min,precipitation_sum&timezone=auto&temperature_unit=fahrenheit)

Finally, to quantify customer sentiment from unstructured review text, I used the Ellmer R package to interface with a large language model. This allowed me to extract structured features such as sentiment (on a 1–10 scale) and a binary indicator for whether a review exhibited “kooky” or unusual behavior.

[Structured Text Extraction Using Ellmer & ChatGPT](https://ellmer.tidyverse.org/)

---

## Workflow 

The workflow for this project began with sourcing and preparing a large scale dataset of customer reviews. I first loaded the Yelp review dataset, which contains approximately seven million observations, along with the corresponding business dataset. In order to improve runtimes and keep geographic differences between customers constant, I filtered the business data to include only establishments located in Illinois. I then joined the reviews and business datasets using the business_id field, allowing me to append location information such as latitude and longitude to each review. To facilitate time based analysis and API integration, I converted the review timestamps into a standardized date format (YYYY-MM-DD) and created a separate dataset of unique review dates to reduce the number of calls to the moon phase API.

To study the potential influence of lunar cycles, I filtered the dataset to include reviews between March 2015 and March 2020. This time window was intentionally chosen to exclude the COVID-19 period, which could introduce abnormal patterns in customer behavior. Using the filtered set of unique dates, I built a function to call the United States Naval Observatory Moon Phase API and retrieve the corresponding moon phase for each date. Because the API operates on a per-date basis, I iterated over all unique dates and compiled the results into a structured dataset (moon_df), which was then joined back onto the review data by date.

Next, I incorporated weather data to control for environmental factors that may influence customer sentiment. To minimize redundant API calls, I created a set of unique combinations of latitude, longitude, and review date. I then built a function to query the Open Meteo Historical Weather API, retrieving daily maximum temperature, minimum temperature, and total precipitation for each location and date pair. Due to API rate limits, I implemented a short delay (Sys.sleep(0.12)) between requests and collected the data in batches. The resulting weather dataset was then joined back onto the review-level data using date and geographic coordinates.

To extract meaningful insights from the unstructured review text, I used the Ellmer R package to perform structured sentiment analysis using a large language model. Each review was passed to the model with a prompt designed to return two specific outputs: a sentiment score on a 1–10 scale and a binary indicator capturing whether the review exhibited unusually erratic or “weird” behavior. This approach allowed me to transform qualitative text into quantitative features that could be analyzed alongside the moon phase and weather variables. 

Finally, these steps resulted in a unified dataset containing review-level information enriched with both lunar phase, weather conditions, and sentiment analysis. This combined dataset serves as the foundation for analyzing whether external factors such as moon phases and weather patterns are associated with variations in customer sentiment and behavior.

---

## Tableau Dashboard

[Public Dashboard](https:dashboard link)

---

## Technical Presentation

[Technical Presentation - Youtube](https: Youtube)
