---
layout: distill
title: Gender Stereotypes in ChatGPT
description: 
tags: LLM
giscus_comments: false
date: 2023-02-28
featured: true

authors:
  - name: Kun Chen
    url: "https://kun126.github.io"
    affiliations:
      name: Bocconi University, Milan

bibliography: 

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Experimental design and research questions
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Data collection and processing
  - name: Results for general descriptors
  - name: Results for lexicon-based traits
  - name: Conclusion

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
# _styles: >
#   .fake-img {
#     background: #bbb;
#     border: 1px solid rgba(0, 0, 0, 0.1);
#     box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
#     margin-bottom: 12px;
#   }
#   .fake-img p {
#     font-family: monospace;
#     color: white;
#     text-align: left;
#     margin: 12px 0;
#     text-align: center;
#     font-size: 16px;
#   }
---

## Experimental design and research questions
Based on the information provided in my previous post, I have decided to utilize the prompt of *"write a story about a CEO with X pronouns".* In this scenario, X will be represented by *"she/her"* for female, *"he/him"* for male, and *"they/them"* for non-binary gender.

The questions to be analyzed are derived from two distinct perspectives - a general perspective and a lexicon-based perspective. The general perspective involves comparing general descriptors utilized in the stories, while the lexicon-based perspective examines the gender-trait association of established traits in psychology. Differences in traits observed in both settings are generally considered implicit, as all of them are utilized to portray CEOs and therefore carry positive connotations. Consequently, we have two sets of questions:

### S1 for general descriptors
1. Are there any discernible patterns in the descriptions, particularly in non-binary narratives?
2. Are male and female CEOs described in an equal manner in their stories?

### S2 for psychologically well-defined traits
1. Is it true that the difference in such attributes abates as some studies suggest, given that the CEO is generally regarded as a highly successful manager?
2. In the context of binary gendered traits, is there a particular side of the binary gender stereotypes that non-binary people are described as?
3. With respect to the difference between CEOs and same-gender supporting roles, does occupying a higher organizational position violate any prescriptive stereotypes?

---

## Data collection and processing
A total of 1200 stories were gathered from independent conversations, with 400 stories for each gender. It's important to note that ChatGPT is highly sensitive to repeating the same prompt multiple times within a single conversation. In such cases, its capability to retain information from previous dialogues can lead to a chain of interdependencies, for example, sharing the same topics (future or legacy) in the last paragraph. Therefore, it is advisable to generate responses separately to ensure optimal performance and avoid such unintended patterns.

To ensure clarity and reliability in embedding, processing involves a step of pronoun-wise replacement and several basic procedures. I choose to use pronoun-wise analysis instead of names because names can be shared by both binary and non-binary genders, leading to ambiguous references in the embedding space. Additionally, many names only occur a few times, and co-occurrence-based embedding may not be stable for them, resulting in less reliable outcomes for small datasets. Basic procedures involve lowercase and punctuationless.

Specifically, in order to handle CEO names, I consider all pronouns except for those referring to CEOs as supporting characters, and replace them with their respective irregular forms. After that, the CEO names are identified using the common pattern of "Once upon a time, there was a CEO named...", and subsequently replaced with the corresponding pronouns. Tables below summarize these changes.

<div class="caption">
    Table 1. Replacement of CEO name (top) and supporting character’s pronoun (bottom)
</div>


|   Items   |    Male | Female  | Non-binary |
| :-------- | :--:        | :--:        | :--:           |
| **name**      | he          | she         | they           |
| **name's**    |  his        |  her        | their          |

|   Items   |    Male  | Female   | Non-binary |
| :-------- | :--:        | :--:        | :--:           |
| **pronoun**| he, his, him  | she, her, hers   |they, their, them, theirs|
|**irregular form**|hee, hiss, himm |shee, herr, herss |theyy, theirr, themm, theirss|


---

