# ![Digital Futures Academy](https://github.com/digital-futures-academy/DataScienceMasterResources/blob/main/Resources/datascience-notebook-header.png?raw=true)

## Activity 2: Write the Acceptance Criteria

**Time:** 20 minutes (3 to read Part 1, 12 to complete Part 2, 5 debrief)  
**Work in:** the same teams as Activity 1  
**You need:** the client's answers from Activity 0

This file has two parts:

- **Part 1** sets out the **Definition of Done**, which applies to every story, and the project's **quality and performance targets** (non-functional requirements agreed with the client).
- **Part 2** gives each user story its own **acceptance criteria**. Stories 1 and 2 are complete as worked examples. You fill the gaps in Stories 3 to 5, then write two of Story 6's criteria yourself.

> **Remember the rule:** if it applies to every story, it belongs in the Definition of Done. If it is specific to one story, it is an acceptance criterion. That is why the acceptance criteria below do not repeat the DoD.

---

## Part 1a: Definition of Done

Agreed by the whole delivery team with the Product Owner at the start of the project. **Every story** must meet all of these before it is done.

### Code quality

- [ ] Python passes `flake8` (PEP 8) with no errors.
- [ ] SQL passes `sqlfluff` linting, avoids `SELECT *` and uses meaningful aliases.
- [ ] Logic is in small, named functions; no copy-and-paste duplication.
- [ ] Errors are caught with `try`/`except`, logged with a clear message, and never silently ignored.
- [ ] No credentials or connection strings in code; they come from configuration.
- [ ] Code is reviewed and approved by at least one other team member.

### Testing

- [ ] Unit tests cover the new functions; integration tests cover the hand-offs between stages.
- [ ] All tests pass in the automated test run (CI), not only on a developer's machine.
- [ ] Test coverage is at least **90%** for the code changed in the story.
- [ ] Test data contains no real personal data.

### Data handling

- [ ] Every rejected or changed record is logged with the reason.
- [ ] Logs contain `customer_id` where needed, but never names or other personal data.

### Documentation

- [ ] Functions have docstrings; complex logic has comments.
- [ ] The README and any pipeline diagrams reflect the change.

### Acceptance

- [ ] All of the story's acceptance criteria are met.
- [ ] The story is demonstrated to, and accepted by, the Product Owner.

---

## Part 1b: Quality and Performance Targets

These are **non-functional requirements** agreed with the client. They are not part of the DoD, because each one applies to particular stories. Acceptance criteria quote them where relevant.

### Performance

| Operation | Target |
|---|---|
| Database extraction (10,500 rows, 4 fields) | Under 1 minute |
| CSV extraction (5,200 rows, 5 columns) | Under 30 seconds |
| Cleaning | Under 1 second per 1,000 rows |
| Joins and aggregations | Under 5 seconds per 10,000 rows |
| Loading | Under 5 seconds per 10,000 rows |
| Full end-to-end run | Under 30 minutes |

### Data quality

| Measure | Target |
|---|---|
| Accuracy | At least 99% of sampled records match a manual recalculation from source (error rate no more than 1%) |
| Duplicates | 0% remain after cleaning |
| Missing or invalid values | 100% handled by an agreed rule (removed, defaulted or set to null) and logged |
| Completeness | 100% of expected columns present |
| Consistency | 100% of values in the agreed format (for example, ISO 8601 dates) |

### Reliability, privacy and security

| Measure | Target |
|---|---|
| Re-running | Running the pipeline twice gives an identical result |
| Failure | A failed run leaves the previous output intact and is reported |
| Data minimisation | Only the columns the analysis needs reach the target table |
| Access | `customer_summary` is readable by the analytics team only |

---

## Data structure

The `transactions` table has these fields:

```csv
transaction_id,customer_id,transaction_date,amount
```

The `customers.csv` file has these headings:

```csv
customer_id,name,age,country,is_active
```

The target table `customer_summary` has these columns:

```csv
customer_id,age,country,total_spent,avg_transaction_value,transaction_count
```

---

## Part 2: Acceptance Criteria per Story

Fill each `___` in Stories 3 to 5 using the client's answers (Activity 0), the targets in Part 1b and the data structure above. For Story 6, write the two missing criteria in full. Be ready to justify each value.

---

### Story 1: Extract transactions (worked example)

```text
As a Data Analyst,
I want the transaction data extracted from the SQL database,
so that it can be cleaned and joined with the customer data.
```

- [ ] Given the `transactions` table holds 10,500 rows with 4 fields, when the data is extracted, then all 10,500 rows and the fields `transaction_id`, `customer_id`, `transaction_date` and `amount` are returned.
- [ ] Given the same table, when the data is extracted, then extraction completes in under 1 minute.
- [ ] Given the database is unreachable, or the query fails or times out, when extraction runs, then the error is logged and the pipeline stops without producing partial output.

### Story 2: Extract customers (worked example)

```text
As a Data Analyst,
I want the customer data extracted from customers.csv,
so that it can be cleaned and joined with the transaction data.
```

