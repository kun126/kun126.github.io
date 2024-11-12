---
layout: distill
title: High Resolution Population Estimates
description: 
tags: demographics
giscus_comments: false
date: 2024-11-08
featured: true

authors:
  - name: Kun Chen
    url: "https://kun126.github.io"
    affiliations:
      name: Data-Pop Alliance, New York

bibliography: 

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Introduction
  - name: Methodological Differences
  - name: Caveats
  - name: Comparing Gridded Population Products
  - name: Considerations for Different Use Cases

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

**High-resolution population estimates** have become essential in fields like healthcare, disaster response, urban planning, and environmental management. These datasets provide a detailed view of population distribution, allowing decision-makers to target resources and interventions more effectively. Recent advances in integrating satellite data with census information have further improved the accuracy and timeliness of these population maps, making them powerful tools for both research and practical applications.

Two widely-used high-resolution population datasets are **WorldPop** and Meta’s **High-Resolution Settlement Layer (HRSL)**:

- **WorldPop**, developed at the University of Southampton, offers open-access, peer-reviewed population datasets, which includes two types of population grids: one estimates populations across all land grid squares globally (unconstrained), while the other estimates populations only within areas identified as built settlements (constrained).
- **Meta’s HRSL**, created with CIESIN at Columbia University, combines satellite imagery with census data to estimate populations specifically within identified settlements. This high spatial resolution data provides detailed insights into both urban and rural population distributions.

In this post, we will compare the methodologies of these two datasets, exploring their assumptions, modeling approaches, and limitations, to help guide users in choosing the most suitable product for their needs.

---

## Methodological Differences

### Starting Points and Goals
WorldPop addresses a major limitation of prior studies—the dependency on high-resolution imagery, which is often costly and computationally intensive. By designing its models to work with a broad range of global datasets, WorldPop is capable of integrating both continuous and discrete covariates, allowing it to produce reliable population estimates across different scales, even in areas with limited high-resolution data. In contrast, HRSL prioritizes accuracy, particularly in rural regions where sparse populations pose significant challenges to remote sensing techniques and traditional modeling. By improving building detection, HRSL enhances the accuracy of population estimates in these low-density areas, aiming for global consistency.

### Modeling Approach
WorldPop employs a Random Forest model combined with a variety of geospatial inputs to perform dasymetric redistribution, aiming to capture the spatial heterogeneity of population distribution at the pixel level within census units. The model uses recent census-based population counts, redistributing them across grid cells by analyzing the relationships between population densities and diverse covariate layers, such as land use, elevation, and infrastructure. This approach assumes that the Random Forest model’s capability to incorporate multiple variables enhances the accuracy of population estimates.

HRSL, on the other hand, bases its methodology on high-resolution building detection, operating on the assumption that buildings serve as a strong indicator of population presence, especially in sparsely populated rural areas. Meta employs deep learning architectures, primarily Convolutional Neural Networks (CNNs) such as SegNet and FeedbackNet, to detect human-made structures in high-resolution satellite imagery. Once identified, the population is distributed proportionally across all buildings within census units.

### Data Sources and Input Layers
WorldPop integrates traditional factors associated with population distribution—such as land cover, digital elevation models, and slope estimates—alongside supplementary geospatial data layers that may indicate human presence, including road networks, waterways, settlement boundaries, protected areas, night lights, and facility locations. Together, these data sources enhance the model's flexibility and accuracy. Meta's model, on the other hand, uses high-resolution (50 cm) satellite imagery from DigitalGlobe, primarily collected between 2010 and 2015, to identify and map individual buildings.

### Evaluation Metrics
WorldPop evaluates model performance by comparing aggregated grid cell predictions to census data, and by benchmarking against other population mapping products, such as GPW, GRUMP, and Afri/AsiaPop. WorldPop quantifies accuracy using root mean square error (RMSE), percent RMSE (%RMSE), and mean absolute error (MAE). HRSL’s evaluation, however, is more focused on the accuracy of its building detection process. It separates statistical errors, which stem from random variation, from systematic errors, which result from misclassification (e.g., false positives). Meta uses precision and recall to assess building identification accuracy and standard error to evaluate population redistribution across detected settled areas.

---

## Caveats
When comparing high-resolution population models, particularly Meta’s High Resolution Settlement Layer (HRSL) and WorldPop, it's crucial to understand each model’s strengths, limitations, and assumptions. Both models strive to estimate where people live, but their differing approaches mean that each model has unique challenges and trade-offs, especially when applied across diverse regions. Here’s a breakdown of the main limitations of each approach:

**WorldPop**
- **Input Layers and Spatial Resolution:** WorldPop’s model incorporates multiple layers of environmental and ancillary data to improve contextual accuracy. However, this layered approach limits spatial resolution to that of the coarsest data layer, which can reduce overall precision. Additionally, the quality of these input layers varies by region and collection period, relying heavily on local data collection standards. This variability introduces potential biases and inconsistencies when data is aggregated across different countries or regions.

