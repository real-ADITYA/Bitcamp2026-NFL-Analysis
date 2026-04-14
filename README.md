# Bitcamp NFL Draft Project — Notebook Guide

## Overview

This project studies **NFL draft value**, with a focus on identifying **hidden gems** and using that idea to understand **which teams draft well or poorly**. Across the notebooks, the project evolves from an early fantasy-rookie analysis into a more complete pipeline that connects **combine traits**, **draft position**, and **later NFL production**.

The three notebooks serve different roles:

1. **`NFLdraft.ipynb`** — early exploratory notebook focused on **rookie fantasy outcomes**
2. **`Draft_Gems_Reports.ipynb`** — scouting report / text-trait notebook focused on **qualitative player traits**
3. **`nfl_draft_gems.ipynb`** — the main polished notebook that builds a **historical gem model** and scores the **2026 class**

---

## Recommended Reading Order

### 1. `NFLdraft.ipynb`
Read this first if you want to understand the **starting point** of the project.

### 2. `Draft_Gems_Reports.ipynb`
Read this second if you want to see how the project expanded into **scouting-report trait extraction**.

### 3. `nfl_draft_gems.ipynb`
Read this last. It is the **main notebook** and the best representation of the final Bitcamp idea.

---

## 1. `NFLdraft.ipynb`

## Purpose
This notebook is an **early exploratory analysis** that looks at rookie players and their fantasy football value. Its main idea is:

- take top fantasy performers by position
- compare them against rookie draft data
- see which teams, colleges, and positions produced fantasy-relevant rookies

## What the notebook does

### A. Loads fantasy data by position
It imports separate CSV files for:
- quarterbacks
- running backs
- wide receivers
- tight ends

### B. Keeps only top fantasy performers
It trims the fantasy datasets to an approximate fantasy-relevant range:
- top 24 QBs
- top 36 RBs
- top 48 WRs
- top 24 TEs

This makes the notebook focus on players who actually mattered in fantasy formats.

### C. Cleans player names
Fantasy data often includes team abbreviations inside the player field, so the notebook removes the trailing team text from player names. This is needed so the names match the rookie dataset.

### D. Loads 2025 rookie draft data
The notebook then reads a rookie draft CSV and compares the rookie list against the top fantasy players.

### E. Matches rookies to fantasy-relevant players
For each position, it finds players who:
- were rookies in 2025
- also showed up among the top fantasy scorers

### F. Creates simple visualizations
The notebook then graphs:
- number of top fantasy rookies by team
- number of top fantasy rookies by college
- number of top fantasy rookies by position

## Main takeaway
This notebook is a good **idea-generation notebook**. It is less about modeling and more about discovering patterns such as:
- which teams landed productive rookies
- which colleges fed the most fantasy-relevant rookies
- which positions produced the most immediate impact

## Why it matters to the project
This notebook helps motivate the broader project question:

> Can draft information help us understand which players and teams create the most value?

It is the most basic version of that question.

## Limitations
This notebook is more exploratory than predictive:
- it focuses on one rookie class
- it uses fantasy output directly
- it does not yet define hidden gems formally
- it does not model long-term value over expected draft position

---

## 2. `Draft_Gems_Reports.ipynb`

## Purpose
This notebook explores the **text side** of draft evaluation by using **scouting reports**. Instead of focusing only on measurements or fantasy stats, it tries to understand what kinds of **strengths and weaknesses** appear in reports for successful later-round players.

## What the notebook does

### A. Loads offensive player statistics
It begins with yearly offensive player stats and uses them to filter for meaningful NFL contributors.

### B. Defines a rough “successful later-round player” filter
It narrows the dataset to players who:
- played significant offensive snaps
- were drafted in later rounds
- had strong enough fantasy production

It also filters to more recent draft classes where scouting report data is available.

### C. Extracts unique player lists
Once the successful later-round players are identified, the notebook extracts:
- player name
- position
- college

This helps form the candidate set for report analysis.

### D. Loads scouting report data
The notebook reads a cleaned scouting report CSV containing text fields such as:
- strengths
- weaknesses
- position

### E. Builds a trait dictionary
A large keyword map is created to identify traits in report text. These include categories such as:
- instincts
- vision
- processing
- toughness
- and many more

