**Edge Case: Missing mark when creating student via POST /students**
When creating a student via POST /students, the 'mark' field is not optional. Store NULL in the database and exclude it from statistics (average, min, max).

Reason: This allows students to exist before marks are released, while keeping database statistics accurate by filtering out NULL values in the /stats endpoint.

**Edge Case: Missing required fields in POST /students**

When creating student via POST /students, if 'name' or 'course' missing, return 404 {"error": "name and course are required"}. 

Reason: Enforces data integrity for core student info.

**Edge Case: Invalid student ID in PUT /students/<id>**

When updating via PUT /students/<int:student_id>, if ID invalid (non-int), Flask auto-404s; if exists None, return 404 {"error": "student not found"}. 

Reason: Prevents invalid updates safely.

**Edge Case: Non-existent ID in DELETE /students/<id>**

When deleting via DELETE /students/<int:student_id>, if not found, return 404 {"error": "student not found"}. 

Reason: Avoids failures on wrong resources. 

**Edge Case: No marks in GET /stats**

When computing stats via GET /stats, if no valid marks (all NULL/empty), return {"count":0, "average":None, "min":None, "max":None}. 

Reason: Handles pre-mark release or empty data accurately.