- **Modeling Technique:** WorldPop uses a random forest machine learning model, which is based on decision trees. While flexible and powerful, this model has limitations in accounting for complex spatial variations across diverse geographic regions. Moreover, the decision-making process within random forests can be opaque, making it challenging to understand how specific inputs shape final estimates. This lack of interpretability may impact user confidence in the model’s outputs.

- **Non-zero Allocated Output:** A unique limitation of WorldPop’s model is that it does not use building footprint data, resulting in population estimates for all land grid cells, even in areas without residents. This can lead to misallocations, placing population estimates in regions that are likely uninhabited.

**Meta (HRSL)**
- **Population Allocation:** Meta’s HRSL model uses a proportional allocation method to estimate population distribution. While this approach is straightforward, it leaves room for improvement through more advanced techniques. Adopting more sophisticated redistribution approaches could enhance accuracy by accounting for nuanced variations in population spread, particularly in diverse settings.
- **Assumptions:** HRSL assumes a uniform approach across urban and rural areas, basing estimates on building identification alone. This creates potential inaccuracies, particularly in urban areas where buildings vary in height and function (residential versus non-residential). Because HRSL does not yet consider these factors, its estimates may be less accurate in densely built environments.

---

## Top-Down vs. Bottom-Up Strategy
Building on previous chapters, this section takes a higher-level perspective on modeling strategies, shifting the focus from technical and model-specific details to structural design. Here, we outline two primary approaches: the top-down and bottom-up methods.

Both WorldPop and HRSL employ the Top-Down Approach, which starts with broad, aggregate data sources, such as national census counts. These aggregate counts, usually at high administrative levels, are then redistributed into smaller, consistent grids, using supporting data like land use, satellite imagery, and other geospatial inputs. In contrast, the Bottom-Up Approach begins with highly detailed, localized data—such as household surveys—and scales up to create gridded population estimates across larger regions. Each approach offers unique strengths and trade-offs, which shape population mapping outcomes.

**Top-Down Approach**
- **Pros:** It’s efficient, using readily available census and ancillary data to cover large areas consistently. It works well for standardized datasets at a national or global scale.
- **Cons:** Resolution can be limited by the initial census data quality, and it may not accurately capture fast-changing population patterns.

**Bottom-Up Approach**
- **Pros:** Offers highly detailed, localized population data, ideal for small areas and regions with rapid population changes.
- **Cons:** It’s resource-intensive, often requiring extensive surveys, and may miss data in hard-to-access areas, making it challenging to scale up.

---

## Comparing Gridded Population Products
In this section, we summarize key characteristics of main gridded population products, providing a comparison across multiple dimensions such as **methodology, long-term monitoring capabilities, regional and global usability, and practical considerations**. The focus will include WorldPop, HRSL, along with two other widely used products: **Gridded Population of the World (GPW)**, developed by the Center for International Earth Science Information Network (CIESIN) at Columbia University, and **LandScan**, provided by Oak Ridge National Laboratory (ORNL). 




<div class="caption">
    Table 1. Comparison of Global Gridded Population Datasets on Methodology 
</div>

|            **Characteristics**             |          **WorldPop**          |                 **HRSL**                 |              **GPW**              |              **LandScan**               |
|:------------------------------------------:|:------------------------------------:|:----------------------------------------:|:----------------------------------:|:---------------------------------------:|
| **Top-down/Bottom-up**                   | Top-down                   | Top-down                                | Top-down                           | Top-down for global version, bottom-up for HD version   |
| **Allocation Method**                      | Dasymetric                           | Proportional/uniform                    | Proportional/uniform               | Dasymetric                              |
| **Model**                                  | Random forest                        | Convolutional Neural Network (CNN)      | Statistical mapping                | Probabilistic weighting (global)        |
| **Input Data**                             | Census data, land cover, elevation data, road networks, waterways, settlement boundaries, protected areas, night lights, and facility locations | Census data, DigitalGlobe satellite images | Census data, administrative data, water mask | Census data, land cover, elevation data, road networks, night lights (global); ORNL Population Density Tables, land use, infrastructure data, and points of interest (POI) |

<div class="caption">
    Table 2. Comparison of Global Gridded Population Datasets on Monitoring Capability
</div>

