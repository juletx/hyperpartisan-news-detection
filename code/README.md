﻿# Analyzing hyperpartisan documents

The purpose of this code is to analyze the usage of words in documents which are considered to be *hyperpartisan*, or not. Hyperpartisan arguments are those that "exhibit blind, prejudiced, or unreasoning allegiance to one party, faction, cause, or person".

The dataset were used in the [semeval-2019 task 4](https://pan.webis.de/semeval19/semeval19-web/) on hyperpartisan News detection. Whereas the task on semeval was to design a system to auto- matically detect hyperpartisan news, in this exercise we are going to exploit both corpora and analyze which terms are the most relevant in each of the sets. For this, analysis we will use the so-called log odd ratio.

I recommend you to follow a two-step approach to obtain the log-odd ratios of the words. In the first step, you should generate text files from the XML documents. Then, in a separated step, you should create a le with the words along with its **log-odd ratio**.

## 1. Generate text files

The first step is to generate two text files for hyperpartisan and non-hyperpartisan news articles, respectively. You have to divide the News articles contained in [articles-validation-bypublisher-20181122.xml.zip](https://zenodo.org/record/1489920/files/articles-validation-bypublisher-20181122.zip?download=1) into two text les (`hyperpartisan.txt` and `non-hyperpartisan.txt`), according to their ground truth value in [ground-truth-validation-bypublisher-20181122.xml.zip](https://zenodo.org/record/1489920/files/ground-truth-validation-bypublisher-20181122.zip?download=1). You will need the `lxml` library in python to analyze the XML documents and extract the necessary information.

When dividing the articles, it is highly recommended that you tokenize the text using a proper tokenizer. There are several tokenizers available for English in Python, chose the one that fits you best.

## 2. Extract log-odd ratios

Having the two text files, write a script that extracts the log-odd ratios of each word, by applying the equations. Because the log-odd ratio is sensitive to infrequent words, discard words that appear less than 20 times in the corpus. As a bonus, you can also extract the log-odd ratios of the bigrams in the corpus.

The log odd ratio is a measure of words compared on two sets of documents ($i$ and $j$), which in our case corresponds to hyperpartisan and non-hyperpartisan documents, respectively. Each word then can be associated with its log-odd ratio $r_w$, which is a number that can be positive or negative: positive numbers are associated with set $i$, and negative numbers with set $j$.

The log-odd ratio $r_w$ is defined as:

$$p_w^{(i)} = \frac{f_w^{(i)}}{N^{(i)}}; p_w^{(j)} = \frac{f_w^{(j)}}{N^{(j)}}$$

$$o_w^{(i)} = \frac{p_w^{(i)}}{1-p_w^{(i)}}; o_w^{(j)} = \frac{p_w^{(j)}}{1-p_w^{(j)}}$$

$$r_w = \log{o_w^{(i)}} - \log{o_w^{(j)}}$$

where $f_w^{(i)}$ is the frequency of word $w$ in group $i$ (hyperpartisan or non-hyperpartisan), and $N^{(i)}$ is the number of words in group $i$.

## 3. Analyze the results

Having the log-odd ratios, extract the most relevant 50 words in hyperpartisan and non-hyperpartisan documents. Analyze these words, and write a small document with your findings. Is there any interesting word on some set? Can you draw some conclusions regarding hyperpartisan text with respect to non-hyperpartisan ones? If you also computed the log-odd ratios for bigrams, repeat the analysis using bigrams.

### Words

There are many differences betweeen the 50 most relevant words of hyperpartisan and non-hyperpartisan news. Here are the main findings of each class.

Words of hyperpartisan articles:

- Hyperpartisan articles contain words ending in -ist/-ism/-ity(anarchist, anarchism, globalist, globalists, individualist, anarchists, zionists, vulgarity, profanity). These do not appear in non-hyperpartisan words.

- Other hyperpartisan words that describe people (slager, teabagger, shep, lgbtq, courteous). Similar terms do not appear in non-hyperpartisan words.

- Bad words in hyperpartisan articles (fucking, trolling, fuck, fck). There are no bad words in non-hyperpartisan.

- News sites or webs in hyperpartisan articles (wonkette, realclearpolitics, newsbusters, vox, gofundme, newsmax, foxnewscom). This suggest that these news sites are commonly associated with hyperpartisan news. Most correspond to news agencies in the US. No news agencies appear in non-hyperpartisan words.

- Other organizations in hyperpartisan news (usmc (United States Marine Corps), splc (Southern Poverty Law Center), emmys). They are US organizations.

- People in hyperpartisan articles (oreilly, kilmeade, chomsky, cavuto, grahamcassidy, omalley, madsen, beyoncé, willard, odonell, kliff, machado, watters, susteren). They correspond to politicians, journalists and famous people.

Words of non-hyperpartisan articles:

- Demonyms in non-hyperpartisan articles (subsaharan, nigerians, thai, israelpalestinian, nigerian). They correspond to people from other countries. No demonyms appear in hyperpartisan words.

- Places in non-hyperpartisan articles (bangkok, myanmar, rakhine, nigeria, thailand, tribune, kyoto, lima). Many places appear in non-hyperpartsan words, none in hyperpartisan words. They correspond to other countries and cities.

- People in non-hyperpartisan articles (straus, zuma, newsom, hun, schwarzenegger, hu (Hu Jintao)). They correspond to politicians and famous people.

- Organizations in non-hyperpartisan articles (treasuries, boko, haram, tic, utaustin (The University of Texas at Austin), anc (African National Congress, pri (Partido Revolucionario Institucional), nld (National League for Democracy)). Unlike hyperpartisan organizations, many organizations are from other countries different from the US.

- There are many economics terms in non-hyperpartisan articles (renminbi, yen, rebalance, cfr, depreciation, exporters, aggregator, outflow). Some correspond to currencies and other to actions or people.

### Bigrams

There are many differences betweeen the 50 most relevant bigrams of hyperpartisan and non-hyperpartisan news. Here are the main findings of each class.

Bigrams of hyperpartisan articles:

- More negative words than on non-hyperpartisan news (threats violence, hate group, divestment sanctions, overdose deaths, illegal alien)

- People (obama, trump, bill oreilly, romney, darren wilson, mr comey, van susteren). They correspond to politicians or famous people

- Media related terms (media research, independent journalism, media matters, corporate media, associate editor)

- Politics related terms (trump obama, legislature, obamacare, america health, basic income, ruling class) 

Bigrams of non-hyperpartisan articles:

- Demonyms in non-hyperpartisan articles (southeast asian, african).

- Places in non-hyperpartisan news (texas, us, china, southeast asia, travis county, austin). Some places are repeated a lot in different bigrams: china, us and texas are the most repeated ones.

- Many economics related bigrams also appear a lot (emerging economies, exchange rate, emerging markets, direct investment, private investors...).

- Organizations (boko haram, international institutions, china gorvernment...)

- People are also mentioned (dan patrick, jacob zuma, suu kyi, president jacob, david dewhurst)