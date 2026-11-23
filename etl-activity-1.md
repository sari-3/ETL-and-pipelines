# ![Digital Futures Academy](https://github.com/digital-futures-academy/DataScienceMasterResources/blob/main/Resources/datascience-notebook-header.png?raw=true)

## Activity 1: Identify the User Stories

**Time:** 20 minutes (15 in teams, 5 debrief)  
**Work in:** teams of three to five  
**You need:** the client's answers from Activity 0

### Instructions

Turn the requirements below into user stories. The requirements fall into three **epics**: Extract, Transform and Load. Break each epic into one or more stories using this format:

```text
As a [role],
I want [goal],
so that [benefit].
```

Two rules:

- **One role per story.** Name the person who gets the value: a Data Analyst, a Data Scientist or the Marketing Manager. Avoid combined roles such as "Data Analyst/Scientist".
- **Keep the "so that".** It tells the team *why*, which is what lets them make sensible decisions when details are unclear.

---

### Key requirements

**Data Analysts and Data Scientists need:**

- the transaction and customer data brought into the pipeline from both sources
- assurance that the data is clean, consistent and accurate
- a single dataset combining transaction and demographic data
- the result stored in a SQL table for analysis
- to be able to reset or update the data to repeat the analysis

**The Marketing Manager (business stakeholder) needs:**

- the **active** customers who have spent **more than $500**, so they can be targeted with rewards
- each high-value customer's **age** and **country**, so analysts can report on trends

| Epic | What it delivers |
|---|---|
| Epic 1: Extract | Transaction and customer data brought into the pipeline from both sources |
| Epic 2: Transform | Each source cleaned, then combined into a single enriched dataset. Cleaning is the first part of Transform. |
| Epic 3: Load | The final dataset stored in a SQL table that can be safely reset or updated |

---

### User stories

#### Epic 1: Extract

> **Hint:** you have two data sources, and each needs its own extraction.

```text
As a Data Analyst,
I want the transaction and customer data,
so that I can analyse transaction pattern for each customer or compare with other customers
```

```text
As a Data Analyst,
I want an easily readable single dataset containing the combined transaction and demographic data,
so that I can easily analyse the reults and be able to reset or update the data as needed.
```

```text
As a Data Analyst,
I want consistent and accurate data,
so that I can accurately measure customer statistics
```

```text
As a ,
I want ,
so that 
```
---

#### Epic 2: Transform

> **Hint:** clean each extracted source separately (two stories), then combine them (one story).  
> **Think:** who gets the value from the combined, filtered dataset?

```text
As a Data Analyst,
I want the final dataset stored in a SQL table that can be safely reset or updated,
so that I can repeat the analysis on fresh data without creating duplicates.
```

```text
As a Marketing Manager, 
I want to identify active customers who have spent over $500 
so that I can target them with relevant marketing campaigns and rewards.
```

```text
As a ,
I want ,
so that 
```

---

#### Epic 3: Load

```text
As a ,
I want ,
so that 
```

> **Discuss:** Load has only one story. Is it really an epic? Write one sentence explaining your view.

---

### You should finish with

- Six user stories across three epics, each with a single role
- One sentence on whether Load is an epic, and why
