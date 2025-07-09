CREATE TABLE NHS_AE (
    Period VARCHAR(20),
    Org_Code VARCHAR(10),
    Org_Name VARCHAR(255),
    AE_Attendances_Type1 INT,
    AE_Attendances_Type2 INT,
    AE_Attendances_Other INT,
    Attendances_Over_4hrs_Type1 INT,
    Wait_4_to_12_hrs INT,
    Wait_Over_12_hrs INT,
    Emergency_Admissions_Type1 INT,
    Emergency_Admissions_Other INT,
    Month DATE
);

## 1. Total Attendances by Month

SELECT 
  FORMAT(Month, 'yyyy-MM') AS Month,
  SUM(AE_Attendances_Type1 + AE_Attendances_Type2 + AE_Attendances_Other) AS Total_Attendances
FROM NHS_AE
GROUP BY Month
ORDER BY Month;

## 2. Top 5 Trusts with Most Emergency Admissions
 
SELECT TOP 5 
  Org_Name,
  SUM(Emergency_Admissions_Type1 + Emergency_Admissions_Other) AS Total_Admissions
FROM NHS_AE
GROUP BY Org_Name
ORDER BY Total_Admissions DESC;

## 3. Trend of 12+ Hour Waits

SELECT 
  FORMAT(Month, 'yyyy-MM') AS Month,
  SUM(Wait_Over_12_hrs) AS Patients_12hr_Wait
FROM NHS_AE
GROUP BY Month
ORDER BY Month;






