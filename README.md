
# Exploration of Customer Lunacy Across Moon Phases
## ISA 401 Final Project

This repository contains the work for my final project for ISA 401, a data visualization and business intelligence course at Miami University.

---

## Project Setting

Back in high school, I worked as a server at a family-owned restaurant. There were several nights when my coworkers and I noticed that our tables felt a little more unpredictable than usual. One of my coworkers, Sonya, would always say, “It must be a full moon tonight.” Out of curiosity, I started checking, and surprisingly she was sometimes right.

That experience stuck with me. For this project, I wanted to revisit that idea and explore it more systematically. Specifically, I set out to determine whether there is any measurable relationship between lunar phases and customer behavior.

---

## Data Sources

To analyze customer sentiment, I needed a reliable source of restaurant reviews. I initially explored scraping platforms such as Google Reviews, OpenTable, and TripAdvisor, but ran into limitations related to access, structure, and scraping restrictions. Instead, I used the Yelp Open Dataset, which is designed for academic use. This dataset provides structured information including review text, timestamps, ratings, and business location data, making it ideal for joining with external data sources.

[Yelp Reviews Open Dataset](https://business.yelp.com/data/resources/open-dataset/)

To incorporate lunar data, I used the United States Naval Observatory’s Moon Phase API. This allowed me to extract the moon phase associated with specific dates in my dataset.

[US Navy Moon Phase API](https://aa.usno.navy.mil/data/api#phase)

Because external factors like weather can influence some people's mood, I included historical weather data using the Open Meteo API. For each date and location, I collected daily maximum and minimum temperature as well as total precipitation.

[Open Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api?hourly=&daily=temperature_2m_max,temperature_2m_min,precipitation_sum&timezone=auto&temperature_unit=fahrenheit)

Finally, to quantify customer sentiment from unstructured review text, I used the Ellmer R package to interface with a large language model. This allowed me to extract structured features such as sentiment (on a 1–10 scale) and a binary indicator for whether a review exhibited “kooky” or unusual behavior.

[Structured Text Extraction Using Ellmer & ChatGPT](https://ellmer.tidyverse.org/)

---

## Workflow 



---

## Tableau Dashboard