There are separate groups for:
- strengths
- weaknesses

### F. Counts trait mentions
Each scouting report is processed so that the notebook can count how often each trait appears in:
- the strength text
- the weakness text

It then converts those counts into binary presence flags.

### G. Summarizes traits by position
The notebook computes how common traits are for each position and visualizes:
- most common strengths by position
- most common weaknesses by position

### H. Looks for “polarizing” traits
It checks for traits that appear as both a strength and a weakness across players or even for the same player. That helps identify traits that may be interpreted differently depending on context.

### I. Correlates trait patterns with performance
The notebook merges trait data with player performance indicators such as:
- average fantasy points
- average offensive snaps
- draft round

It then uses correlation analysis and heatmaps to see which reported traits are associated with better or worse outcomes.

## Main takeaway
This notebook adds a **qualitative layer** to the project. It asks:

> What do successful later-round players tend to look like in scouting language?

That makes the project more interesting because it moves beyond raw numbers and into how players were described before entering the league.

## Why it matters to the project
This notebook can strengthen the final Bitcamp story by showing that hidden gems are not just statistical accidents. Some may share recurring scouting themes, such as:
- instincts
- toughness
- vision
- processing
- effort
- versatility

## Limitations
This notebook is very useful, but it is also more experimental:
- keyword matching is not the same as full NLP understanding
- scouting report wording can vary heavily
- results may depend on the hand-built trait dictionary
- this notebook is more descriptive than predictive

---

## 3. `nfl_draft_gems.ipynb`

## Purpose
This is the **main notebook** of the project. It builds a structured pipeline to identify historical NFL draft gems using combine traits and later NFL outcomes, then applies that logic to the **2026 combine class**.

This is the notebook that best represents the project as a Bitcamp hackathon submission.

## Big-picture goal
The notebook tries to answer:

> Can pre-draft combine traits help us identify players who may become late-round NFL gems?

## What the notebook does

### A. Introduces the project
The notebook frames the project around the idea that NFL teams are always searching for value outside the early rounds, especially on Day 3 and late Day 2.

### B. Uses three main data sources
The notebook combines:
- historical combine data
- 2026 combine data
- offensive NFL performance stats

This creates a bridge from **pre-draft traits** to **post-draft outcomes**.

### C. Standardizes the combine datasets
The historical and 2026 combine files use different column names, so the notebook renames them into a shared schema. Important features include:
- player
- position
- school
- height
- weight
- forty-yard dash
- vertical jump
- bench press
- broad jump
- three-cone drill
- shuttle
- draft info

### D. Cleans the NFL performance data
The NFL stats table is reduced to the core outcome fields:
- player
- position
- draft year
- draft round
- draft pick
- season
- fantasy_points_ppr
- offense_snaps

It then creates two important outcome indicators:
- **starter season** = at least 500 offensive snaps
- **strong fantasy season**
  - top 12 at QB or TE
  - top 24 at RB or WR

### E. Merges historical combine data with NFL outcomes
To do this reliably, the notebook normalizes names by:
- lowercasing
- removing punctuation
- removing suffixes like Jr. or III

Then it merges combine records with NFL outcome records.

### F. Builds the historical training window
The notebook filters to a training period where both combine data and NFL outcomes are available. This becomes the historical dataset used for gem labeling and model training.

### G. Defines what a gem is
This is one of the most important parts of the entire project.

A player is labeled as a **gem** if they are:
- drafted in the **4th round or later**
- recorded a **starter season**
- recorded a **strong fantasy season**

This gives the project a clean and understandable target label.

### H. Analyzes historical gems
The notebook then studies how gems are distributed across:
- draft classes
- positions

It also compares average combine traits for:
- gems
- non-gems

### I. Creates exploratory visualizations
The notebook includes graphs for:
- gems by draft round
- gems by position
- forty-yard dash for gems vs non-gems
- vertical jump for gems vs non-gems
- snap count vs fantasy production

These figures help explain what differentiates gem-like players.

### J. Builds the model
The notebook uses a logistic regression pipeline with:
- median imputation
- scaling for numeric features
- one-hot encoding for position
- class balancing

