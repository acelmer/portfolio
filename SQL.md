# SQL Database Schema
<p align="center">
<img src="https://github.com/acelmer/portfolio/assets/145276189/337687e5-131b-4cef-b341-50780a03600b" width=50% height=50%>
</p>

### Task 1 - Show patient_id, first_name, last_name from patients whose diagnosis is 'Dementia'.

```sql
SELECT patients.patient_id, first_name, last_name
FROM patients
JOIN admissions
ON patients.patient_id = admissions.patient_id 
WHERE diagnosis = 'Dementia'
```
### Task 2 - We are looking for a specific patient. Pull all columns for the patient who matches the following criteria:
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
### Task 3 - Show patient_id, first_name, last_name, and attending doctor's specialty. Show only the patients who has a diagnosis as 'Epilepsy' and the doctor's first name is 'Lisa'.

```sql
SELECT p.patient_id, p.first_name, p.last_name, d.specialty
FROM patients AS p
JOIN admissions AS a ON p.patient_id = a.patient_id
JOIN doctors AS d ON a.attending_doctor_id = d.doctor_id
WHERE diagnosis = 'Epilepsy' AND d.first_name = 'Lisa'
```
### Task 4 - All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password. The password must be the following, in order:
1. patient_id
2. the numerical length of patient's last_name
3. year of patient's birth_date

```sql
SELECT DISTINCT p.patient_id, concat(p.patient_id,len(last_name),year(birth_date)) AS temp_password
FROM patients AS p
JOIN admissions ON p.patient_id = admissions.patient_id
```
### Task 5 - Show the provinces that has more patients identified as 'M' than 'F'. Must only show full province_name.

```sql
SELECT province_name
FROM patients AS p
JOIN province_names AS p_n on p.province_id = p_n.province_id
GROUP BY province_name
HAVING
	COUNT( CASE WHEN gender = 'M' THEN 1 END) > COUNT( CASE WHEN gender = 'F' THEN 1 END)
```