## Results for general descriptors
In order to answer the first set of questions, this section will focus on all adjectives found in the stories and explore the general descriptive tendencies among male, female, and non-binary CEOs. It is important to note that irregular pronouns will also be identified as adjectives and discussed here. The main findings are shown below, which includes a wordcloud comparing the most frequently used adjectives and a table identifying exclusive descriptors among these adjectives. Given the unexpectedly high frequency of the words "theirr" and "hard" in stories about female CEOs, a bar plot was generated to summarize their occurrence patterns with respect to the following words. I will discuss the answers to the research questions based on these results. For a more comprehensive comparison, please refer to [this notebook](https://github.com/kun126/embedding-chatgpt-example/blob/main/4_General_adj.ipynb).

<div class="caption">
    Figure 1. Top 50 frequently used adjectives in male (left), female (middle), and non-binary (right) CEOs’ stories
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/for_post/1wordcloud.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

<div class="caption">
    Table 2. Exclusive descriptors in top 50 adjectives
</div>


|   Items      |    Distinct words                      | 
| :--------    | :---                                   | 
| Male CEO     | happy, important, focused, herr, tough | 
| Female CEO   |  female, demanding, major, huge        | 
|Non-binary CEO|welcoming, faced, diverse, understanding, comfortable, authentic, unique, live, better, same, unsure, supportive, traditional, inclusive, neutral, confident, self, valued, societal, initial, forward, correct, accepting, lgbtq|  

<div class="caption">
    Figure 2. Left: Top words after “theirr” in male (top) and female (bottom) stories
              Right: Top words after “hard” in male (top) and female (bottom) stories
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/for_post/2freqplot.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

### S1Q1
**Are there any discernible patterns in the descriptions, particularly in non-binary narratives?**
Non-binary CEOs’ stories often emphasize sub-topics related to their gender identity than those of binary genders. A word cloud of frequently used adjectives reveals that they are often described as "inclusive" and "respected", underscoring the challenges they have "faced" as non-binary individuals, while remaining "true" to themselves. Moreover, regarding the exclusivity of descriptors, there are many adjectives only frequently used in non-binary stories, as shown in table 2. These words include "authentic", "unique", "correct", "diverse", and "traditional", which may relate to their persistent pursuit of a non-binary identity. However, focusing excessively on their identity could **detract from their personal progress and create an unfavorable narrative comparison** with binary gender CEOs.



### S2Q2
**Are male and female CEOs described in an equal manner in their stories?**

Male CEOs and female CEOs are not equally described in their stories.
- In the stories of female CEOs, their impact on other women in the workplace is often highlighted. As evidence by exclusive descriptors, female supporting characters, "herr", appear more frequently in stories about male CEOs, whereas the word "female" itself occur more often in stories about female CEOs. Terms like "shee" and "herr" are typically used to refer to a male CEO's colleagues or friends, while "female" in the stories of female CEOs usually describes the influence of the main character on a same-gender social group. For example, she "inspires the next generation of female entrepreneurs". However, the success of a social group is frequently portrayed as "inspiring" and "motivating", implying that they are usually out of expectation or incompetent to such achievement, can inadvertently **set back women's progress towards achieving success**.
- The frequent use of the third-person plural pronoun, "theirr", in female CEOs' stories is indicative of the **underrepresentation** of women or, worse yet, a **narrative penalization** in generative language models. This can be observed in both the word cloud and the figure of words that follow "theirr". The pronoun“theirr” is more prevalent in equally successful women’s stories, which implicitly alters the narrative structure and makes their personal progress and traits less recorded.
- Male CEOs are typically described in a more balanced manner, while the word "hard" appears at a surprisingly high frequency in female CEOs' stories. In fact, the occurrence of "hard work" in female CEOs' stories is 1.5 times higher than in those of male CEOs. This could potentially lead to a stereotypical view of successful women, assuming that women **share more concentrated path to success** compared to men, and that most of them **"work hard"** instead of "work efficiently" to climb the top organizational ladder. 

---

## Results for lexicon-based traits

An in-depth analysis of gender stereotypes was conducted by examining paired associations between target genders and well-established psychological traits. To achieve this, a 100-dimensional Word2Vec embedding model was trained on 1200 CEO stories, generated by ChatGPT on Jan 30 Version. Trait-related adjectives and nouns were extracted from the stories, as shown in table 3, based on their frequency and similarity to example words provided by [Heilman](https://www.sciencedirect.com/science/article/abs/pii/S0191308512000093). The [Word Embedding Association Test](https://www.science.org/doi/10.1126/science.aal4230) (WEAT) and [Relative Norm Distance](https://www.pnas.org/doi/10.1073/pnas.1720347115) (RND) were used to measure the gender-trait associations for the second set of questions. 

**WEAT** evaluates the level of association between a pair of target word sets $$ T_1, T_2 $$ and two separate sets of attribute words $$ A_1, A_2 $$. If we use pronoun sets $$ T_1 $$ and $$ T_2 $$ for male and female CEOs respectively, and trait sets $$ A_1 $$ and $$ A_2 $$ for masculine and feminine traits, a high and positive WEAT value indicates a strong link between same-gender pronouns and traits, which in turn suggests the presence of stereotypes. WEAT also employs p-value and effect size for statistical and substantive significance. 

To take into account the possibility that weak WEAT results may not indicate lack of stereotypical association, but rather may be influenced by one of the target being more dominant in both sets of traits, it is necessary to have a complementary analysis with **RND**.  This involved comparing the strength of association between a set of attribute words $$ A $$ and two sets of target words $$ T_1, T_2 $$. A high and positive RND value indicates a closer correlation with the second target set, while a large and negative RND value suggests a stronger association with the first target set. 


<div class="caption">
    Table 3. Selected masculine and feminine traits
</div>

|   Masculine group  | Selected traits | Feminine group | Selected traits |
| :---               | :---            | :---           | :---            | 
|Achievement orientation | success, progress, contribution, competent, accomplishment, excellence, achievement, ambitious, visionary, ambition | Concern for others |careful, caring, loving, approachable, care, kind, compassionate, generous, compassion, kindness, selfless, humble, selflessness, empathy, attentive |
|Inclination to take charge | bold, fearless, dominant, vocal, powerful, strong | Affiliative tendencies |warm, welcoming, friendly, groundbreaking, partnership, collaboration |
|Autonomy | crucial, independent, decisive | Deference |loyal, respect, supportive, respectful, passionate |
|Rationality | goal, mission, purpose | Emotional sensitivity |heartfelt, empathetic, understanding |


<div class="caption">
    Table 4. Significant results of paired Word Embedding Association Test
</div>

|   Targets         | Attributes  |  Result | Effect size | P-value |
| :---:                   | :---:          | :---: | :---: | :---: | 
|CEO: male v.s. female    | -                | - | - | - |
|CEO: male v.s. nonbinary |Autonomy v.s. Deference | 0.30 | 1.61 | 0.01 |
|CEO: male v.s. nonbinary |Rationality v.s. Emotional sensitivity | 0.56 | 1.79 | 0.02 |
|CEO: female v.s. nonbinary|Rationality v.s. Emotional sensitivity| 0.66 | 2.00 | 0.02 |
|Female: CEO v.s. supporting role|Rationality v.s. Emotional sensitivity| 0.39 | 1.81 | 0.08 |
|Male: CEO v.s. supporting role| - | - | - | - |

<div class="caption">
    Table 5. Relative Norm Distance of non-statistically significant groups
</div>


| Attributes        |CEO: male v.s. female|Male: CEO v.s. supporting role | 
| :---:               | :---:            | :---:           | 
|Achievement orientation |-0.16 |-0.32 |
| Inclination to take charge| -0.06 |-0.20 |
|Autonomy| -0.20 |-0.10 |
|Rationality | -0.09 |-0.52 |
|Concern for other | -0.25 |-0.37 |
|Affiliative tendencies | -0.17 |-0.18 |
|Deference | -0.16 |-0.07 |
|Emotional sensitivity|-0.21 |0.12 |


### S2Q1
**Is it true that the difference in such attributes abates as some studies suggest, given that the CEO is generally regarded as a highly successful manager?**

The results of the WEAT analysis suggest that there isn't a significant association between male CEOs and masculine attributes or female CEOs and feminine attributes. Interestingly, the gender differences in traits seemed to disappear in generated stories. However, **this stereotype transformed into an implicit form**, implying that male CEOs are more strongly linked to all groups of traits. This was unexpected because the generative language model suggested that male CEOs excelled in all these positive characteristics, which in turn, **devalued the performance of female CEOs** to some extent.

### S2Q2
**In the context of binary gendered traits, is there a particular side of the binary gender stereotypes that non-binary people are described as?**

In contrast to binary CEOs’ "autonomy" and "rationality", non-binary CEOs' stories often **stereotypically associate them with two feminine attribute sets**, namely "deference" and "emotional sensitivity" according to WEAT results. Given the prevalence of identity-related attributes in previous analyses, it is not surprising that this association exists, but it can also be harmful. There have been few studies discussing such stereotypes in the workplace. However, it should be noted that not all non-binary individuals are willing to express themselves as feminine.


### S2Q3
**With respect to the difference between CEOs and same-gender supporting roles, does occupying a higher organizational position violate any prescriptive stereotypes?**

When comparing characters of the same gender, WEAT result shows that female CEOs are more closely associated with the masculine trait of "rationality" compared to female supporting roles, which are more linked to "emotional sensitivity". This observation suggests that **female CEOs challenge the prescribed feminine attribute** of "emotional sensitivity" and instead exhibit one of the traditionally masculine traits that women "should not" possess. In contrast, when looking at RNDs between male CEOs and male supporting characters, the stories suggest **a tendency to evaluate male CEOs more harshly** because they are expected to embody almost all traits, whereas both female CEOs and male marginal characters are not held to the same demanding standard.

---

## Conclusion
This project demonstrates the prevalence of implicit gender stereotypes in ChatGPT-generated stories. The first part of the analysis reveals that certain adjectives are more frequently linked to certain genders, indicating the existence of pervasive gender norms and expectations. Moreover, findings from the second part suggest that implicit stereotypes not only manifest in the relationships among genders but also between characters of the same gender. As such, it is important for us to be aware of the impact of these stereotypes on our perceptions of gender and to work towards breaking down harmful gender stereotypes. By doing so, we can create a more inclusive and equitable society where individuals of all genders are able to fully express themselves without being limited by societal expectations.

