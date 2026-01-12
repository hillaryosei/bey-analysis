# Beyoncé Lyrics Theme Analysis (2003-2022)
![Image of the artist Beyoncé through the many eras of her career. From left to right are: Dangerously In Love, B-Day, I Am...Sasha Fierce, 4, BEYONCÉ, Lemonade, and Renaissance](https://github.com/hillaryosei/bey-analysis/blob/main/bey-albums.jpg)

This project applies natural language processing and unsupervised machine learning to analyze how Beyoncé’s lyrical themes evolve across her career. Using TF-IDF vectorization and Non-Negative Matrix Factorization (NMF), I identify dominant lyrical themes and track their prevalence over time.

The goal of this project is both exploratory (What themes and sentiments emerge naturally from the lyrics?) and analytical (How do those themes shift across albums and eras?).

## Project Overview

* **Dataset:** Line-level Beyoncé lyrics (grouped into full songs), [created and compiled by myself](https://www.kaggle.com/datasets/hillaryosei/beyonce-lyrics)
* **Songs analyzed:** 92 songs
* **Albums covered:** 7
* **Core techniques:**
    * Text preprocessing
    * TF-IDF vectorization
    * NMF topic modeling
    * Temporal aggregation & visualization
* **Tech stack:**
    * Python
    * pandas
    * numpy
    * scikit-learn
    * nltk
    * matplotlib
    * Jupyter Notebook

## Data
The raw dataset contains one row per lyric line with the following fields:
* `artist`
* `album`
* `track_title`
* `track_num`
* `lyric`
* `line`
* `year`

### Data Preparation Steps
1. Group lyric lines by `track_title`
2. Concatenate llines into full-song lyric documents
3. Retain one row per song with:
    * full lyrics
    * release year

This transformation allows topic modeling at the song level, rather than treating isolated lyric lines as independent documents.

## Methodology
1. Text vectorization (TF-IDF)
    * Lyrics are converted into numerical feature vectors using TF-IDF
    * English stopwords are removed
    * `min_df=0.1` is used to reduce noise from rare terms
    * Result: each song is represented by its most informative words

2. Topic modeling (NMF)
* **Non-Negative Matrix Factorization (NMF)** is applied with 5 components
* NMF was chosen because:
    * It produces interpretable, additive topics
    * Topic weights are non-negative and easy to threshold
* Top words per topic are inspected and manually labeled

**Identified themes**
Based on the highest-weight words per topic, themes are labeled as:
* Love
* Heartbreak
* Sex
* Party
* Independence

3. Theme presence scoring
* Each song receives a score for every theme
* A theme is considered present if its score ≥ 0.1
* This converts continuous topic weights into binary indicators (0/1)

This makes it possible to count how many songs per year strongly express each theme.

## Visualization & analysis
Theme presence is aggregated by release year and visualized as a time series.
* X-axis: Year (album era)
* Y-axis: Number of songs expressing a theme
* Each line: One lyrical theme

This allows direct comparison of thematic emphasis across Beyoncé’s career.

## Results
The analysis reveals clear, interpretable trends across time:

### Early career (2003-2006)
* Love and heartbreak dominate
* Lyrics emphasize romance, vulnerability, and relationship dynamics
* Independence appears less frequently and usually alongside love themes

### Transitional era (2008-2013)
* Sex and party themes increase
* Lyrics become more confident and expressive
* Themes begin to overlap more strongly within songs

### Later career (2016-2022)
* Independence emerges as one of the most prominent themes
* Songs increasingly emphasize autonomy, self-worth, power, and identity
* Party themes remain present, but are often paired with empowerment rather than escapism

### Overall takeaway
The topic model captures a clear thematic evolution:
From romantic vulnerability → confidence → self-defined independence

## Repository Structure

```
├── bey-analysis
│   ├── beyonce_lyrics.csv       # Dataset containing Beyoncé's song lyrics
│   ├── bey-lyric-analysis.ipynb  # Jupyter Notebook with the analysis code
├── bey-albums.jpg             # Cover image for README
├── README.md                   # Project documentation (you are here)
```

## Getting Started

To replicate or build upon this analysis, follow these steps:

1. Clone the repository:

```
git clone https://github.com/hillaryosei/bey-analysis.git
```

2. Navigate to the project directory:

```
cd bey-analysis
```

3. Install the required dependencies. It is recommended to set up a virtual environment before installing the dependencies:

```
pip install pandas numpy matplotlib jupyter
```

4. Launch Jupyter Notebook:

```
jupyter notebook
```

5. Open the `bey-lyric-analysis.ipynb` notebook and run the code cells sequentially.


## Future Improvements
* Album-level rather than year-level aggregation
* Interactive visualization (Plotly / Streamlit)
* Added Cowboy Carter album to the analysis

## Disclaimer
Lyrics are used for analytical and educational purposes only.
All rights belong to their respective copyright holders.
