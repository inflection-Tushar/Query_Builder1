```few shots or queries related to biometrics_body_temperature table ```
|sr|text|Query|
|:-|:---|:----|
|1.|give me the last month body temperature for this patient id|- SELECT * FROM biometrics_body_temperature WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= NOW() - INTERVAL 1 MONTH;|
|2.|what is my body temperature yesterday|- SELECT BodyTemperature FROM biometrics_body_temperature WHERE PatientUserId = 'patient_uuid_here' AND DATE(RecordDate) = CURDATE() - INTERVAL 1 DAY;|
|3.| give me my highest body temperature in this weak|- SELECT MAX(BodyTemperature) AS HighestBodyTemperature FROM biometrics_body_temperature WHERE PatientUserId = 'patient_uuid_here' AND YEARWEEK(RecordDate, 1) = YEARWEEK(CURDATE(), 1);|
|4.|give the total records from this table|- SELECT COUNT(*) AS TotalRecords FROM biometrics_body_temperature;|

<!-- few shots or queries related to biometrics_body_height table -->


|5.|give me the total records of height for the particular id |- SELECT COUNT(*) AS TotalHeightRecords FROM biometrics_body_height WHERE PersonId = 'person_uuid_here';|

|6.|what is the highest body temperature in last week for particular id|- SELECT MAX(BodyTemperature) AS HighestBodyTemperature FROM biometrics_body_temperature WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 WEEK;|

|7.|give the history of height for last month for particular id |- SELECT * FROM biometrics_body_height WHERE PersonId = 'person_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 MONTH;|



``` few shots or queries related to biometrics_blood_pressure table ```

|8.| give me the blood pressure history for last month for the particular patient id | - SELECT * FROM biometrics_blood_pressure WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 MONTH;|

|9.|notice the high blood pressure in last week for particular patient id | - SELECT * FROM biometrics_blood_pressure WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 WEEK AND (Systolic > your_high_threshold OR Diastolic > your_high_threshold);|

|10.| give the total patient who check the blood pressure |- SELECT COUNT(DISTINCT PatientUserId) AS TotalPatients FROM biometrics_blood_pressure;|

|11.| give the updated time for this patient id |- SELECT MAX(UpdatedAt) AS LatestUpdateTime FROM biometrics_blood_pressure WHERE PatientUserId = 'patient_uuid_here';|



``` few shots or queris related to biometrics_blood_oxygen_saturation table ```
 
|12.|give me the last month history of oxygen level in blood for particular id |-SELECT * FROM biometrics_blood_oxygen_saturation WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 MONTH;|
|13.| give me the lowest level of oxygen is noticed for particular id |-SELECT MIN(BloodOxygenSaturation) AS LowestOxygenLevel FROM biometrics_blood_oxygen_saturation WHERE PatientUserId = 'patient_uuid_here';|
14.
    <!-- give me the highest oxygen level is noticed for particular id -->
    - SELECT MAX(BloodOxygenSaturation) AS HighestOxygenLevel FROM biometrics_blood_oxygen_saturation WHERE PatientUserId = 'patient_uuid_here';
15.
    <!-- total who check the oxygen level in blood -->
    - SELECT COUNT(DISTINCT PatientUserId) AS TotalPatients FROM biometrics_blood_oxygen_saturation;


<!-- few shots or queries related to biometrics_blood_glucose table -->

1.
    <!-- highest blood pressure noticed for particular id -->
    - SELECT MAX(BloodGlucose) AS HighestBloodGlucose FROM biometrics_blood_glucose WHERE PatientUserId = 'patient_uuid_here';
2.
    <!-- give the hostory of last month glucose for particular id -->
    - SELECT * FROM biometrics_blood_glucose WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 MONTH;
3. 
    <!-- total patient who check glucose in blood -->
    - SELECT COUNT(DISTINCT PatientUserId) AS TotalPatients FROM biometrics_blood_glucose;


<!-- few shots or queries related to biometrics_blood_cholesterol table -->

1.
    <!-- give me the record where i have a risk of heart attack using hdl and ldl for particular id -->
    - SELECT * FROM biometrics_blood_cholesterol WHERE PatientUserId = 'patient_uuid_here' AND (HDL < your_hdl_threshold OR LDL > your_ldl_threshold);

2.
    <!-- last time highest cholesterol -->
    - SELECT * FROM biometrics_blood_cholesterol WHERE PatientUserId = 'patient_uuid_here' ORDER BY TotalCholesterol DESC LIMIT 1;

3.
    <!-- give the history of a cholesterol for this patient id -->
    - SELECT * FROM biometrics_blood_cholesterol WHERE PatientUserId = 'patient_uuid_here' ORDER BY RecordDate DESC;



<!-- few shots or queries related to biometrics_body_weight table -->

