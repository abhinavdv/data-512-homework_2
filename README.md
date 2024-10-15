# Analysing Bias in Wikipedia Politician articles data by Country

## Goal

The goal of this assignment is to analyse bias in Wikipedia Politician articles data by country. The analysis is done by combining data from Wikipedia articles with country populations and article quality data. Article quality data is coming from a ML model called ORES.

The expectation is to perform an analysis of the data and answer the below 6 questions:

1. Top 10 countries by coverage: The 10 countries with the highest total articles per capita (in descending order) .
2. Bottom 10 countries by coverage: The 10 countries with the lowest total articles per capita (in ascending order) .
3. Top 10 countries by high quality: The 10 countries with the highest high quality articles per capita (in descending order) .
4. Bottom 10 countries by high quality: The 10 countries with the lowest high quality articles per capita (in ascending order).
5. Geographic regions by total coverage: A rank ordered list of geographic regions (in descending order) by total articles per capita.
6. Geographic regions by high quality coverage: Rank ordered list of geographic regions (in descending order) by high quality articles per capita.

## Code Organization

The code for the assignment is organized into the following notebooks:

1. 1_wiki_article_page_info_retrieval.ipynb: This notebook retrieves the Wikipedia articles for politicians by country and saves the data to a CSV file.
2. 2_getting_ores_data.ipynb: This notebook retrieves the quality of the Wikipedia articles using the ORES API and saves the data to a CSV file. The quality of the articles is classified into six categories: FA (Featured Article), GA (Good Article), B, C, Start, and Stub.
3. 3_merge_datasets.ipynb: some of the steps to taken to format some of these files better for faster access in the analysis dataset.
4. 4_analysis.ipynb: This notebook performs the analysis of the data and answers the six questions mentioned above.

Run Each notebook in the order mentioned above to get the final analysis. Alternatively, you can run the 4th notebook directly. But make sure to have all the csv files in repository before running the 4th notebook.

## API used

### ORES API

The ORES API is utilized to determine the quality of Wikipedia articles. It classifies articles into six quality categories: FA (Featured Article), GA (Good Article), B, C, Start, and Stub. To retrieve the quality of an article, the following URL is used:

- https://ores.wikimedia.org/v3/scores/enwiki/?models=articlequality&revids=REVID
- https://www.mediawiki.org/wiki/ORES

The API response is a dictionary where the article's quality can be found under the key prediction.

### Pageinfo API (Mediawiki)

- The Pageinfo API from Mediawiki was used to retrieve the last revision ID of a Wikipedia article.
- For more information about the API, visit https://www.mediawiki.org/wiki/API:Pageinfo

## Licenses

### Source Data

The data is sourced from the Wikimedia Foundation via their publicly available Pageinfo API and ORES API. According to the Wikimedia Foundation's [Terms of Use](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use), users may freely utilize the content with proper attribution, preservation of open licenses, and respect for copyright. Appropriate attribution is provided to ensure compliance with these terms.

### Data Acquisition Code

Some portions of the code below are derived from examples created by Dr. David W. McDonald for the DATA 512 course in the UW MS Data Science degree program. This code is shared under the Creative Commons CC-BY license. Revision 1.2 - September 16, 2024.

## Generated Files

Following are the intermediary files generated during the analysis:

1. ores_output.json -> the output from the ORES API calls giving us the quality of the articles
2. politicians_by_country_AUG.2024.csv -> the dataset containing the politicians and their countries (Provided in the assignment)
3. population_by_country_AUG.2024.csv -> the dataset containing the population of the countries (Provided in the assignment)
4. wiki_information.csv -> the dataset containing rev_ids of the wiki articles

## Issues faced/ Special considerations

1. After retriving data from the ORES API, 4 records did not have proper responses. The upper limit given was 1% and since number was less than 1%, I decided to continue with the analysis.
2. There were a few duplicate records in the politicians data. I decided to keep the first record and remove the rest.
3. The csv files might need to be put in the path of the notebook to run the analysis. This has also been mentioned in each notebook.

## Research Implications

The data reveals some interesting patterns. In the first table, I was surprised to see that smaller countries like Antigua and Barbuda, Micronesia, and the Marshall Islands have the highest articles per capita. It seems their low populations, paired with a similar number of politicians, drive up the ratio. On the other hand, populous nations like China and India rank low, which makes sense, but it made me wonder if factors like literacy rates, internet access, or GDP also play a role.

When looking at high-quality articles in the third table, I initially expected larger countries to lead, assuming they’d have more rigorous vetting processes. However, smaller nations like Montenegro and Luxembourg ranked higher, possibly due to better internet penetration and education. Countries like India and China, despite low overall coverage, actually do better in terms of high-quality content, though places like Bangladesh and Pakistan continue to lag.

The geographic analysis further highlights that smaller regions generally have more articles per capita, while many Asian and African regions have less, probably due to factors like lower literacy, internet access, or even restrictive government policies. What stood out to me in the final table is that African regions have more high-quality articles per capita than Asian countries, which I didn’t expect. I suspect that greater Western influence in Africa might be enriching the content available there.

I could not find any conclusive evidence of a particular set of factors driving these patterns. However, I believe that further research into the impact of literacy, internet access, and government policies on Wikipedia content could provide more insights. I also feel that analysising the size of people actively using wikipedia in a country will give a better understanding of the quality of articles as wikipedia is a platform where people can contribute to the articles.

Question-1: What biases did you expect to find in the data (before you started working with it), and why?
I expected to find that countries with higher populations would have more article data since there would be more people actively participating. Then, I felt that other factors like internet connectivity access and freedom of speech would impact the access to wikiedia which would inturn imapct the number of articles. Also, I thought that the literacy rates of the country would also impact the quality of the articles.

Question-2: What (potential) sources of bias did you discover in the course of your data processing and analysis?

- One bias is the way that reader of these articles would percive the politicians of the country. If there are less articles, less is known whihc is okay. However if there are more poorly written articles, it might lead to a negative perception of the politicians and the country as a whole. Thus, more literate and internet accessable countries might have better articles leading to a bias.
- Another way of seeing bias is that countries which control the internet have stricter policies. I some cases as read in the VOX article about [AI’s Islamophobia problem](https://www.vox.com/future-perfect/22672414/ai-artificial-intelligence-gpt-3-bias-muslim), there is an example of the GPT-3 always replying with pro-Chinese propoganda, countries where the government has strict control over the internet might have articles which are biased towards the government.
- Another bias can also be in the ORES data itself. Given that we do not know how well the model is trained, the quality of the ORES data should be questioned.

Question-3: What might your results suggest about (English) Wikipedia as a data source?

- I feel that there is an over-representation of countries with more access to wikipedia in general. We should understand that the data is not a true representation of the world and should be taken with a grain of salt.
- We should also understand that all data i wikipedia might not be accurate and it should be cross-verified with other resources as with any other information page.
- Sometimes, writers might have a bias and push an agenda. This needs to be kept in mind while reading the articles.

Question-4: How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?

- In countries with fewer articles, researchers could add more data from other sources such as verified studies, government reports etc. Also, the dialect of English as stated in Duarte, N., Llanso, E., & Loup, A. (2018), might play factor in the ML algorithm picking up the quality of the article. Researchers can also use the actual data of number of users of wikipedia instead of just the poulation of a country to get a better context of the activeness of a particular country or rgion in wikipedia.