The model uses features such as:
- position
- height
- weight
- forty
- vertical
- bench
- broad jump
- three-cone
- shuttle

### K. Evaluates the model
The notebook performs a train/test split and evaluates performance using:
- ROC-AUC
- average precision
- classification report
- confusion matrix

This is the predictive core of the project.

### L. Interprets model coefficients
After fitting the model on the full historical labeled set, it extracts the learned coefficients so the team can discuss which traits push players toward or away from gem-like status.

### M. Scores the 2026 combine class
The model is then applied to the 2026 combine table to generate a:
- **gem_like_score**

This gives every 2026 prospect a probability-like score based on similarity to historical late-round gems.

### N. Produces top 2026 gem candidates
Finally, the notebook ranks players and also creates top candidates by position.

This is the most demo-friendly part of the notebook because it turns historical analysis into a forward-looking prediction tool.

## Main takeaway
This notebook is the strongest final product because it combines:
- data preprocessing
- feature engineering
- label construction
- exploratory analysis
- machine learning
- practical predictions for a future draft class

It is the notebook you would use to explain the project to judges.

## Why it matters to the project
This notebook gives the project a real product-style pitch:

> Use historical combine and NFL production data to identify traits associated with later-round success, then surface overlooked 2026 prospects with gem-like profiles.

That is clean, understandable, and hackathon-ready.

## Limitations
The notebook is strong, but it still has important limits:
- it focuses on offensive outcomes
- the gem label uses fantasy success, so it is more fantasy/offense oriented than full football value
- it does not yet model busts
- it does not yet evaluate team drafting quality directly
- combine metrics alone may miss important context such as college production, scheme fit, injuries, and scouting nuance

---

## How the Three Notebooks Fit Together

The notebooks can be understood as three stages of the same idea.

### Stage 1: Rookie fantasy exploration
**`NFLdraft.ipynb`**
- explores rookie fantasy impact
- identifies useful joins between draft data and outcomes

### Stage 2: Scouting-report trait analysis
**`Draft_Gems_Reports.ipynb`**
- explores the language behind successful later-round players
- adds qualitative trait analysis

### Stage 3: Historical gem modeling
**`nfl_draft_gems.ipynb`**
- formalizes the gem definition
- builds a predictive model
- scores the 2026 class

Together, they show the progression from:
- descriptive exploration
to
- qualitative trait mining
to
- predictive modeling

---

## Suggested Bitcamp Demo Framing

If you are presenting this project at Bitcamp, the cleanest summary is:

### Project idea
We built a system that uses historical combine data and NFL outcomes to identify the profile of later-round draft gems, then used that model to score 2026 prospects.

### Why it matters
NFL teams often miss on later-round value, and fans, analysts, and front offices all care about finding overlooked talent.

### What makes the project interesting
- combines sports analytics and machine learning
- uses both quantitative and qualitative information
- produces forward-looking prospect scores
- can be extended into team drafting analysis and bust prediction

---

## Best “next steps” for the project

If this project continues beyond the hackathon, the strongest next additions would be:

### 1. Add bust labeling
Right now the project mainly models hidden gems. A natural extension is to define busts using:
- early-round draft capital
- poor NFL production
- low snap counts
- weak fantasy or positional outcomes

### 2. Evaluate team drafting quality
Once gems and busts are defined, you can compute:
- gem count by team
- bust count by team
- gem rate by team
- average value over expected by team

This would answer the next major question:
> Which teams draft well or poorly?

### 3. Add college production
Combine testing alone is useful, but adding college performance would likely improve predictions.

### 4. Expand to defense
The current notebook leans heavily toward offensive players and fantasy-relevant outcomes.

### 5. Use scouting report traits as model features
The trait extraction notebook could be folded into the main gem model for a more powerful hybrid system.

---

## Bottom Line

- **`NFLdraft.ipynb`** is the early exploratory notebook.
- **`Draft_Gems_Reports.ipynb`** is the qualitative scouting-report notebook.
- **`nfl_draft_gems.ipynb`** is the main final notebook and the best one to showcase.

If you want one notebook to lead with during a Bitcamp presentation, it should be **`nfl_draft_gems.ipynb`**. The other two are best presented as supporting work that helped shape the final idea.