1. 
    <!-- highest body weight noticed for this patient id -->
    - SELECT * FROM biometrics_body_weight WHERE PatientUserId = 'patient_uuid_here' ORDER BY BodyWeight DESC LIMIT 1;
2.
    <!-- give the history of body weight for particular id -->
    - SELECT * FROM biometrics_body_weight WHERE PatientUserId = 'patient_uuid_here' ORDER BY RecordDate DESC;

3. 


<!-- few shots or queries related to blood_donation_volunteers table -->
 
 1.
    <!-- give the selected blood groups -->
    - SELECT DISTINCT SelectedBloodGroup FROM blood_donation_volunteers WHERE IsAvailable = 1; -- Optional condition to filter by availability

2.
    <!-- give the mobile number of volunteers -->
    - SELECT SelectedPhoneNumber FROM blood_donation_volunteers WHERE IsAvailable = 1; -- Optional condition to filter by availability

3.
    <!-- give the blood groups available in the table -->
    - SELECT DISTINCT BloodGroup FROM blood_donation_volunteers WHERE IsAvailable = 1; -- Optional condition to filter by availability


<!-- few shots or queries related to blood_donors table -->

1. 
    <!-- donors who are available for this blood group -->
    - SELECT * FROM blood_donors WHERE BloodGroup = 'desired_blood_group' AND IsAvailable = 1;
2.
    <!-- give the donor for particular AcceptorUserId -->
    - SELECT * FROM blood_donors WHERE AcceptorUserId = 'desired_acceptor_user_id';

3.


<!-- few shots or queries related to custom_tasks table  -->

1.
    <!-- task for the particular user -->
    - SELECT * FROM custom_tasks WHERE UserId = 'desired_user_id';
2.
    <!-- task scheduled time for particular user id -->
    - SELECT Task, ScheduledStartTime, ScheduledEndTime FROM custom_tasks WHERE UserId = 'desired_user_id';
3.
    <!-- give the task and description for particular id -->
    - SELECT Task, Description FROM custom_tasks WHERE UserId = 'desired_user_id';

4.


<!-- few shots or queries related to doctors table -->

1.
    <!-- give the speciality of doctor for this doctor id -->
    - SELECT Specialities FROM doctors WHERE id = 'desired_doctor_id';

2.
    <!-- qualifications of doctor for this particular id -->
    - SELECT Qualifications FROM doctors WHERE id = 'desired_doctor_id';
3.
    <!-- doctors specialized in particular field -->
    -   SELECT * FROM doctors WHERE Specialities LIKE '%desired_speciality%';

4.
    <!-- give the experience or calculate the experience of doctor -->
    -   SELECT id, PractisingSince, TIMESTAMPDIFF(YEAR, PractisingSince, CURDATE()) AS ExperienceYears FROM doctors;



<!-- few shots or queries related to health_priorities table -->

1.
    <!-- health priority type for this patient user id -->
    -   SELECT DISTINCT HealthPriorityType FROM health_priorities WHERE PatientUserId = 'desired_patient_id';

2.
    <!-- provider for particular id -->
    - SELECT DISTINCT Provider FROM health_priorities WHERE PatientUserId = 'desired_patient_id';

3.


<!-- few shot or queries related to health_priority_types table -->

1.
    <!-- health_priority_types for particular id -->
    -   SELECT Type, Tags FROM health_priority_types WHERE id = 'desired_id';
2.
    <!-- which are the health priorities types -->
    -  SELECT Type, Tags FROM health_priority_types;
3.


<!-- few shot or queries related to otp table -->

1.
     <!-- give the otp for particular user id -->
    - SELECT Otp FROM otp WHERE UserId = 'desired_user_id' AND Utilized = 0 ORDER BY ValidFrom DESC LIMIT 1;

2.
      <!-- check the validity of otp for particular user id -->
    - SELECT * FROM otp WHERE UserId = 'desired_user_id' AND Otp = 'provided_otp' AND Utilized = 0 AND NOW() BETWEEN ValidFrom AND ValidTill;

3.


<!-- few shots or queries related to patient_documents table -->

1.
    <!-- which are the documents submitted by particular user id -->
    - SELECT * FROM patient_documents WHERE PatientUserId = 'desired_user_id';

2.
    <!-- give the uploaded date of particular documents -->
    - SELECT UploadedDate FROM patient_documents WHERE PatientUserId = 'desired_user_id';

3.
    <!-- authenticated url for the particular user -->
    -   SELECT AuthenticatedUrl FROM patient_documents WHERE PatientUserId = 'desired_user_id';

4.


<!-- few shots or queries related to patient_emergency_contacts table -->

1.
    <!-- phone number for particular user id -->
    -   SELECT AdditionalPhoneNumbers FROM patient_emergency_contacts WHERE PatientUserId = 'desired_user_id';

