---
layout: distill
title: Framework and Limitations of LLM-based Gender Stereotypes Analysis
description: 
tags: LLM
giscus_comments: false
date: 2023-02-27
featured: false

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
  - name: Introduction
  - name: An overview of gender stereotypes
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Limitations in current studies
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

## Introduction
In this post, I will introduce an influential theoretical framework of gender stereotypes and discuss some limitations in the current analysis of these stereotypes in generated stories.

---

## An overview of gender stereotypes
Gender stereotypes are pervasive in our society. They are generalized beliefs about gender groups that are applied to individual members simply because they belong to that group. Studies on gender stereotypes have frequently focused on binary gender in the workplace setting. Most of these studies have found that binary gender stereotypes have both descriptive and prescriptive characteristics. 

Descriptive gender stereotypes represent what women and men **are like**, which has been studied considerably. An influential point of view is that men are characterized as **"agentic"**, whereas women are described as **"communal"**. These differences have been further summarized into four pairs: achievement orientation versus concern for others; inclination to take charge versus affiliative tendencies; autonomy versus deference; and rationality versus emotional sensitivity. While there has been research exploring the impact of these stereotypes, some studies suggest that the gender differences in traits can be lessened when women are described as **highly successful managers**.

Prescriptive gender stereotypes refer to societal expectations regarding how women and men **should be like**. They serve as a preconceived notion when the only information available is someone's gender. Descriptive stereotypes make up one aspect of prescriptive stereotypes, establishing norms for how a particular gender group **"should be"**. For example, women are often stereotyped as communal, so communal traits are naturally expected of them. The other aspect of prescriptive stereotypes involves what individuals of a particular gender group **"should not be"**. For instance, men are discouraged from exhibiting communal attributes such as caring and sensitivity since they are traditionally associated with women.

Understanding key characteristics of gender stereotypes can be useful in identifying critical traits and establishing a connection between model outcomes and societal concerns.

---

## Limitations in current studies
With the increasing use of artificial intelligence and natural language generation, it is essential to evaluate the impact of these technologies on reinforcing gender stereotypes. In this section, I will delve into the limitations that currently surround the research on gender stereotypes in generated stories. 

### Non-binary gender
Researchers have not treated stereotypes of non-binary gender in much detail due to the absence of a consistent analytical framework in theoretical studies. Some researchers claim that non-binary individuals are often evaluated within the context of binary gender, with societal norms pressuring them to conform to one binary identity. Additionally, other researchers believe that non-binary individuals are a marginalized group that may be unfairly perceived as incompetent, cold, and mentally unstable. Furthermore, prior to ChatGPT, generative language models were unable to identify non-binary prompts and provide comparable responses, as discussed in [my previous post](https://kun126.github.io/2023/02/26/Why-ChatGPT-is-better-for-pronoun-based-analysis-of-non-binary-gender/).

### Implicit stereotypes
Numerous studies have been conducted on explicit stereotypes, which primarily focus on occupational biases. These biases are commonly observed in linking women with professions like nursing and homemaking, while men are linked to professions such as science and banking. In terms of gender-associated attributes, researchers have developed opposing trait lexicons, but these only help to interpret explicit stereotypes. For example, "weak" and "childish" are traits associated with women, while "strong" and "mature" are traits linked to men. However, implicit stereotypes with harmful implications and positive connotations remain less explored, and only a few studies have investigated this area.

### Prescriptive characteristic
When discussing the characteristics of gender stereotypes, it is unfortunate that there is currently few literature available that investigates prescriptive gender stereotypes. The existing studies that have been conducted on this topic are limited in their scope, as they often focus solely on feeding popular gendered names in prompts, which only allows for comparisons between different genders. While some studies have examined descriptive gender stereotypes (i.e., the traits and characteristics that individuals associate with different genders), these findings do not provide a full understanding of the complexities of gender stereotypes.

---

## Conclusion
Considering all that has been mentioned thus far, in my upcoming post, I will propose a method to analyze implicit stereotypes for three different genders: male, female, and non-binary. Additionally, I will also discuss prescriptive stereotypes within the same genders, which dictate what behaviors and characteristics are expected of individuals within a specific gender group. 


