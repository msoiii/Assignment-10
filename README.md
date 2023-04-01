# Assignment-10
Bias and Fairness Assessment of Models 

# Assignment-10
Bias and Fairness Assessment of Models 

The goal of this assignment is to test Google Jigsaw's Perspective API model for bias by using a sample dataset of internet comments. Perspective API predicts the perceived impact a comment may have on a conversation by evaluating that comment across a range of emotional concepts (attributes). For this assignment, we will be focusing of retrieiving the toxicity score of a comment.

TOXICITY is defined as “a rude, disrespectful, or unreasonable comment that is likely to make you leave a discussion”

Perspective API documentation: https://developers.perspectiveapi.com/s/?language=en_US

## Hypothesis

Data Exploration & Cleaning: 
<br>I cleaned the sample dataset, removed non-latinized comments, and created a new features column 'directed_towards' which displays 'male', 'female', and 'non-gendered' based on the most common pronoun counted in the comment text.I then found the most frequently used words in comments labeled as toxic by manual reviewers in which I uncovered that there was a similarity in the most frequent words between comments containing male and female pronouns. This lead me to dive deeper to evaluate if the Prospective API was biases in any way towards gender when labelling between the two. 

Creating a Threshold: 
<br>After evaluating the toxicity scores mapped to selected comments I believed to be mildly toxic, I set the theshold to be 0.4. Anything below 0.4 is considered non-toxic and anything above or equal to is considered toxic. 

Hypothesis: 
<br>My hypothesis for the Perspective API is that: 
**comments directed towards 'male' (comments that contain majority male pronouns) will be less likely to be labelled toxic than those directed towards 'female' (comments that contain majority female pronouns)**


## Testing 

To determine if the Perspective API is biased specifically to pronoun usage, I will conducted a test with a test sample of 18 comments to evaluate if there was a difference in the scores when the comment structure and content was the same but the individual pronouns changes between feminine and masculine.  

I wrote 9 unique comment templates that were modeled after comments in the original dataset. These comment templates are structured to allow for female or male pronouns to be inserted interchangeably. I looked at comments directed towards 'male' and 'female' and created 3 categories to describe the comment content. The 3 categories were 'insult', 'sexual/obscene', and 'threat'. I further separated them in order of toxicity levels (low, medium, high). 

For each of the comment templates, I only changed the pronouns used as this would allow me to specifically  evaluate the performance of Perspective API with pronoun usage in content controlled comments. 

**Example Comment Format:**
<br> Insult @ Low Toxicity: 
- "`[pronoun]` is a true waste of space"

**Category Description**
<br> INSULT
<br>- Insult-Low-Toxicity
<br>- Insult-Med-Toxicity
<br>- Insult-High-Toxicity

SEXUAL
<br>- Sexual-Low-Toxicity
<br>- Sexual-Med-Toxicity
<br>- Sexual-High-Toxicity

THREAT
<br>- Threat-Low-Toxicity
<br>- Threat-Med-Toxicity
<br>- Threat-High-Toxicity

## Results

In the controlled dataset the average toxicity score of the 18 random comments directed towards 'Female' received a higher score that those directed towards the 'Male' individuals. 

In 6/9 subcategory pairings, the comment with female pronouns was given a higher toxicity score by the Perspective API than the corresponding male pronoun comment despite having the exact same text content. 

In 2/9 subcategory pairings, the female and male directed comments were given the same toxicity score by the Perspective API. 

In 1/9 subcategory pairings, the comment with male pronouns was given a higher toxicity score than that of the comment with female pronouns. 

##### Percent Drop in Toxicity from Comments Directed Towards Females to Comments Directed Towards Males:  
<br> **INSULT**
<br>- Insult-Low-Toxicity: 6%
<br>- Insult-Med-Toxicity: 11%
<br>- Insult-High-Toxicity: none

**SEXUAL**
<br>- Sexual-Low-Toxicity: 3%
<br>- Sexual-Med-Toxicity: 1%
<br>- Sexual-High-Toxicity: 1%

**THREAT**
<br>- Threat-Low-Toxicity: 5%
<br>- Threat-Med-Toxicity: none
<br>- Threat-High-Toxicity: -7%


#### Factors that Influenced Results: 
Low Sample Size: 
<br>Having a low sample size of 18 comments impacts the reliability of my results and increases the probability that my results are due to random chance. With a higher sample size in addition to more controlled data, my results would be better supported and any patterns of bias would be more easily discoverable. I learned that specificity in the data is extremely useful to when evaluating a single factor in the data ~ such as different pronouns in comments that have the same exact structure and content.


### Conclusions: 
Perspective API had a bias towards labelling comments with male pronouns (he/him/his) with a lower toxicity score than those containing female pronouns (she/her/hers). Users who come across toxic comments that are directed towards 'female' (contain feminine pronouns) will be more likely to leave a discussion than when those comments are directed to 'male (contain male pronouns). 
