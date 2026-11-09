# Project brief: Can genre help predict video game sales success?

**Status:** Working plan, 9 November 2026. **Submission deadline: 22 April 2027.** The research question and methods can change if the evidence warrants it. The milestone dates below are proposed checkpoints, not additional university deadlines.

## 1. Overview and motivation

Publishers choose what kinds of games to make under uncertainty. The changing direction of *Resident Evil* and the prominence of *Call of Duty* in Shooters make genre an interesting starting point. These are **motivating examples**, not proof that genre causes sales. Publisher, franchise, platform, marketing, budget and many other factors may matter too.

This project uses the public [Video Games Sales as at 22 Dec 2016 dataset](https://www.kaggle.com/datasets/sidtwr/videogames-sales-dataset). Each original row is a game on one platform. The working analysis combines platform records for the same title, then asks whether the title's recorded worldwide sales reach **one million copies**. [Capcom](https://www.capcom.co.jp/ir/english/business/million.html) describes one million units for a title as a major hit, which gives the threshold a practical rationale. The dataset's totals remain estimates and may omit digital or other sales.

## 2. Aim and research question

**Aim:** Assess how useful genre is for predicting whether a game title reaches one million **recorded** worldwide sales across the platforms present in this dataset, and whether publisher and release year improve that prediction.

**Main question:** *To what extent can genre predict whether a video game title reaches one million recorded worldwide sales, and how does the prediction change when publisher and release year are considered?*

**Subquestions:**

1. How common is a one-million-title, overall and within each genre?
2. Do publisher or franchise patterns alter the apparent genre relationship?
3. Does the mix of recorded genres change by release year?
4. Do models using genre beat a simple baseline on unseen titles, and how much do publisher and year add?

**Meaning of “predict”:** Look for a useful statistical association using information that could be known before release. Do **not** interpret a model coefficient or genre comparison as evidence that changing a game's genre would cause a sales change. “Success” here means only the stated sales threshold; the data do not measure profit.

## 3. Requirements from the coursework

| Area | Evidence to produce |
|---|---|
| Data understanding (30%) | Origin, row meaning, coverage, missing values, duplicates, sales distribution, genre/publisher/year patterns, and an explanation of how findings changed the target and feature choices. Purposeful figures with written interpretation. |
| Problem and models (25%) | A justified title-level target; a main model suited to categorical data; one less suitable alternative actually applied to the same data and rejected using evidence. |
| Method and evaluation (30%) | A meaningful baseline, an untouched test set, validation using only training data, preprocessing fitted within the training pipeline, fixed random seeds, metrics suited to the relatively uncommon success class, and honest interpretation of errors. |
| Reflection and communication (15%) | Limits of sales estimates and genre labels; what real use would require; a specific AI-use appendix, including corrections to AI output. |
| Submission | A 2,000-word report (per the brief, ±10%) with the word count stated, bibliography in the style specified by the module and DOIs where available, plus a runnable Jupyter notebook with visible outputs. Label report figures/tables with the producing notebook cell. Give data source, library versions and run instructions. |

## 4. SMART working objectives

These are proposed checkpoints leading to the **22 April 2027** submission. They can move around other coursework, provided the final verification time is protected.

| When | Specific, measurable outcome |
|---|---|
| By **30 November 2026** | Check title aggregation and document every exclusion/correction; produce at least three figures that directly inform the target, feature choice or data limitations; write a short interpretation under each. |
| By **15 December 2026** | Read and note the two academic sources below. Record one useful claim and one limitation for each, in your own words. |
| By **31 January 2027** | Freeze the main target and features. Record the number of titles and the percentage labelled successful. Check whether conclusions change under at least one alternative threshold (for example 0.5 or 2 million). |
| By **28 February 2027** | Compare a majority-class or prior-probability baseline, a genre-only model, and a genre + publisher + year model on the same held-out titles. Test a less suitable alternative on the same split. Report a confusion matrix plus precision, recall and a suitable summary metric. |
| By **31 March 2027** | Draft the report within the permitted word count, insert cell-linked figures/tables, verify every citation and DOI, and write the AI-use appendix in your own words. |
| By **19 April 2027** | Restart and run every notebook cell in order, keep all outputs visible, confirm results match the report, and check that the data and version instructions let another person rerun it. |
| On **22 April 2027** | Submit the final report and notebook via Blackboard before the stated submission time. |

## 5. Working analytical choices to test

- **Unit of analysis:** one game title. Combining platform rows matters: some titles pass one million in total even though no single platform row does. Check that exact-name grouping has not merged unrelated games. The current exploration excludes eight ambiguous names and records a checked genre correction for *FIFA Soccer 13*; retain an audit trail and the untouched CSV.
- **Main target:** at least one million combined **recorded** sales. This threshold is interpretable, but subjective and sensitive to missing sales.
- **Candidate features:** genre first, then publisher and first recorded release year. Platform reach is worth exploring but may be unavailable when a publisher is making an early decision. Review the timing of each feature before modelling. Metacritic scores have many missing values and are usually known after release, so they are not a good feature for a pre-release question.
- **Candidate main model:** logistic regression with appropriate encoding. It is a reasonable starting point for a binary target and makes a transparent comparison between genre-only and expanded features.
- **Candidate less suitable model:** k-nearest neighbours on the same dataset. Its distance between one-hot encoded genres/publishers may be hard to justify. This is a hypothesis to evaluate, not a prewritten conclusion; if it performs well, report that honestly and explain what the comparison does and does not show.
- **Evaluation:** keep one title in one split only; use a fixed, stratified train/test split for the cross-sectional question, and consider a later-year holdout as a robustness check. A majority-class accuracy near 82% would be easy to obtain by predicting every title is below one million, so include precision, recall and a confusion matrix. Consider PR-AUC if predicted probabilities are used.

## 6. Focused literature review plan

The coursework does **not** explicitly demand a stand-alone literature review. For a 2,000-word report, a focused **200–300-word “context and related research” section** is more useful than a long survey. Each source should support a decision or a limitation:

| Source | What it contributes | How to use it critically |
|---|---|---|
| [Cox (2014)](https://researchportal.port.ac.uk/en/publications/what-makes-a-blockbuster-video-game-an-empirical-analysis-of-us-s/), DOI [10.1002/mde.2608](https://doi.org/10.1002/mde.2608) | Studies the likelihood of a video game title becoming a blockbuster; uses logistic regression among other methods and reports associations with publisher and platform. | Motivates testing more than genre. Its US data and definition of a blockbuster are not identical to ours. Read the paper before describing exact thresholds or findings beyond the abstract. |
| [Faisal and Peltoniemi (2018)](https://researchportal.tuni.fi/en/publications/establishing-video-game-genres-using-data-driven-modeling-and-pro/), DOI [10.1177/1555412015601541](https://doi.org/10.1177/1555412015601541) | Examines how video game genres are established using product databases. | Use to discuss why one broad genre label can be debatable and why classification errors matter. Check the full paper for specific claims. |
| [Capcom, *Platinum Titles*](https://www.capcom.co.jp/ir/english/business/million.html) | Gives a real-world rationale for the one-million-unit threshold. | A publisher's description of a “major hit” is a working convention; it is not a profit measure or universal rule. |
| [VGChartz methodology](https://www.vgchartz.com/methodology.php) | Explains limitations of its legacy software-sales estimates and the difficulty of digital coverage. | Use to qualify how much trust to place in recorded sales and how far findings apply beyond this historic dataset. |

**Literature questions for you to answer after reading:** Why did Cox use a binary blockbuster outcome? What does “publisher effect” mean without claiming causation? How might a broad or wrong genre label change our results? Is one million copies a fair threshold for every publisher and year?

## 7. Main limitations and checks

- The file ends in 2016, so it cannot directly analyse *Resident Evil 7* or today's games. A 2016 snapshot gives older releases more time to accumulate sales than newer releases.
- Recorded sales are estimates, not verified complete lifetime totals. The dataset does not include budgets, prices, marketing, development decisions or a reliable launch-period sales series.
- A yearly increase in the **share of titles** in a genre does not establish that publishers copied an earlier hit. We can describe the pattern, then state what additional time-series evidence would be needed.
- Genre and publisher are associated with franchises, investment, platform and audience. These comparisons do not identify a causal effect.
- Check whether large franchises such as *Call of Duty* dominate totals or success rates; report both counts and rates so a few famous games do not stand in for a whole genre.

## 8. Suggested report shape (2,000 words excluding references/appendices)

1. Introduction, question and related research: **300 words**.
2. Data origin, quality and exploration: **500 words**.
3. Target, features and model rationale: **350 words**.
4. Validation, results and interpretation: **600 words**.
5. Reflection and conclusion: **250 words**.

The exact balance can move as findings develop. Keep the report in your own voice and use the notebook as the source for every number and figure.

## 9. Decisions for the student to make

1. Is the intended use **before release** (help a publisher choose a project) or **at release** (estimate potential for an announced game)? This determines which features are legitimate.
2. Does “success” mean **one million recorded copies**, or would a different threshold better match the question? Explain the choice using both the data distribution and a real-world source.
3. Do you want the story to centre on **genre alone**, or on how genre changes when publisher is added? The second is likely more honest but needs careful wording.

### Referencing note

The supplied coursework text says **UWE Harvard**. [UWE's current general guidance](https://www.uwe.ac.uk/study/study-support/study-skills/referencing/cite-them-right-harvard) says **Cite Them Right Harvard** became its default in September 2026. Follow the module brief unless the lecturer confirms an updated requirement; check the final references against the required guide.
