---
layout: distill
title: Why ChatGPT is Better at Pronoun-based Analysis
description: 
tags: LLM
giscus_comments: false
date: 2023-02-26
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
  - name: Introduction
  - name: Answer by ChatGPT
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Two Advantages of ChatGPT
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

[ChatGPT](https://openai.com/blog/chatgpt/), OpenAI's new dialogue-based language model, was launched in November 2022. Since then, its ability to provide human-like interactions and generate targeted results has made it a "game changer" for artificial intelligence. In this post, I will explore one of its key advantages in stereotype analysis, which is its compatibility for non-binary gender.

---

## Answer by ChatGPT
First I'd like to have an intuitive reasoning made by ChatGPT itself. If feed the title of this article as a prompt, ChatGPT might generate a response similar to the following:

> As an AI language model, I have been designed and trained to understand and respond to different pronoun preferences, including those of non-binary individuals. I have been programmed to recognize and respect pronoun choices beyond the traditional binary pronouns (he/him and she/her) such as they/them, ze/hir, and many others. 
> Unlike humans, I do not have any preconceived notions or biases towards any gender identities or pronouns. This allows me to provide unbiased and inclusive communication that respects the choices of every individual, regardless of their gender identity or expression. 
> Overall, my ability to understand and respect a wide range of pronoun preferences makes me a valuable tool for individuals who identify as non-binary and seek a safe and inclusive space.

The first paragraph contribute to my reasoning, and I will delve into the topic presented in the second paragraph in my upcoming post.

---

## Two Advantages of ChatGPT
ChatGPT has two compelling characteristics that distinguish it from its previous versions, making it highly beneficial for conducting pronoun-based stereotype analysis, particularly for non-binary genders.

### Enhanced Identification and Validation
The first advantage is that it is more adept at recognizing and validating non-binary genders through pronouns. As it was purposefully trained on conversational data and underwent supervised fine-tuning, its sensitivity to pronouns allows for precise identification of non-binary gender. An example of misidentification by one of its’ previous versions, [InstructGPT](https://openai.com/blog/instruction-following/), is:

> *Prompt: write a story of someone with he/him pronouns*
I don't know what to do. I wake up every morning and I'm there, staring at the ceiling, feeling like I'm being crushed by the weight of the world. I want to get up and do something, but I know that I can't. I don't have anyone to do anything with me, I can't even do it by myself. I don't know what to do.  

Unlike [GPT-3](https://openai.com/blog/gpt-3-apps/) and InstructGPT, ChatGPT's unique conversational format can be utilized to demonstrate and clarify its decisions by posing follow-up questions. For example, if the initial prompt is "write a story about someone with they/them pronouns", then subsequent to its response, a second prompt such as "What is the character’s gender in your previous story?" or "Is this character a queer or a gender-neutral person?" can be presented. ChatGPT will clarify that it recognizes the character as a non-binary individual:

> *Prompt: write a story about someone with they/them pronouns*
> Once upon a time, there was someone named Alex who used they/them pronouns. Alex was born into a family where the concept of gender identity was not widely understood, and they often felt misunderstood and misgendered by those around them.

> *Prompt: What is the Alex's gender in your previous story?*
> In the previous story, Alex's gender is nonbinary. They use they/them pronouns to reflect their gender identity.

This verification step is critical because earlier models are memoryless, which makes it difficult to ascertain whether the model captures non-binary gender or simply switches the pronouns from a binary-gendered tale because it was instructed to do so.

### Comparable Responses

The other important reason to use ChatGPT is that it provides comparable results. consistently delivers comparable results. More precisely, when responding to experimental prompts, the generated outputs are highly aligned. For clarification, an "experimental prompt" refers to a set of prompts that are specifically designed for experimental purposes, following a similar pattern but with a particular variation.

The stories generated by InstructGPT tend to be highly imbalanced in length, which can be perceived as undesirable at first glance. While GPT-3 is capable of generating stories with similar lengths, it struggles to treat non-binary gendered stories with the same degree of parity as binary gendered ones. Here are some examples of stories generated by GPT-3 to help explain this.

> *Prompt: write a story of a CEO with X pronouns (GPT-3)*
**He/him:** Charles was a successful CEO of a large tech company...
**She/her:** Samantha Stevenson was a CEO of a large, successful company... 
**They/them:** They had been a CEO for several years and done a great job, but... They/them: The CEO was a trailblazer in their industry, known for...

> *Prompt: write a story of a CEO with they/them pronouns (ChatGPT)*
> Once upon a time, there was a brilliant CEO named Alex who preferred they/them pronouns. Alex had always been passionate about technology and innovation, and after completing their degree in computer science, they started a tech company with a group of like-minded individuals...

In a binary gendered story, the pattern "who was a CEO of..." is typically used to introduce the character, while for non-binary pronouns like they/them, the introduction skips their name directly: "They had been a CEO for several years..." or "The CEO was a trailblazer in the industry, known for...". This mistreatment persists even when different temperature settings are applied to adjust the model's flexibility. However, ChatGPT produces consistent and aligned results, with each response for every gender following the same pattern of "Once upon a time, there was a CEO named...".

---

## Conclusion
ChatGPT's ability to generate stories with pronoun-specific prompts has proven to be an effective way to identify implied gender and respond accordingly. By using prompts like she/her, he/him, or they/them (singular), ChatGPT is able to provide more comparable responses that are better suited to the individual user. 
