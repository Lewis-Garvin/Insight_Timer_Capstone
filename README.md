# Insight Timer Capstone Project
An analysis of guided meditations and teachers on the Insight Timer app for my NSS Data Analytics capstone project

## Table of Contents
- [Motivation](#motivation)
- [Data Questions](#data-questions)
- [Data Source](#data-source)
- [Analysis and Data Visualizations](#analysis-and-data-visualizations)
- [Installation](#installation)
- [Usage](#usage)

## Motivation
Insight Timer is the world’s largest free, openly accessible library of guided meditations. Unlike most other meditation apps, which offer a limited set of curated guided meditations, Insight Timer is an open platform on which anyone may join as a meditation teacher offering meditations of any and all varieties. Insight Timer shares a portion of their premium membership revenues with their teachers, so it is becoming a source of supplemental income for a variety of meditation and yoga teachers, musicians, and others.

Despite Insight Timer’s openness and flexibility, they store and present information about their teachers and guided meditations in a very structured form specific to the domain. Most of this information is available on their website outside of the app. I have not found a comparable dataset for a large number of guided meditations or teachers.

What could Insight Timer’s database of information on teachers and meditations tell us about what meditation looks like today and how it is changing?

I have a personal interest in this topic as someone who has been learning and practicing meditation for the past seven years at Wild Heart Meditation Center in Nashville.

## Data Questions
- What types of guided meditations are available and popular on Insight Timer?
- What are the characteristics of popular guided meditations and successful meditation teachers? (A key metric is the number of times a meditation is played. Insight Timer distributes a percentage of their revenue to teachers based in part on their total number of plays.)
- What opportunities are there for new teachers to find an audience for their guided meditations on Insight Timer?



## Data Source
The data source is Insight Timer’s website (https://insighttimer.com/), which has structured information available for their guided meditations and meditation teachers. This data is collected by web scraping using Python and Selenium.

Meditation Teachers (~16,000) <br>
Example page: https://insighttimer.com/jackkornfield  <br>
Columns: <br>
- Name
- Location
- Followers
- Languages
- Date Joined
- About
- Image url

Guided Meditations (~160,000)  <br>
Example page: https://insighttimer.com/jackkornfield/guided-meditations/breathing-meditation  <br>
- Title
- Teacher
- Length
- Number of plays
- Average Rating
- Number of reviews
- Type: ‘Guided’, ‘Talks’, or ‘Music’
- Suitable for: ‘Beginners’, ‘Everyone’, etc.
- Topics: Multiple tags/keywords from list of over 200 topics.
- Description

As of January 5, 2022, data has been successfully collected for all meditation teachers and about 60,000 guided meditations.

## Analysis and Data Visualizations
A Google Slides presentation summarizing the findings of this project may be found here:
https://docs.google.com/presentation/d/1eHlNvPp8X6wVc52N4GmQEQnC_GQZcu9EmH5Da51aFPE/edit?usp=sharing <br>
Talking points for each slide will also be made available soon.

# Installation
Note: The web scraping in this project works with the Insight Timer website (https://insighttimer.com/) as of December 2022. Future changes to the Insight Timer website may be incompatible with this project, which will need to be updated to accommodate those changes.

To use this project, you will need to have the following Python libraries installed:
- bs4
- datetime
- IPython
- json
- locationtagger
- matplotlib.pyplot
- nltk
- numpy
- os
- pandas
- plotly.express
- re
- seaborn
- selenium
- string

To use selenium for the web scraping notebooks, download a selenium webdriver appropriate for your browser (chromedriver.exe for Chrome). Update the chrome_driver_path variable within the notebook to reflect the location of your file.

Create the following subdirectories within your local project directory:
- /data
- /data/med_detail_batch_files
- /data/med_list_batch_files
- /data/teacher_batch_files

# Usage
The eight notebooks in this project are used to scrape data from Insight Timer's website, cleanse the resulting data, and finally to analyze it by creating data visualizations using the Python libraries matplotlib, seaborn, and Plotly. The table below shows the dependencies among the notebooks and the data files they read and create. Most of the scraping notebooks process and save their results in batches; each of these notebooks can be run multiple times to process a subset of batches.

| Group | Notebook | Dependencies | Data Files Read | Data Files Created |
| :----: | :----: | :----: | :----: | :----: |
| Teacher List | scrape_teacher_list.ipynb | None | None (web scraping only) | teachers_list_df.csv |
| Teacher Detail | scrape_teacher_detail.ipynb | Run after scrape_teacher_list.ipynb | teachers_list_df.csv, teachers_batch_list.csv | teachers_batch_list.csv, batch files in /data/teacher_batch_files |
| Teacher Detail | cleansing_teacher.ipynb | Run after scrape_teacher_detail.ipynb | batch files in /data/teacher_batch_files | teachers_df.csv, teachers_languages_df.csv |
| Teacher Detail | cleansing_locationtagger.ipynb | Run after cleansing_teacher.ipynb | teachers_df.csv | Updates teachers_df.csv, adding city and country columns |
| Meditations | scrape_meditation_list.ipynb | Run after scrape_teacher_list.ipynb; Can run before Teacher Detail group | teachers_list_df.csv, med_list_batches.csv | med_list_batches.csv, batch files in /data/med_list_batch_files |
| Meditations | scrape_meditation_detail.ipynb | Run after scrape_meditation_list.ipynb | med_detail_batch_df.csv, batch files in /data/med_list_batch_files | med_detail_batch.csv, batch files in /data/med_detail_batch_files |
| Meditations | cleansing_meditations.ipynb | Run after scrape_meditation_detail.ipynb | batch files in /data/med_detail_batch_files | meditations_df, meditations_topics_df.csv, topics_df.csv |
| Analysis | analysis_and_visualizations.ipynb | Run after all other groups/notebooks | teachers_df.csv, teachers_languages_df.csv, meditations_df.csv, topics_df.csv, meditations_topics_df.csv |
