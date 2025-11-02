This readme file was generated on [2025-11-02] by [Nitchanun Sinchaikul]


# GENERAL INFORMATION

* Title of Dataset: Movie Dialogue Density Dataset
## Author/Principal Investigator Information
Name: Nitchanun Sinchaikul
ORCID: 0009-0000-5409-5779
Institution: Queen Mary University of London
Address: Mile End Rd, Bethnal Green, London E1 4NS
Email: bb25061@qmul.ac.uk

* Date of data collection: 2025-11-02
* Geographic location of data collection: Not Applicable (Data was digitally derived from existing online sources).
* Information about funding sources that supported the collection of the data: This dataset was created as a requirement for the LIN7078 module at Queen Mary University of London.


# SHARING/ACCESS INFORMATION

* Licenses/restrictions placed on the data: CC BY-SA 4.0
* Links to publications that cite or use the data: None at this time
* Links to other publicly accessible locations of the data:
	* https://www.kaggle.com/datasets/nitchanunsinchaikul/movie-dialogue-density-dataset
* Links/relationships to ancillary data sets: This dataset is derived from the sources listed below.
* Was data derived from another source? Yes.
	* If yes, list source(s):
		* Dataset: "Movie Subtitle Dataset"
        	* Author: Adiamaan
        	* Location: https://www.kaggle.com/datasets/adiamaan/movie-subtitle-dataset
        	* Files Used: `movies_meta.csv` (Source 1) and `movies_subtitles.csv` (Source 2)
* Recommended citation for this dataset:
	* Nitchanun Sinchaikul. (2025). Movie Dialogue Density Dataset. https://www.kaggle.com/datasets/nitchanunsinchaikul/movie-dialogue-density-dataset.


# DATA & FILE OVERVIEW

## File List:
	* `dr1_ns_movie_dialogue_dataset.tsv`
    	* `dr1_ns_readme.txt`


# METHODOLOGICAL INFORMATION

## Description of methods used for collection/generation of data: 
	* Data was not collected directly from people. This dataset was constructed by downloading and processing two existing data files from the Kaggle source listed above.
	* Purpose: The goal is creating a tidy dataset for analyzing language in film, specifically focusing on the "density" of dialogue (how much talking there is). This dataset enables quantitative analysis of how dialogue volume differs across genres or runtime (e.g., do Action films more likely to have less number in words per minute than Drama films).

## Methods for processing the data: 
* The dataset was generated from the raw source files using an R script. The following steps were performed:
    1. Loaded: `movies_meta.csv` (Source 1) and `movies_subtitles.csv` (Source 2) were loaded into R Studio.
    2. Summarized: All subtitle lines from Source 2 (which had one row per line of dialogue) were grouped by `imdb_id` and collapsed into a single text block per movie.
    3. Combined: The metadata table (Source 1) was joined with the new summarized text table (Source 2) using `imdb_id` as the key.
    4. Filtered: The dataset was filtered to include only English-language films (`original_language == "en"`) with 	valid `runtime` data.
    5. Cleaned Genres: The `genres` column (stored as JSON text) was parsed to create a clean, human-readable comma-separated list.
    6. Constructed Subtitles: The raw subtitle text was cleaned (removing timestamps, HTML tags, and bracketed descriptions). `TotalWordCount` and `UniqueWordCount` were then calculated for each movie.
    7. Finalized: The `WordsPerMinute` variable was derived (`TotalWordCount / runtime`). The text column was removed, and a final sample of 600 observations was saved as `dr1_ns_movie_dialogue_dataset.tsv`.

## Instrument- or software-specific information needed to interpret the data: 
	* The script was run using R (v.4.5.1)
    	* Required packages: readr, dplyr, stringr, tidyr, jsonlite.



# DATA-SPECIFIC INFORMATION FOR: `dr1_ns_movie_dialogue_dataset.tsv`

* Number of variables: 7
* Number of cases/rows: 600
* Variable List:
	* `imdb_id` (character): Unique identifier from IMDb. Used as the primary key.
   	* `original_title` (character): The original title of the movie.
    	* `runtime` (integer): The total runtime of the movie in minutes.
    	* `genres` (character): A comma-separated list of genres (e.g., "Action, Adventure, Drama").
    	* `TotalWordCount` (integer): The total number of words in the cleaned subtitle text. **What it means: The total volume of dialogue in the movie.
    	* `UniqueWordCount` (integer): The number of unique (distinct) words in the cleaned subtitle text. **What it means: The size of the movie's vocabulary (lexical richness)
    	* `WordsPerMinute` (numeric): A measure of dialogue density (`TotalWordCount / runtime`). **What it means: The "dialogue density" or "pace" of the movie. A high number suggests a "talky" film (e.g., a Drama), while a low number suggests a more visual film (e.g., an Action movie).
* Missing data codes: Rows with missing or invalid data (e.g., `runtime = 0`) were filtered out. No missing data codes are present in the final file.