2.
    <!-- give the address of particular patient  -->
    -   SELECT AddressId FROM patient_emergency_contacts WHERE PatientUserId = 'desired_user_id';

3.
    <!-- give the relation of relative to the particular patient id -->
    - SELECT ContactRelation FROM patient_emergency_contacts WHERE PatientUserId = 'desired_user_id';

4.
     <!-- give the organization of relatives for particular patient id -->
    - SELECT OrganizationId FROM patient_emergency_contacts WHERE PatientUserId = 'desired_user_id';



<!-- few shots or queries related to patient_goals table -->

1.
    <!-- give the goal title of particular patient id -->
    - SELECT Title FROM patient_goals WHERE PatientUserId = 'desired_user_id';

2.
    <!-- give the provider who provide the goal to the particular patient -->
    - SELECT DISTINCT Provider FROM patient_goals WHERE PatientUserId = 'desired_user_id';

3.
    <!-- give the complete time of goal for particular patient id -->
    - SELECT CompletedAt FROM patient_goals WHERE PatientUserId = 'desired_user_id';

4.
    <!-- give the goal abondoned time for particular patient id -->
    - SELECT CompletedAt FROM patient_goals WHERE PatientUserId = 'desired_user_id' AND GoalAbandoned = 1;

5.


 <!-- few shots or queries related to patient_health_profiles table -->

 1.
    <!-- give the blood group for particular patient id -->
    - SELECT BloodGroup FROM patient_health_profiles WHERE PatientUserId = 'your_patient_user_id';

2.
    <!-- give the marital status of particular user -->
    - SELECT MaritalStatus FROM patient_health_profiles WHERE PatientUserId = 'your_patient_user_id';

3.
    <!-- give the all details of particular id -->
    - SELECT * FROM patient_health_profiles WHERE PatientUserId = 'your_patient_user_id';

4.
    <!-- give the bloodpressure and cholesterol deatils of particular id -->
    - SELECT * FROM biometrics_blood_pressure WHERE PatientUserId = 'your_patient_user_id';

    - SELECT * FROM biometrics_blood_cholesterol WHERE PatientUserId = 'your_patient_user_id';
5.
    <!-- give the drinking status of particular id -->
    - SELECT IsDrinker, DrinkingSeverity, DrinkingSince FROM patient_health_profiles WHERE PatientUserId = 'your_patient_user_id';

6.


<!-- few shots or queries related to patient_insurances table -->

1.
    <!-- give the insurance provider to the particular patient id -->
    - SELECT InsuranceProvider FROM patient_insurances WHERE PatientUserId = 'your_patient_user_id';

2.
    <!-- give the insurance policy code for particular patient -->
    - SELECT InsurancePolicyCode FROM patient_insurances WHERE PatientUserId = 'your_patient_user_id';

3.
    <!-- give the validity of insurance to the particular id -->
    - SELECT ValidFrom, ValidTill FROM patient_insurances WHERE PatientUserId = 'your_patient_user_id';


<!-- few shots or queries related to patients table -->

1. 
    <!-- give the national health id for particular user -->
    - SELECT NationalHealthId FROM patients WHERE UserId = 'your_user_id';

2.
    <!-- give the associated hospital for particular id -->
    - SELECT AssociatedHospital FROM patients WHERE UserId = 'your_user_id';

3.
    <!-- give the display id for particular user -->
    - SELECT DisplayId FROM patients WHERE UserId = 'your_user_id';



<!-- few shots or queries related to person_addresses -->

1.
    <!-- give the address type for particular person id -->
    -    SELECT AddressType FROM person_addresses WHERE PersonId = 'your_person_id';

2.
    <!-- give the address id for particular person id -->
    - SELECT AddressId FROM person_addresses WHERE PersonId = 'your_person_id';
 
3.


<!-- few shots or queries related to person_roles table -->

1.
    <!-- give the role for particular person id -->
    - SELECT RoleName FROM person_roles WHERE PersonId = 'your_person_id'; 


<!-- few shots or queries related to persons table -->

1. 
    <!-- give the gender of thid id -->
    - SELECT Gender FROM persons WHERE id = 'your_person_id';

2.
    <!-- give the birthdate of particular person id -->
    - SELECT BirthDate FROM persons WHERE id = 'your_person_id';

3. 
    <!-- give the contact number of particular id -->
    - SELECT Phone FROM persons WHERE id = 'your_person_id';

4.
    <!-- give the full name of this id -->
    - SELECT CONCAT(FirstName, ' ', MiddleName, ' ', LastName) AS FullName FROM persons WHERE id = 'your_person_id';


5.


<!-- few shots or queries related to roles table -->

1.
    <!-- give the role for particular id -->
    - SELECT RoleName FROM roles WHERE id = your_specific_id;

