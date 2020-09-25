# Competitive Landscape Analysis

## Overview
The goal of this project is to perform competitive landscape analysis using ML techniques such as similarity analysis and topic modeling. Business insights were drawn following a SWOT framework.

## Approach
### Preliminary step: research
For each target organization, missions and programs were scraped from the Internet manually and recorded into an Excel spreadsheet.

### Data import
For demonstration purpose, this analysis will be carried out on organizations with `priority != 3`

### Preprocessing
- Text Cleaning
  - Lowercase
  - Remove punctuations, special characters and digits
  - Tokenization
  - Lemmatization
  - Remove stopwords. Also exclude
  - Organization names (and their acronyms)
  - Some other frequent words we are not interested in, i.e., words that are likely to appear for almost every document
    - Remark: we don't want the repetitive occurrences of these words to affect token frequency later. ['nonprofit','non','profit','inc','program','mission', 'organization','world','today','day','jersey','student','kid','education','year','age']
  - Vectorization: TF-IDF

### Similarity Analysis for Missions
- K-means Clustering
  - `K=5`
    - Given the small dataset, tuning is not so necessary as larger K will always lead to smaller inertia.
  - Visualization: Multidimensional scaling
  <img src="https://github.com/lullaby1024/Competitive_Landscape_Analysis/blob/master/img/cluster.png" width="85%">

- Organizations with the same color are of the same cluster so that they share similar missions.
- The distance between each organization shows the difference in missions.
- Closer organizations are more similar in missions (also higher probability of collaboration/competition?)

### Topic Modeling for Programs (with Gensim)
- Model: LDA
  - Weight implies importance of the word to the topic
  - Ideally, we want each topic to be distinct - to have distinct keywords.
  - Baseline coherence (3 topics):  0.38
    - Topic Coherence measures relative distance between words within a topic.
    - We target for a high coherence.
  - Best coherence (5 topics): 0.41
- Visualization: pyLDAvis
 <img src="https://github.com/lullaby1024/Competitive_Landscape_Analysis/blob/master/img/topic_annotated.png" width="85%">

## Business Insights
- The following questions are answered by this project:
  - Which organizations have similar missions as JerseySTEM?
  - Which organizations have similar programs as JerseySTEM?
  - Based on the results, where does JerseySTEM lie in the market? What are the opportunities/threats?
  
## Limitations
- Scraping is done manually. Scrapers can be developed to automate the process.
- Scaling
  - This project only models on 12 target organizations.
- Model performance
  - Coherence for the best model is still low.
    - Improvements on text preprocessing (or even data gathering), e.g., bigrams
    - Use of other models, e.g., LDA Mallet
  - Hyperparameters tuning needs to be done with more care if the problem scales up. This include but is not limited to:
    - Choice of K (number of clusters) in clustering
    - Choice of K (number of topics), alpha, beta
    
## Tableau
- Two dashboards were created to summarize results and facilitate comparison.
- [Competitive Landscape Analysis](https://public.tableau.com/profile/qi.feng1229#!/vizhome/CompetitiveLanscape/Dashboard1). This dashboard summarizes basic info about each organization. It includes a map, a bar chart for revenue and three pie charts for age group, STEM area and whether the programs charge.
<img src="https://github.com/lullaby1024/Competitive_Landscape_Analysis/blob/master/img/competitive_landscape.png" width="80%">

- [Competitive Landscape Analysis - Mission Similarities](https://public.tableau.com/profile/qi.feng1229#!/vizhome/CompetitiveLanscape-MissionSimilarity/Dashboard2). This dashboard visualizes the mission similarities across the organizations.
<img src="https://github.com/lullaby1024/Competitive_Landscape_Analysis/blob/master/img/competitive_landscape_missions.png" width="80%">
