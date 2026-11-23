# ![Digital Futures Academy](https://github.com/digital-futures-academy/DataScienceMasterResources/blob/main/Resources/datascience-notebook-header.png?raw=true)

## Activity 0: Question the Brief

**Time:** 12 minutes (7 in teams, 5 with the client)  
**Work in:** teams of three to five

A consultant never builds straight from a brief. Every brief leaves gaps, and if you fill them with assumptions you may build the wrong dataset. Your job in this activity is to find those gaps before any user stories are written.

---

### The client brief

> A client needs a robust ETL pipeline that integrates **transaction data from a SQL database** with **customer demographic data from a CSV file**. The data must be cleaned, standardised and enriched, keeping only **active customers who have spent over \$500**, so that the client can target high-value customers with relevant marketing and rewards. The business also wants insight into the **age and country** profile of these customers. The result must be stored in a **SQL table** that can be **reset or updated regularly**.

### The data

| Source | Format | Fields | Volume |
|---|---|---|---|
| `transactions` | SQL database table | `transaction_id`, `customer_id`, `transaction_date`, `amount` | 10,500 rows |
| `customers.csv` | CSV file | `customer_id`, `name`, `age`, `country`, `is_active` | 5,200 rows |

Known data-quality problems: missing values, duplicates, inconsistent formats, invalid entries, and customers who appear in one source but not the other.

---

### Your task

1. **Write at least five questions** you would ask the client before building anything. Use the four categories below to make sure you cover the ground.
2. **Label each question** as **F** (functional: *what* the pipeline does) or **NF** (non-functional: *how well* it does it, including privacy and security).
3. **Star your top two:** the questions whose answers would most change what you build.

Your trainer will then play the client. Each team asks its two starred questions in turn, skipping any that another team has already asked. You will get the full answer sheet afterwards.

| Category | Prompts to get you started |
|---|---|
| **Business rules** | What exactly does "spent over \$500" mean? What makes a customer "active"? |
| **Data** | What counts as a duplicate? What should happen to bad or missing values? |
| **Operations** | How often is "regularly"? Who runs the pipeline? What happens if it fails? |
| **People and privacy** | Who will use the output? Does it need everything in the source, including names? |

---

### Your questions

| # | Question | Category | F / NF | Top 2? |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |

---

### Debrief

- Which of your questions would have caused the most rework if you had guessed the answer?
- The brief includes names and ages. What does that mean for how you design and test the pipeline?

Keep the client's answers: you will use them in Activities 1 to 4.