2.
    <!-- give the description of the role for particular id -->
    - SELECT Description FROM roles WHERE id = your_specific_id;

3.
    <!-- which are the unique roles are available in table -->
    - SELECT DISTINCT RoleName FROM roles;


<!-- few shots or queries related to roles table -->

1.
    <!-- give the role for particular id -->
    - SELECT RoleName FROM roles WHERE id = your_specific_id;

2.
    <!-- give the description of the role for particular id -->
    - SELECT Description FROM roles WHERE id = your_specific_id;

3.
    <!-- which are the unique roles are available in table -->
    - SELECT DISTINCT RoleName FROM roles;



<!-- few shots or queries related to shared_document_details table  -->

1.
    <!-- give the document type for particular patient id -->
    -   SELECT DocumentType FROM shared_document_details WHERE PatientUserId = 'your_patient_user_id';
 
 
 2.
    <!-- give the date of document shared for particular id -->
    - SELECT SharedDate FROM shared_document_details WHERE id = 'your_document_id';


3.
    <!-- give the links for documents to particular id -->
     - SELECT OriginalLink, ShortLink FROM shared_document_details WHERE PatientUserId = 'your_patient_user_id';


<!-- few shots or queries related to user_device_details table -->

1.
    <!-- give the device name for particular user -->
    - SELECT DeviceName FROM user_device_details WHERE UserId = 'your_user_id';

2.
    <!-- Operating System Type and Version for a Particular User -->
    - SELECT OSType, OSVersion FROM user_device_details WHERE UserId = 'your_user_id';

3.
    <!-- App Name and Version for a Particular User -->
    - SELECT AppName, AppVersion FROM user_device_details WHERE UserId = 'your_user_id';

4.
    <!-- give the token for particular user -->
    - SELECT Token FROM user_device_details WHERE UserId = 'your_user_id';



<!-- few shots or queries related to user_login_sessions table -->

1.
    <!-- Retrieve Active Sessions for a User -->
    - SELECT * FROM user_login_sessions WHERE UserId = 'your_user_id' AND IsActive = 1;

2.
    <!-- Retrieve Expired Sessions for a User -->
    - SELECT * FROM user_login_sessions WHERE UserId = 'your_user_id' AND IsActive = 0;

3.
    <!-- Retrieve All Sessions for a User -->
    - SELECT * FROM user_login_sessions WHERE UserId = 'your_user_id';

4.
    <!-- Retrieve Sessions that Expired Before a Specific Date -->
    - SELECT * FROM user_login_sessions WHERE ValidTill < 'your_date';



<!-- few shots or queries related to user_tasks table -->

1.
    <!-- Retrieve All Tasks for a User -->
    - SELECT * FROM user_tasks WHERE UserId = 'your_user_id';

2.
    <!-- Retrieve Active Tasks for a User -->
    - SELECT * FROM user_tasks WHERE UserId = 'your_user_id' AND Finished = 0 AND Cancelled = 0;

3.
    <!-- Retrieve Finished Tasks for a User -->
    - SELECT * FROM user_tasks WHERE UserId = 'your_user_id' AND Finished = 1;

4.
    <!-- Retrieve Cancelled Tasks for a User -->
    - SELECT * FROM user_tasks WHERE UserId = 'your_user_id' AND Cancelled = 1;

5.
    <!-- Retrieve Recurrent Tasks for a User -->
    - SELECT * FROM user_tasks WHERE UserId = 'your_user_id' AND IsRecurrent = 1;



<!-- few shots or queries related to users table -->

1.
    <!-- Retrieve User Details by UserName -->
    - SELECT * FROM users WHERE UserName = 'your_username';

2.
    <!-- Retrieve User Details by PersonId -->
    - SELECT * FROM users WHERE PersonId = 'your_person_id';

3.
    <!-- Retrieve Active Users -->
    - SELECT * FROM users WHERE DeletedAt IS NULL;

4.
    <!-- Retrieve Test Users -->
    - SELECT * FROM users WHERE IsTestUser = 1;

5.
    <!-- Retrieve Users by Role -->
    - SELECT * FROM users WHERE RoleId = 'your_role_id';



<!-- few shots or queries related to addresses table  -->

1.
    <!-- Retrieve Address Details by Address ID -->
    - SELECT * FROM addresses WHERE id = 'your_address_id';

2.
    <!-- Retrieve Addresses by Type -->
    - SELECT * FROM addresses WHERE Type = 'your_address_type';

3.
    <!-- Retrieve Addresses in a Specific City -->
    - SELECT * FROM addresses WHERE City = 'your_city';

4.
    <!-- Retrieve Addresses in a Specific Country -->
    - SELECT * FROM addresses WHERE Country = 'your_country';

5.
    <!-- Retrieve Active Addresses -->
    - SELECT * FROM addresses WHERE DeletedAt IS NULL;