|            **Characteristics**             |          **WorldPop**          |                 **HRSL**                 |              **GPW**              |              **LandScan**               |
|:------------------------------------------:|:------------------------------------:|:----------------------------------------:|:----------------------------------:|:---------------------------------------:|
| **Latest available year**                       | 2020                   | 2020 public version, 2023 AWS version | 2020  | 2022 from GEE, 2023 from Explorer       |
| **Last Update Date**                       | 2020                                 | 2020 (public), 2023 (AWS)   | 2018                                | 2023                                    |
| **Update Frequency**                       | Yearly for unconstrained; no updates for constrained | Quarterly                                | Every five years                    | Yearly                                   |
| **Resolution**                             | 100m, 1km                            | 30m                                     | 1km                                 | 1km (global), 100m (HD)                 |
| **Available Period**                       | 2000-2020 (unconstrained); 2020 only (constrained) | 2020 (public); at least 2020-2024 (AWS) | 2000-2020                       | 2000-2022 (global)              |


<div class="caption">
    Table 3. Comparison of Global Gridded Population Datasets on Global Usability
</div>

|            **Characteristics**             |          **WorldPop**          |                 **HRSL**                 |              **GPW**              |              **LandScan**               |
|:------------------------------------------:|:------------------------------------:|:----------------------------------------:|:----------------------------------:|:---------------------------------------:|
| **Input comparability**                           | Mixed input layers from various periods | Yes, global building identification     | Yes, as only population count and masks are considered | Mixed input layers from various periods |
| **Coverage**                               | Global                               | Global                                  | Global                             | Global (global); selected countries (HD) |
| **UN Adjustment**                          | Yes, for both constrained and unconstrained | Yes                                     | Yes                                 | No, but differences are minor           |

<div class="caption">
    Table 4. Comparison of Global Gridded Population Datasets on Rural Usability
</div>

|            **Characteristics**             |          **WorldPop**          |                 **HRSL**                 |              **GPW**              |              **LandScan**               |
|:------------------------------------------:|:------------------------------------:|:----------------------------------------:|:----------------------------------:|:---------------------------------------:|
| **Input for building identification**              |  No                 | Yes            | No                     | No (global); Yes (HD)   |
| **Zero Allocation**                        | Yes (constrained)            | Yes                                     | Yes                                 | Yes                                     |


<div class="caption">
    Table 5. Comparison of Global Gridded Population Datasets on Other Practical Considerations
</div>

|            **Characteristics**             |          **WorldPop**          |                 **HRSL**                 |              **GPW**              |              **LandScan**               |
|:------------------------------------------:|:------------------------------------:|:----------------------------------------:|:----------------------------------:|:---------------------------------------:|
| **Relationship to Census**                 | Census disaggregation                | Census disaggregation                   | Census disaggregation               | Census disaggregation (global); no census (HD) |
| **Age and Sex Breakdown**                  | Yes                                  | Yes                                     | Yes                                 | ADM1 level only                         |
| **GEE Accessibility**                      | Yes                                  | Yes, 2020 only                          | Yes                                 | Yes                                     |



---

## Considerations for Different Use Cases
When selecting a gridded population product, the decision involves balancing the available data with the specific needs of the use case. The choice depends on a variety of factors, starting with the most critical requirements for the application. Below is a proposed decision-making process to help determine the best gridded population product for customized use cases.

**Single Country, Non-Monitoring Settings**

If you are working in a single country with no long-term monitoring goals, and you need the latest available data at a finer resolution, we recommend investing in bottom-up modeling based on recent surveys (such as DHS). Alternatively, consider LandScan HD if high-resolution age and sex breakdowns are not critical, or HRSL if you have access to AWS services.

**Single Country, Long-Term Monitoring**

For long-term monitoring in a single country, WorldPop, GPW, and LandScan are ideal, as they provide population rasters dating back to 2000 and ensure historical consistency. It's important to note that GPW updates every five years, while WorldPop and LandScan update annually. The choice between these datasets will depend on the presence of sparsely populated or undeveloped regions. In such areas, a zero-allocation method with building identification is preferred over non-zero allocation (as shown in the maps below). Even when land cover data is used, some datasets may overlook sparse settlements and categorize these areas into larger land types like grassland or cropland. Another key consideration is resolution—WorldPop and HRSL are better suited when a finer resolution is needed.

<div class="caption">
    Figure 1. HRSL, LandScan, WorldPop Constraint and Unconstraint Population Map
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/for_post/3popmap.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

**Global/Regional Setting**

When working on a global or regional scale, additional considerations beyond spatial and temporal needs become relevant, such as the ability to adjust data across countries after redistribution. This is viable on the user’s side if consistent datasets like UN population estimates are available. However, the population product should ideally offer global coverage, making LandScan HD less suitable for this purpose.

**Practical Considerations**

There are several practical factors that can influence the final decision. In humanitarian contexts, where age and sex breakdowns are crucial for analyzing vulnerable populations, WorldPop, HRSL, and GPW are ideal options. For countries with recent, reliable population data—particularly for policy planning, demographic analysis, and resource allocation—aligning to census data is an essential consideration. Lastly, the availability and accessibility of these datasets via platforms like Google Earth Engine (GEE) may also impact the decision.

