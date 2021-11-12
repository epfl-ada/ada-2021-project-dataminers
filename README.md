# Project Purposal (Milestone 2)
## *How American political efforts affect their annual greenhouse gas emissions?*
## Abstract
Climate change is one of the world’s top topics today, and reducing greenhouse gas emissions is a heavy responsibility of the governments of major countries. However, there also exists objections. As the largest emitter of carbon dioxide per capita in the world, how did American politicians care about it, and what are their attitudes towards it? In this project we are eager to see how much the American politicians focus on the global warming topic and how their attitudes change throughout the 12 years of 2008-2020. By comparing the result with the actual total annual greenhouse gas emissions in the United States, we try to develop the real impact of American political efforts on their actual emissions, and how it is correlated. Additionally, we are also curious about the different demographic distribution among politicians with positive and negative attitudes towards reducing carbon dioxide emissions, which may give us some insights on what might have resulted in the negative attitudes.
## Research Questions
### Task 1: The real impact of American political efforts on their actual emissions, and how it is correlated
---
#### Task 1.1: How much did American politicians care about global warming
Calculate the number of occurrences of the quotations related to climate change issues every year from 2008 to 2020 (assuming that the number of occurrence of the topic in the newspaper is related with the politicians' attention to it).
**Expected result:** *political attention value* = Number of occurrences of the quotations related to climate change issues every year

---
#### Task 1.2: How did the political attitudes towards mitigating global warming fluctuate between 2008-2020
Apply sentiment analysis to the quotations and score them from 0-1, with 0 as most negative attitude.
**Expected result:** *political support rate* = the fraction of quotations with positive attitudes

---
#### Task 1.3: What is the real impact of American political efforts on their actual emissions
Together with the actual annual greenhouse gas emissions data, construct a regression analysis of 

$$
\footnotesize
\begin{aligned} 
 emissions \sim & political\ attention\ value+political \ support\ rate\\ 
& +political\ attention\ value*political\ support\ rate
\end{aligned}
$$ 

*Discuss:* The casualty relationship is impossible to detect in this context, because the change of the greenhouse gas emissions can be also due to various non-political reasons, for example, the decrease of air and road travel during the COVID-19 pandemic.

---
### Task 2: How do politicians’ demographic factors (party affiliation, age, gender, etc.) affect their attitudes to this issue
What characteristics do people who are against it have in common, and what might have resulted in the negative attitudes.

## Proposed additional datasets
-   Metadata about the speakers in the Quotebank dataset (speaker_attributes.parquet): We will assign each speaker his party affiliation, age, gender, ethnic group, academic degree, religion from this dataset
    
-   Total annual greenhouse gas emissions in the United States from 2008 to 2019: the data is in csv format with a shape of (8,12). Columns are years from 2008 to 2019. Rows are GHG emissions in 7 sectors, including transportation, electricity generation, industry, agriculture, commercial, residential, and U.S. territories. Last row is the total amount of GHG in all 7 sectors. We plan to draw a line stacked chart ([one example here](https://github.com/epfl-ada/ada-2021-project-dataminers/blob/main/pics/us-ghg-emissions.png?raw=true)) to visualize the trend and use the data to perform a regression analysis with the results from quotebank.
(Source: EPA's annual Inventory of the U.S. Greenhouse Gas Emissions and Sinks [Greenhouse Gas Inventory Data Explorer | US EPA](https://cfpub.epa.gov/ghgdata/inventoryexplorer/#allsectors/allsectors/allgas/econsect/all))
## Methods
![workflow](https://github.com/epfl-ada/ada-2021-project-dataminers/blob/main/pics/workflow.png?raw=true)
<center><b>Workflow</b></center>

* **Information retrieval**: collect climate change related quotations for each year
	* method: basic search engine using word embeddings (can capture syntactic relationships and encode the word into low dimensions)
	
* **Sentiment analysis**: assign each quotation sentiment score (from 0-1, with 0 as most negative attitude)
	* method: 
	
		1. data labeling: manually label (and also with the help of proper sentiment dictionary) some qutations as training/validation dataset
		
		2. model training: apply different NLP models (textCNN, LSTM, etc.) to score the rest quotations, choose the model with best performance
		
|Model| Feasibility |
|:--:|:--:|
| Logistic Regression/SVM | traditional methods; not the first choice for large dataset |
| Random Forest | not widely used, but worth trying |
| BERT | too many parameters; long training time |
| LSTM | commonly used; can capture the sequence relationship between words |
| textCNN | simple; fast training speed; low interpretability; not commonly used |

* **Observational study**: analyze whether for example, gender (same for other demographic factors), is the cause of negative attitude towards reducing carbon dioxide emissions
	* method: propensity-score matching to study the causality
  
## Organization and proposed timeline
| Date | Task to be done| Executor|
|:-:|:-:|:-:|
| 11.12-11.20| Information retrieval|Jingqi Liu, Yinghui Jiang|
| 11.21-12.4 | Sentiment analysis |Maocheng Xu, Yu Zhou|
| 12.5-12.10 | Observational study |Jingqi Liu, Yu Zhou|
| 12.10-12.17 | Visualization storytelling |Yinghui Jiang, Jingqi Liu|
| 12.17-12.20 | Website design & presentation preparation |Maocheng Xu, Yu Zhou|
 
