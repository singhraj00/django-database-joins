
# 📊 SQL GROUP BY & Aggregation with Django ORM – Complete Guide

This repository explains how to use **SQL’s GROUP BY** and aggregation functions in real-world projects and how Django ORM handles these operations efficiently. It's a perfect reference for building reports, dashboards, or any application that needs to summarize or analyze data.

---

## ✅ What You’ll Learn

- 📂 What is `GROUP BY` in SQL and when it’s used  
- 🧮 Common aggregation functions like `COUNT()`, `SUM()`, `AVG()`, `MAX()`, `MIN()`  
- 🔑 How Django ORM uses `annotate()` and `aggregate()` for grouping and summarizing data  
- 🚀 Real-world examples like counting employees per department, calculating total salary, etc.

---

## 📚 GROUP BY in SQL

SQL’s `GROUP BY` groups rows based on a shared column and applies aggregation functions.

### Example:
```sql
SELECT department_id, COUNT(*)
FROM employee
GROUP BY department_id;
```
➡ Groups employees by department and counts how many are in each.

Common Functions:

✅ COUNT() – Counts the number of rows

✅ SUM() – Adds up numeric values

✅ AVG() – Finds the average value

✅ MAX() / MIN() – Finds the largest or smallest value



---

✅ How Django ORM Implements GROUP BY

Django abstracts SQL operations into ORM methods, so you don’t write raw SQL queries.

Example Models:

class Department(models.Model):
    name = models.CharField(max_length=100)

class Employee(models.Model):
    name = models.CharField(max_length=100)
    salary = models.DecimalField(max_digits=10, decimal_places=2)
    department = models.ForeignKey(Department, on_delete=models.SET_NULL, null=True)


---

✅ Example 1 – Count Employees per Department

from django.db.models import Count

departments = Department.objects.annotate(employee_count=Count('employee'))

for dept in departments:
    print(dept.name, dept.employee_count)

➡ Groups employees by department and counts them.


---

✅ Example 2 – Sum of Salaries per Department

from django.db.models import Sum

departments = Department.objects.annotate(total_salary=Sum('employee__salary'))

for dept in departments:
    print(dept.name, dept.total_salary)

➡ Calculates the total salary in each department.


---

✅ Example 3 – Average Salary per Department

from django.db.models import Avg

departments = Department.objects.annotate(avg_salary=Avg('employee__salary'))

for dept in departments:
    print(dept.name, dept.avg_salary)

➡ Finds the average salary for each department.


---

✅ Example 4 – Filter Based on Aggregation

departments = Department.objects.annotate(employee_count=Count('employee')) \
                                .filter(employee_count__gt=5)

for dept in departments:
    print(dept.name, dept.employee_count)

➡ Shows departments with more than 5 employees.


---

✅ Example 5 – Overall Summary with aggregate()

from django.db.models import Count

total_employees = Employee.objects.aggregate(total=Count('id'))

print("Total Employees:", total_employees['total'])

➡ Gives a summary across all records without grouping.


---

✅ Key Takeaways

✔ GROUP BY helps group data by one or more columns and apply aggregation
✔ Django ORM’s annotate() is equivalent to GROUP BY
✔ Aggregation functions like Count, Sum, Avg, etc., are used inside annotate() or aggregate()
✔ aggregate() is used for global summaries without grouping
✔ Combining filters and annotations makes complex data queries simple and efficient


---

📂 When to Use

✅ Reporting dashboards

✅ Analyzing user data, sales, and performance metrics

✅ Generating summaries for admin panels

✅ Filtering groups based on summary statistics



---

🚀 Ready to Level Up?

This guide is designed to give you both the theoretical understanding and practical Django ORM tools you need to master data summarization in your projects!

Feel free to ⭐ star this repository if it helped you!


---
