# SQL Database Schema
<img src="https://github.com/acelmer/portfolio/assets/145276189/337687e5-131b-4cef-b341-50780a03600b" width=50% height=50%>

## Task 1 - Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.

```sql
SELECT patients.patient_id, first_name, last_name
FROM patients
JOIN admissions
ON patients.patient_id = admissions.patient_id 
WHERE diagnosis = 'Dementia'
```
## Task 2 - We are looking for a specific patient. Pull all columns for the patient who matches the following criteria:
- First_name contains an 'r' after the first two letters.
- Identifies their gender as 'F'
- Born in February, May, or December
- Their weight would be between 60kg and 80kg
- Their patient_id is an odd number
- They are from the city 'Kingston'

```sql
SELECT *
FROM patients
WHERE first_name LIKE '__r%' 
AND gender = 'F' 
AND month(birth_date) IN (2, 5, 12) 
AND weight between 60 AND 80 
AND patient_id % 2 = 1 
AND city = 'Kingston'
```
