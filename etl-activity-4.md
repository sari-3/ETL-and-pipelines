# ![Digital Futures Academy](https://github.com/digital-futures-academy/DataScienceMasterResources/blob/main/Resources/datascience-notebook-header.png?raw=true)

## Activity 4: Plan the Tests for a User Story

**Time:** 20 minutes (15 to work, 5 debrief)  
**Work in:** individually or in pairs

To decide which tests a story needs, start from:

1. the user story
2. its acceptance criteria (Activity 2)
3. the Definition of Done (Activity 2, Part 1a)
4. the test data you will use, which must contain no real personal data

Each test belongs to one of five categories. The first four come from the story's acceptance criteria; the fifth comes from the Definition of Done.

| Category | What it proves | Comes from |
|---|---|---|
| Functional | The story does what it should | Acceptance criteria |
| Performance | It meets the speed target | Acceptance criteria (quoting the targets in Part 1b) |
| Data quality | The data is complete and accurate | Acceptance criteria |
| Error handling | Failures are caught, logged and stop the run safely | Acceptance criteria |
| DoD checks | The work meets the team's quality bar | Definition of Done |

Write every test in **Given / When / Then** form, and note its **level**: unit (one function), integration (components together) or end-to-end (the whole pipeline).

---

### Worked example: Story 1, extract transactions

```text
As a Data Analyst,
I want the transaction data extracted from the SQL database,
so that it can be cleaned and joined with the customer data.
```

**Functional (integration)**

- [ ] Given the `transactions` table holds 10,500 rows with 4 fields, when the data is extracted, then the result has exactly 10,500 rows.
- [ ] Given the same table, when the data is extracted, then the result has exactly the columns `transaction_id`, `customer_id`, `transaction_date` and `amount`.

**Performance (integration)**

- [ ] Given the `transactions` table holds 10,500 rows with 4 fields, when the data is extracted, then extraction completes in under 1 minute.

**Data quality (integration)**

- [ ] Given a fixed sample of 20 `transaction_id`s, when the extracted rows are compared with the same rows queried directly from the database, then every value matches.

**Error handling (integration)**

- [ ] Given the database is unreachable, when extraction runs, then a connection error is caught, logged, and the pipeline stops without output.
- [ ] Given the query is invalid, when extraction runs, then a query error is caught, logged, and the pipeline stops without output.
- [ ] Given the query exceeds its time limit, when extraction runs, then a timeout error is caught, logged, and the pipeline stops without output.

> These are integration tests because they need a database to fail against; testing them at unit level would mean faking the database. A file is different: you can create a missing or badly encoded test file yourself, so file errors can be unit tests.

**DoD checks (automated in CI)**

- [ ] Given the SQL files, when they are linted with `sqlfluff`, then they pass.
- [ ] Given the Python files, when they are linted with `flake8`, then they pass.
- [ ] Given the full test suite runs, when coverage is measured, then the extraction module is at least 90% covered.

---

### Your turn: Story 2, extract customers

```text
As a Data Analyst,
I want the customer data extracted from customers.csv,
so that it can be cleaned and joined with the transaction data.
```

Its acceptance criteria (from Activity 2):

- Given `customers.csv` holds 5,200 rows with 5 columns, when the file is extracted, then all 5,200 rows and the columns `customer_id`, `name`, `age`, `country` and `is_active` are returned.
- Given the same file, when it is extracted, then extraction completes in under 30 seconds.
- Given the file is missing, cannot be decoded, or its headers do not match, when extraction runs, then the error is logged and the pipeline stops without producing partial output.

Write at least one test for each category. Think about what can go wrong with a **file** that cannot go wrong with a database, such as a missing file, the wrong delimiter or encoding, renamed headers, or malformed rows.

**Functional (level: ___)**

- [ ] Given ..., when ..., then ...

**Performance (level: ___)**

- [ ] Given ..., when ..., then ...

**Data quality (level: ___)**

- [ ] Given ..., when ..., then ...

**Error handling (level: ___)**

- [ ] Given ..., when ..., then ...

**DoD checks**

- [ ] Given ..., when ..., then ...

---

### Debrief

- Which of your tests differ from Story 1, and why?
- Which category had no equivalent for a CSV file?
- Your test file of sample customers: where will it come from, given the DoD bans real personal data?
