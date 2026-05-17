# Remediation Scoring Model for Database Migrations

The **Remediation Scoring Model** is a quantitative framework designed to estimate the engineering effort required to remediate incompatible code, queries, operations, and architectural constructs during database migrations.

The methodology provides a repeatable and structured approach for evaluating migration complexity across applications, modules, or workloads.

---

# Overview

Database migrations are rarely simple "lift-and-shift" exercises. Even when compatibility layers or automated conversion tools exist, workloads often contain unsupported operations, incompatible logic, or architectural assumptions that require remediation.

The Remediation Scoring Model provides:

- A repeatable method for estimating remediation effort
- A standardized classification system
- A normalization approach for comparing workloads of different sizes
- A practical spreadsheet toolkit with built-in charts and radar graphs

---

# Core Concepts

## Remediation Task Classification

Tasks are categorized into three remediation levels:

| Level  | Description |
|--------|-------------|
| Easy   | Minimal code changes or direct compatibility |
| Medium | Query rewrites or moderate logic translation |
| Hard   | Architectural redesign or unsupported features |

---

# Remediation Score Formula

```math
Remediation\ Score = (w_E \times n_E) + (w_M \times n_M) + (w_H \times n_H)
```

Where:

| Variable | Description |
|----------|-------------|
| `w_E` | Weight assigned to Easy remediation tasks |
| `w_M` | Weight assigned to Medium remediation tasks |
| `w_H` | Weight assigned to Hard remediation tasks |
| `n_E` | Number of Easy remediation tasks |
| `n_M` | Number of Medium remediation tasks |
| `n_H` | Number of Hard remediation tasks |

---

# Example

Assume the following workload analysis:

| Complexity | Weight (hours) | Count |
|------------|----------------|-------|
| Easy       | 1              | 20 |
| Medium     | 3              | 10 |
| Hard       | 8              | 5 |

Then:

```math
Remediation\ Score = (1 \times 20) + (3 \times 10) + (8 \times 5)
```

```math
= 20 + 30 + 40 = 90\ hours
```

---

# Normalized Remediation Score

Large workloads naturally produce higher raw scores. To compare workloads fairly, normalization is used.

## Formula

```math
Normalized\ Score = \frac{Remediation\ Score}{Total\ Number\ of\ Fixes}
```

Or:

```math
Normalized\ Score =
\frac{
(n_E \times w_E) + (n_M \times w_M) + (n_H \times w_H)
}{
n_E + n_M + n_H
}
```

---

# Why Normalize?

Normalization allows teams to compare workloads fairly regardless of size.

Example:

| System | Raw Score | Total Fixes | Normalized Score |
|--------|-----------|-------------|------------------|
| System A | 90 | 30 | 3.0 |
| System B | 90 | 90 | 1.0 |

Although both systems require the same total effort, System A has significantly more complex remediation work per issue.

---

# Remediation Examples

## Easy Remediation

### Source Query

```javascript
find({ status: "ACTIVE" })
```

### Equivalent Query

```sql
SELECT *
FROM records
WHERE status = 'ACTIVE';
```

Minimal or no remediation required.

---

## Medium Remediation

### Aggregation Logic

```javascript
aggregate([
  { $group: { _id: "$region", count: { $sum: 1 } } }
])
```

### Equivalent SQL

```sql
SELECT region, COUNT(*)
FROM records
GROUP BY region;
```

Requires translation from one query paradigm to another.

---

## Hard Remediation

### Architectural Feature Replacement

Examples include:

- Time-based data expiration
- Multi-system joins
- Deeply nested hierarchical structures
- Dynamic schema redesign
- Event-driven data lifecycle management

These tasks often require:

- Data model redesign
- Scheduling frameworks
- Stored procedures
- Partitioning strategies
- ETL or transformation pipelines

Represents architectural remediation.

---

# Spreadsheet Features

The Excel toolkit includes:

- Editable remediation weights
- Built-in formulas
- Bar charts
- Spider/radar graphs
- Normalized score calculations

---

# Use Cases

- Migration assessments
- Migration planning workshops
- Engineering effort estimation
- Migration prioritization
- Architecture reviews
- Executive reporting


---

# Related Concepts

- Migration Viability Score
- Database modernization methodologies
- Migration planning frameworks
- Workload assessment models

---

# Author

Matt DeMarco

- Blog post: [https://oramatt.com](https://oramatt.com/2025/07/10/remediation-scoring-model-bringing-precision-to-migration-complexity/)
- GitHub: https://github.com/oramatt

---

# License

See license file

