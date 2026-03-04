# Edge Case: Missing mark when creating student

When creating a student via POST /students, the `mark` field is optional.
If `mark` is not provided, we store `NULL` in the database and exclude it
from statistics (average, min, max).

Reason: This allows students to exist before marks are released, while keeping