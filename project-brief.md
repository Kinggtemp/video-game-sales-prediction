# Project brief: Can genre help predict video game sales success?

**Status:** My working plan, 9 November 2026. **Submission deadline: 22 April 2027.** I may change the research question or methods if the evidence gives me a good reason. The dates below are my own checkpoints, not additional university deadlines.

## 1. Overview and motivation

I became interested in this question because of how the *Resident Evil* series changed direction and how strongly *Call of Duty* is associated with Shooters. These examples made me wonder whether genre helps predict a game’s sales. They do not prove that genre causes sales: publisher, franchise, platform, marketing, budget and other factors may also matter.

I am using the public [Video Games Sales as at 22 Dec 2016 dataset](https://www.kaggle.com/datasets/sidtwr/videogames-sales-dataset). Each original row represents a game on one platform. I plan to combine the platform rows for the same title and examine whether its recorded worldwide sales reach **one million copies**. [Capcom](https://www.capcom.co.jp/ir/english/business/million.html) describes one million units for a title as a major hit, which gives me a reason for testing that threshold. I still need to remember that these figures are estimates and may omit digital or other sales.

## 2. Aim and research question

**Aim:** I want to find out how useful genre is for predicting whether a game title reaches one million **recorded** worldwide sales across the platforms in this dataset. I will also test whether adding publisher and release year improves the prediction.

**Main question:** *To what extent can genre predict whether a video game title reaches one million recorded worldwide sales, and how does the prediction change when publisher and release year are considered?*

**Questions I will investigate:**

1. How common is a one-million-title, overall and within each genre?
2. Do publisher or franchise patterns alter the apparent genre relationship?
3. Does the mix of recorded genres change by release year?
4. Do models using genre beat a simple baseline on unseen titles, and how much do publisher and year add?

**What I mean by “predict”:** I am looking for a useful statistical association using information that could be known before release. I will not treat a model result or a genre comparison as proof that changing a game’s genre would change its sales. By “success”, I currently mean only reaching the stated sales threshold; this dataset does not measure profit.

## 3. What my coursework needs to show

| Area | What I need to show |
|---|---|
| Data understanding (30%) | I will explain the data’s origin, row meaning, coverage, missing values, duplicates and sales distribution. I will interpret genre, publisher and year patterns and show how my findings influenced the target and features. |
| Problem and models (25%) | I will justify the title-level target, choose a main model that suits the data, and apply a less suitable alternative to the same data. I will use the results to explain whether I reject that alternative. |
| Method and evaluation (30%) | I will include a simple baseline, keep a test set untouched during model development, validate using training data, prevent preparation steps from leaking information, fix random seeds and choose metrics that reveal errors on the less common success class. |
| Reflection and communication (15%) | I will discuss the limits of the sales estimates and genre labels, what practical use would require, and how I used and checked AI assistance, including any corrections. |
| Submission | I will submit a 2,000-word report (±10%) with its word count stated, references in Cite Them Right Harvard style and DOIs where available, and a runnable Jupyter notebook with visible outputs. I will label report figures and tables with the producing notebook cell and provide the data source, library versions and run instructions. |

## 4. SMART working objectives

These are my proposed checkpoints leading to the **22 April 2027** submission. I may adjust them around other coursework, but I want to leave time for a full rerun and final check.

| When | What I plan to complete |
|---|---|
| By **30 November 2026** | I will check how platform rows are combined into titles, document each exclusion or correction, and produce at least three figures that help me choose the target or features or understand a limitation. I will explain each figure. |
| By **15 December 2026** | I will read the two academic sources below and write down one useful point and one limitation for each, in my own words. |
| By **31 January 2027** | I will settle on the main target and features, record the number of titles and the percentage labelled successful, and test whether at least one other threshold (such as 0.5 or 2 million) changes the picture. |
| By **28 February 2027** | I will compare a simple baseline, a genre-only model, and a genre + publisher + year model on the same held-out titles. I will also test a less suitable alternative on that split and report a confusion matrix, precision, recall and another suitable summary metric. |
| By **31 March 2027** | I will draft the report within the permitted word count, link each figure and table to its notebook cell, check citations and DOIs, and write the AI-use appendix in my own words. |
| By **19 April 2027** | I will restart and run the notebook from top to bottom, save all outputs, check that its results match the report, and test the data and version instructions. |
| On **22 April 2027** | I will submit the final report and notebook via Blackboard before the stated submission time. |

## 5. Analytical choices I am testing

- **Unit of analysis:** I plan to analyse one game title at a time. Combining platform rows matters because some titles pass one million in total even though no single platform does. I need to check that grouping by exact name has not merged unrelated games. My current exploration excludes eight ambiguous names and records a checked genre correction for *FIFA Soccer 13*. I will keep an audit trail and leave the original CSV unchanged.
- **Main target:** I am testing at least one million combined **recorded** sales. The threshold is easy to explain, but it is a judgement and could be affected by missing sales.
- **Candidate features:** I will start with genre, then test publisher and first recorded release year. I may explore platform reach, although it might not be known when an early decision is made. I will check when each feature would be available. Metacritic scores are often missing here and are generally known after release, so I do not currently plan to use them for a pre-release question.
- **Candidate main model:** I am considering logistic regression with categorical features encoded appropriately. It suits a yes/no target and would let me compare genre alone with the expanded set of features.
- **Candidate alternative:** I will test k-nearest neighbours on the same data. I suspect that measuring distance between encoded genres and publishers may be difficult to justify, but I will judge it using the results. If it performs well, I will report that rather than assume it is unsuitable.
- **Evaluation:** I will keep each title in only one split and use a fixed, stratified train/test split for the main comparison. I may also test a later-year holdout. Predicting every title is below one million could already give accuracy near 82%, so I will examine precision, recall and a confusion matrix rather than rely on accuracy alone. If I use predicted probabilities, I will consider PR-AUC.

## 6. My reading plan

The coursework does not explicitly ask for a separate literature review. I plan to use around **200–300 words** in the report to discuss related research. I want each source to help explain one of my choices or limitations:

| Source | Why I selected it | What I need to check |
|---|---|---|
| [Cox (2014)](https://researchportal.port.ac.uk/en/publications/what-makes-a-blockbuster-video-game-an-empirical-analysis-of-us-s/), DOI [10.1002/mde.2608](https://doi.org/10.1002/mde.2608) | Studies the likelihood of a video game title becoming a blockbuster; uses logistic regression among other methods and reports associations with publisher and platform. | It gives me a reason to test more than genre. Its US data and blockbuster definition differ from mine, so I need to read the paper before using any more specific findings. |
| [Faisal and Peltoniemi (2018)](https://researchportal.tuni.fi/en/publications/establishing-video-game-genres-using-data-driven-modeling-and-pro/), DOI [10.1177/1555412015601541](https://doi.org/10.1177/1555412015601541) | Examines how video game genres are established using product databases. | I can use this to discuss why a single broad genre label may be debatable. I need to read the full paper before making specific claims about its results. |
| [Capcom, *Platinum Titles*](https://www.capcom.co.jp/ir/english/business/million.html) | It gives me a practical reason to test the one-million-unit threshold. | I will treat Capcom’s description of a “major hit” as a convention, not as a profit measure or a universal rule. |
| [VGChartz methodology](https://www.vgchartz.com/methodology.php) | Explains limitations of its legacy software-sales estimates and the difficulty of digital coverage. | I will use this to discuss how much trust I can place in recorded sales and whether the findings apply beyond this historic dataset. |

**Questions I want to answer after reading:** Why did Cox use a binary blockbuster outcome? What does “publisher effect” mean without claiming causation? How might a broad or wrong genre label change our results? Is one million copies a fair threshold for every publisher and year?

## 7. Limitations I need to address

- The file ends in 2016, so I cannot directly analyse *Resident Evil 7* or today's games. A 2016 snapshot gives older releases more time to accumulate sales than newer releases.
- I am working with estimated recorded sales, not verified complete lifetime totals. The dataset does not include budgets, prices, marketing, development decisions or a reliable launch-period sales series.
- A yearly increase in the **share of titles** in a genre does not establish that publishers copied an earlier hit. I can describe any pattern I find and explain what further time-series evidence would be needed to test that idea.
- Genre and publisher are associated with franchises, investment, platform and audience. I cannot use these comparisons to identify a causal effect.
- I will check whether large franchises such as *Call of Duty* dominate totals or success rates. I will show both counts and rates so a few famous games do not stand in for an entire genre.

## 8. Planned report structure (2,000 words excluding references/appendices)

1. Introduction, question and related research: **300 words**.
2. Data origin, quality and exploration: **500 words**.
3. Target, features and model rationale: **350 words**.
4. Validation, results and interpretation: **600 words**.
5. Reflection and conclusion: **250 words**.

I may adjust this balance as the findings develop. Every number and figure in my report will come from the notebook.

## 9. Questions I still need to resolve

1. Am I trying to help a publisher **before release**, when choosing a project, or **at release**, when a game has already been announced? My answer will determine which features I can fairly use.
2. Is **one million recorded copies** the best definition of “success” for this question? I will compare it with the sales distribution and at least one alternative threshold before settling on it.
3. Should the report focus on **genre alone**, or on whether the prediction changes when publisher is added? I will decide after comparing the models and looking at the data.

### Referencing

I will use **Cite Them Right Harvard** for in-text citations and the bibliography, following [UWE Bristol’s current guidance](https://www.uwe.ac.uk/study/study-support/study-skills/referencing/cite-them-right-harvard). I will include DOIs where available and check that every in-text citation has a matching reference.