- [ ] Given `customers.csv` holds 5,200 rows with 5 columns, when the file is extracted, then all 5,200 rows and the columns `customer_id`, `name`, `age`, `country` and `is_active` are returned.
- [ ] Given the same file, when it is extracted, then extraction completes in under 30 seconds.
- [ ] Given the file is missing, cannot be decoded, or its headers do not match, when extraction runs, then the error is logged and the pipeline stops without producing partial output.

---

### Story 3: Clean transactions

```text
As a Data Scientist,
I want the transaction data cleaned and standardised,
so that I can trust the spend figures.
```

- [ ] Given extracted transactions in mixed date formats, when they are cleaned, then every `transaction_date` is in ISO 8601 (YYYY-MM-DD) format.
- [ ] Given two or more rows share a `transaction_id`, when the data is cleaned, then only one remains and 0% duplicates are left.
- [ ] Given a row with a missing or non-numeric `amount`, or a missing `customer_id`, when the data is cleaned, then the row is removed and the reason is logged.
- [ ] Given a row with a negative `amount`, when the data is cleaned, then the row is kept, because negative amounts are not within valid range.
- [ ] Given 10,500 extracted rows, when they are cleaned, then cleaning completes in under 10.5 seconds.

### Story 4: Clean customers

```text
As a Data Scientist,
I want the customer data cleaned and standardised,
so that I can trust the demographic fields.
```

- [ ] Given two or more rows share a `customer_id`, when the data is cleaned, then the first occurrence is kept and the others are logged.
- [ ] Given `is_active` values such as "Yes", "TRUE" or "1", when the data is cleaned, then every `is_active` value is a boolean (true or false).
- [ ] Given an `age` that is missing or outside 18 to 100, when the data is cleaned, then `age` is set to null and the customer is kept.
- [ ] Given a `country` with extra spaces or mixed case, when the data is cleaned, then it is trimmed and in title case; a missing country becomes "Unknown".
- [ ] Given 5,200 extracted rows, when they are cleaned, then cleaning completes in under 5.2 seconds.

### Story 5: Combine and enrich

```text
As the Marketing Manager,
I want a list of active customers who have spent more than $500, with their total spend, average transaction value, age and country,
so that I can target high-value customers with rewards and understand who they are.
```

- [ ] Given cleaned transactions and customers, when they are joined on `customer_id`, then transactions with no matching customer are excluded and their count is logged.
- [ ] Given the joined data, when it is filtered, then only customers with `is_active` = true remain.
- [ ] Given the joined data, when spend is calculated, then `total_spent` equals the sum of `amount` for each `customer_id`, including refunds.
- [ ] Given the joined data, when spend is calculated, then `avg_transaction_value` equals `total_spent` divided by `transaction_count`.
- [ ] Given the enriched data, when high-value customers are selected, then only customers with `total_spent` greater than 500 remain, and a customer with exactly \$500.00 is excluded.
- [ ] Given the final dataset, when its columns are checked, then they are exactly the six `customer_summary` columns, and `name` is not present.
- [ ] Given a random sample of 20 customers, when their figures are recalculated by hand from source, then at least 99% match.

### Story 6: Store and refresh

```text
As a Data Scientist,
I want the result stored in a customer_summary SQL table that I can safely reset or refresh,
so that I can repeat and update my analysis.
```

- [ ] Given the transformed dataset, when it is loaded, then the row count in `customer_summary` equals the row count of the transformed dataset.
- [ ] Given the transformed dataset, when it is loaded, then loading completes in under 5 seconds per 10,000 rows.
- [ ] Given the full pipeline, when it runs end to end, then it completes in under 30 minutes.

**Write these two criteria yourself**, in Given / When / Then form:

1. **Re-running:** what must be true if the pipeline runs a second time with the same sources?
2. **Failure:** what must be true if a load fails part-way?

```text
Re-running:
Given the pipeline has already run,
when it is run again with the same sources,
then `customer_summary` is identical and no `customer_id` appears more than once

Failure:
Given a load fails part-way
when the failure is detected
then the previous version of `customer_summary` remains and the failure is reported
```

---

### Debrief questions

1. **Why don't the acceptance criteria mention code review, linting or test coverage?** they apply to every story, so they live in DoD, repeating them in each story's criteia hides what is genuinely specific to that story
2. **Which criteria came from the client's answers rather than the targets in Part 1b? What would you have written without Activity 0?** the refun rule, the exactly $500 boundary, the duplicate definitions, age range, "Unkown" for country, excluding unmatched transactions, and dropping `name`, without activity 0, each would have been a guess, and several would change which customers appear in the output
3. **Why does Story 5 check that `name` is **not** present?** data minimisation, the analysis does not need names, so the pipeline must not copy them intoo the target table, a test that checks for absence stops someone adding the column back later without a decision
4. **Compare your two Story 6 criteria with another team's. Would both give a clear pass or fail?**
