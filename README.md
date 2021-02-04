# MVP
SQL Query Property Analysis Part 1
--1) Display a list of all property names and their property id’s for Owner Id: 1426. 

select P.Id Property_ID, P.Name Property_Name, O.OwnerId from Property p
join ownerProperty O 
ON O.Id = P.Id
where O.OwnerId= 1426

--1b) Display the current home value for each property in question a

select P.Id Property_ID, P.Name Property_Name, O.OwnerId, PV.Value from Property p
 join ownerProperty O 
ON O.Id = P.Id
 join PropertyHomeValue PV 
ON O.PropertyId = PV.PropertyId
where O.OwnerId= 1426

--1c)For each property in question a), return the following:                                                                      
--Using rental payment amount, rental payment frequency, tenant start date and tenant 
--end date to write a query that returns the sum of all payments from start date to end date. 
 

--1ci)

select P.Id Property_ID, P.Name Property_Name, O.OwnerId, PV.Value, PRP.Amount, PRP.FrequencyType, PRP.Amount*PRP.FrequencyType AS Annual_income, TP.StartDate, TP.EndDate from Property p
join ownerProperty O 
ON O.Id = P.Id
 join PropertyHomeValue PV 
ON O.PropertyId = PV.PropertyId
join PropertyRentalPayment PRP
on PRP.PropertyId = O.PropertyId
 join TenantProperty TP
ON TP.PropertyId = O.PropertyId
where O.OwnerId= 1426


--1cii)
--Display the yield.

select P.Id Property_ID, P.Name Property_Name, O.OwnerId, PV.Value, PRP.Amount, PRP.FrequencyType, PRP.Amount*PRP.FrequencyType AS Annual_income, ((PRP.Amount*PRP.FrequencyType)/PV.Value)*100 as Yield,TP.StartDate, TP.EndDate from Property p
join ownerProperty O 
ON O.Id = P.Id
 join PropertyHomeValue PV 
ON O.PropertyId = PV.PropertyId
join PropertyRentalPayment PRP
on PRP.PropertyId = O.PropertyId
 join TenantProperty TP
ON TP.PropertyId = O.PropertyId
where O.OwnerId= 1426


--1d)
--Display all the jobs available

SELECT * FROM [dbo].[Job] where JobStatusId = 1 or JobStatusId= 2


--1E)
--Display all property names, current tenants first and last names and rental payments per week/ fortnight/month 
--for the properties in question a). 

select * from Person
select P.Id Property_ID, P.Name Property_Name, O.OwnerId, PRSN.FirstName AS Tenant_FNAME, PRSN.LastName As Tenant_LNAME, PRP.Amount , PRP.FrequencyType from Property p
join ownerProperty O 
ON O.Id = P.Id
join Person PRSN
ON PRSN.Id = O.Id
join PropertyRentalPayment PRP
ON O.PropertyId= PRP.PropertyId
where O.OwnerId= 1426
