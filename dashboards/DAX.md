# Measures 

```dax
Age category
let
	AgeValue = try Number.From([age]) otherwise null,
	Band =
    	if AgeValue = null or AgeValue < 20 then "Unknown"
    	else if AgeValue <= 29 then "20-29"
    	else if AgeValue <= 39 then "30-39"
    	else if AgeValue <= 49 then "40-49"
    	else "50+"
in
	Band

Salary Category
let
	SalaryValue = try Number.From([salary]) otherwise null,
	Band =
    	if SalaryValue = null then "Unknown"
    	else if SalaryValue < 2500 then "<2500"
    	else if SalaryValue <= 3499 then "2501-3499"
    	else if SalaryValue <= 4499 then "3500-4499"
    	else ">4500"
in
	Band

Age percentage
AgePercentage =
DIVIDE(
	COUNT(YourTable[Age]),
	CALCULATE(COUNT(YourTable[Age]), ALL(YourTable))
) * 100


StdDev_Sample = STDEV.S(YourTable[Salary])


Total Age Count = COUNT(Employees[Age])

Create another table
Measures =
DATATABLE(
	"Key", INTEGER,
	{ { 1 } }
)

Sort for age
AgeSort =
SWITCH(
	TRUE(),
	Employees[Age] >= 20 && Employees[Age] <= 29, 1,
	Employees[Age] >= 30 && Employees[Age] <= 39, 2,
	Employees[Age] >= 40 && Employees[Age] <= 49, 3,
	4
)

For getting average salary. it applicable to other factors
Average Salary = AVERAGE('sample_data'[salary])
```
