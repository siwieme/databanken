# Relational Databases FAQ Summary

## Series 1: Basic Functionality

### General Tips
- **Read Carefully**: Misinterpretation of assignments often leads to errors (e.g., confusing “decade” with “century” or “rounding down” vs. “rounding”).
- **Error Messages**: PostgreSQL error messages may not fully indicate the cause, so deeper troubleshooting is often needed.
- **Readability**: Using uppercase for keywords like `SELECT`, `FROM`, `WHERE` enhances readability but isn’t required for execution.
- **Unique Column Names**: Queries should ensure unique column names, as required for Dodona’s result comparison.
- **Query Optimization**: Different solutions may vary in efficiency; practicing various methods improves skills.

### Exercises Overview
1. **Operators**: Understand the distinctions among `=`, `LIKE`, and `ILIKE`.
    * `=`: Exact match.
    * `LIKE`: Case-sensitive pattern matching.
    * `ILIKE`: Case-insensitive pattern matching.
2. **Boolean Operators**: Familiarize yourself with De Morgan’s laws.
    * `NOT (A AND B) = (NOT A) OR (NOT B)`
    * `NOT (A OR B) = (NOT A) AND (NOT B)`
3. **Concatenation**: Combine first and last names using `CONCAT` or `||`.
4. **Conditional Logic**: Use `CASE` expressions for conditional logic in `SELECT`.
    * `CASE WHEN condition THEN result ELSE alternative END`
5. **Array Functions**: Use `array_length`, `string_to_array`, and `unnest` effectively.
    * `array_length`: Determine the length of an array.
    * `string_to_array`: Convert a string to an array.
    * `unnest`: Expand an array into rows.
6. **String Manipulation**: Practice avoiding unnecessary characters in string manipulations.
7. **Math Functions**: Understand rounding functions, and choose the appropriate one (`round`, `trunc`, `ceil`, `floor`).
    * `round`: Round to the nearest integer: `round(3.5) = 4`.
    * `trunc`: Truncate to the specified decimal places: `trunc(3.5) = 3`.
    * `ceil`: Round up to the nearest integer: `ceil(3.1) = 4`.
    * `floor`: Round down to the nearest integer: `floor(3.9) = 3`.
8. **Range Checks**: `BETWEEN` operator for checking within ranges.
9. **Distinct Rows**: Utilize `DISTINCT` to avoid duplicate rows in result tables.
10. **String Selection**: Efficiently select parts of strings using functions like `mod` for specific requirements.

---

## Series 2: Joining Multiple Tables

### General Tips
- **Choosing the Right Join**: Most queries require `INNER JOIN`, especially when using foreign key references.
    * `INNER JOIN`: Returns rows with matching values in both tables.
    * `LEFT JOIN`: Returns all rows from the left table and matching rows from the right table.
    * `RIGHT JOIN`: Returns all rows from the right table and matching rows from the left table.
    * `FULL JOIN`: Returns rows when there is a match in either table.
- **NULL Checks**: Use `LEFT JOIN` with `IS NULL` in `WHERE` to identify records without corresponding entries in another table.
- **Avoiding Full Joins**: `CROSS JOIN` and `FULL JOIN` are rare due to high processing requirements.
- **Table Aliases**: Aliases improve readability, especially when self-joining or using the same table multiple times.

### Exercises Overview
1. **Conditional Joins**: For queries requiring absent data (e.g., songs without a presenter), use `LEFT JOIN` with `IS NULL`.
2. **Self-Joins**: Use self-joins to pair rows based on conditions like name similarity.
3. **Composite Keys**: Ensure correct join conditions when working with composite keys.
4. **Nineties Range Check**: Verify if a year falls between 1990 and 1999 using math functions.

---

## Series 3: Subqueries

### General Tips
- **Subquery Types**: Familiarize with subqueries in `WHERE`, `FROM`, and `SELECT` clauses; scalar and correlated subqueries are essential here.
    * `WHERE`: Filter rows based on subquery results.
    * `FROM`: Create a temporary table for further processing.
    * `SELECT`: Retrieve a single value for comparison.
- **Use of `IN`, `EXISTS` Operators**: Effective when working with conditional data retrieval.
    * `IN`: Checks if a value matches any value in a subquery.
    * `EXISTS`: Checks if a subquery returns any rows.
- **Ordering and Limiting**: Use `ORDER BY` and `LIMIT` to retrieve the top results, but note that `LIMIT` may omit ties.
- **Exploring Alternative Solutions**: Practicing multiple solutions strengthens understanding and SQL skills.

### Exercises Overview
1. **Join and Subquery Options**: Use either `JOIN` or subqueries with `NOT IN`, `NOT EXISTS`, etc., for conditional filtering.
2. **Aggregation Functions**: Select specific values (e.g., youngest date) with aggregation.
3. **Complex Queries**: Use subqueries to filter based on conditions like genre, radio show types, or specific presenter conditions.
4. **Unnesting Data**: Handle arrays by creating intermediate tables, and avoid unnesting within `WHERE` or `JOIN` clauses.

---

Each series covers progressively more complex SQL concepts, with Series 1 focusing on basics, Series 2 on multi-table joins, and Series 3 on subqueries. The documents encourage experimenting with various methods to gain a deep understanding of relational databases and SQL queries.
