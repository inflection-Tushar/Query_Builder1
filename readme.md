Few shots for particular table:

1..

CREATE TABLE `biometrics_body_temperature` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `EhrId` varchar(128) DEFAULT NULL,
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --foreign key from the users table
  `TerraSummaryId` varchar(128) DEFAULT NULL,
  `Provider` varchar(128) DEFAULT NULL,
  `BodyTemperature` float NOT NULL, ---contain the temperature of the patients body 
  `Unit` varchar(8) NOT NULL DEFAULT '°F',
  `RecordDate` datetime DEFAULT NULL,
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1.
   give me the last month body temperature for this patient id
    - SELECT * FROM biometrics_body_temperature WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= NOW() - INTERVAL 1 MONTH;
2.
    what is my body temperature yesterday
    - SELECT BodyTemperature FROM biometrics_body_temperature WHERE PatientUserId = 'patient_uuid_here' AND DATE(RecordDate) = CURDATE() - INTERVAL 1 DAY;
3. 
    give me my highest body temperature in this weak
    - SELECT MAX(BodyTemperature) AS HighestBodyTemperature FROM biometrics_body_temperature WHERE PatientUserId = 'patient_uuid_here' AND YEARWEEK(RecordDate, 1) = YEARWEEK(CURDATE(), 1);
4   
    give the total records from this table
    - SELECT COUNT(*) AS TotalRecords FROM biometrics_body_temperature;



2.

CREATE TABLE `biometrics_body_height` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `EhrId` varchar(128) DEFAULT NULL,
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---This is foreign key from persons table/module
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --This is foreign key from users table
  `BodyHeight` float NOT NULL, ---this column contain the height of the patient
  `Unit` varchar(8) NOT NULL DEFAULT 'cm',
  `RecordDate` datetime DEFAULT NULL,
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `PersonId` (`PersonId`),
  KEY `PatientUserId` (`PatientUserId`),
  CONSTRAINT `biometrics_body_height_ibfk_21` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT `biometrics_body_height_ibfk_22` FOREIGN KEY (`PatientUserId`) REFERENCES `users` (`id`) ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1. 
    give me the total records of height for the particular id
    - SELECT COUNT(*) AS TotalHeightRecords FROM biometrics_body_height WHERE PersonId = 'person_uuid_here';

2.
    what is the highest body temperature in last week for particular id
    - SELECT MAX(BodyTemperature) AS HighestBodyTemperature FROM biometrics_body_temperature WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 WEEK;

3. 
    give the history of height for last month for particular id
    - SELECT * FROM biometrics_body_height WHERE PersonId = 'person_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 MONTH;


3.
CREATE TABLE `biometrics_blood_pressure` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `EhrId` varchar(128) DEFAULT NULL,
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --foreign key from persons table
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --foreign key from users table
  `TerraSummaryId` varchar(128) DEFAULT NULL,
  `Provider` varchar(128) DEFAULT NULL,
  `Systolic` float NOT NULL, --maximum blood presure recorded
  `Diastolic` float NOT NULL, --minimum blood pressure recorded
  `Unit` varchar(8) NOT NULL DEFAULT 'mm-Hg',
  `RecordDate` datetime DEFAULT NULL,
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `biometrics_blood_pressure_ibfk_1` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1. 
    give me the blood pressure history for last month for the particular patient id 
    - SELECT * FROM biometrics_blood_pressure WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 MONTH;

2.
    notice the high blood pressure in last week for particular patient id
    - SELECT * FROM biometrics_blood_pressure WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 WEEK AND (Systolic > your_high_threshold OR Diastolic > your_high_threshold);

3. 
    give the total patient who check the blood pressure
    - SELECT COUNT(DISTINCT PatientUserId) AS TotalPatients FROM biometrics_blood_pressure;

4.
    give the updated time for this patient id
    - SELECT MAX(UpdatedAt) AS LatestUpdateTime FROM biometrics_blood_pressure WHERE PatientUserId = 'patient_uuid_here';


4.

  CREATE TABLE `biometrics_blood_oxygen_saturation` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `EhrId` varchar(128) DEFAULT NULL,
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---forein key from users able
  `TerraSummaryId` varchar(128) DEFAULT NULL,
  `Provider` varchar(128) DEFAULT NULL,
  `BloodOxygenSaturation` float NOT NULL, ---oxygen level in blood
  `Unit` varchar(8) NOT NULL DEFAULT '%',
  `RecordDate` datetime DEFAULT NULL,
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:
 
 1.
    give me the last month history of oxygen level in blood for particular id
    -SELECT * FROM biometrics_blood_oxygen_saturation WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 MONTH;
2.
    give me the lowest level of oxygen is noticed for particular id
    -SELECT MIN(BloodOxygenSaturation) AS LowestOxygenLevel FROM biometrics_blood_oxygen_saturation WHERE PatientUserId = 'patient_uuid_here';
3.
    give me the highest oxygen level is noticed for particular id
    - SELECT MAX(BloodOxygenSaturation) AS HighestOxygenLevel FROM biometrics_blood_oxygen_saturation WHERE PatientUserId = 'patient_uuid_here';
4.
    total who check the oxygen level in blood
    - SELECT COUNT(DISTINCT PatientUserId) AS TotalPatients FROM biometrics_blood_oxygen_saturation;


5.

 CREATE TABLE `biometrics_blood_glucose` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `EhrId` varchar(128) DEFAULT NULL,
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---foreign key from persons table
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---foreign key from users table
  `TerraSummaryId` varchar(128) DEFAULT NULL,
  `Provider` varchar(128) DEFAULT NULL,
  `BloodGlucose` float NOT NULL,  ---glucose quantity in users blood
  `A1CLevel` float DEFAULT NULL,
  `Unit` varchar(8) NOT NULL DEFAULT 'mg/dL',
  `RecordDate` datetime DEFAULT NULL,
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `biometrics_blood_glucose_ibfk_1` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1.
    highest blood pressure noticed for particular id
    - SELECT MAX(BloodGlucose) AS HighestBloodGlucose FROM biometrics_blood_glucose WHERE PatientUserId = 'patient_uuid_here';
2.
    give the hostory of last month glucose for particular id
    - SELECT * FROM biometrics_blood_glucose WHERE PatientUserId = 'patient_uuid_here' AND RecordDate >= CURDATE() - INTERVAL 1 MONTH;
3. 
    total patient who check glucose in blood
    - SELECT COUNT(DISTINCT PatientUserId) AS TotalPatients FROM biometrics_blood_glucose;


6.

CREATE TABLE `biometrics_blood_cholesterol` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `EhrId` varchar(128) DEFAULT NULL,
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---foreign key from the persons table
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---foreign key from the users table
  `TotalCholesterol` float DEFAULT NULL,  ---patient cholesterol 
  `HDL` float DEFAULT NULL,
  `LDL` float DEFAULT NULL,
  `TriglycerideLevel` float DEFAULT NULL,
  `Ratio` float DEFAULT NULL,
  `A1CLevel` float DEFAULT NULL,
  `Unit` varchar(8) DEFAULT 'mg/dl',
  `RecordDate` datetime DEFAULT NULL,
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `biometrics_blood_cholesterol_ibfk_1` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1.
    give me the record where i have a risk of heart attack using hdl and ldl for particular id
    - SELECT * FROM biometrics_blood_cholesterol WHERE PatientUserId = 'patient_uuid_here' AND (HDL < your_hdl_threshold OR LDL > your_ldl_threshold);

2.
    last time highest cholesterol
    - SELECT * FROM biometrics_blood_cholesterol WHERE PatientUserId = 'patient_uuid_here' ORDER BY TotalCholesterol DESC LIMIT 1;

3.
    give the history of a cholesterol for this patient id
    - SELECT * FROM biometrics_blood_cholesterol WHERE PatientUserId = 'patient_uuid_here' ORDER BY RecordDate DESC;


7.

CREATE TABLE `biometrics_body_weight` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `EhrId` varchar(128) DEFAULT NULL,
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---patient user id from users table
  `BodyWeight` float NOT NULL, --- body weight of patient
  `Unit` varchar(8) NOT NULL DEFAULT 'Kg',
  `RecordDate` datetime DEFAULT NULL,
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `PatientUserId` (`PatientUserId`),
  CONSTRAINT `biometrics_body_weight_ibfk_1` FOREIGN KEY (`PatientUserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots-

1. 
    highest body weight noticed for this patient id
    - SELECT * FROM biometrics_body_weight WHERE PatientUserId = 'patient_uuid_here' ORDER BY BodyWeight DESC LIMIT 1;
2.
    give the history of body weight for particular id
    - SELECT * FROM biometrics_body_weight WHERE PatientUserId = 'patient_uuid_here' ORDER BY RecordDate DESC;

3. 


8.

  CREATE TABLE `blood_donation_volunteers` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --foreign key from users table
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, -- foreign key from persons table
  `DisplayId` varchar(24) NOT NULL,
  `EhrId` varchar(256) DEFAULT NULL,
  `BloodGroup` varchar(16) DEFAULT NULL, -- blood group of patient
  `LastDonationDate` datetime DEFAULT NULL,
  `MedIssues` varchar(1024) DEFAULT NULL,
  `IsAvailable` tinyint(1) NOT NULL DEFAULT '0',
  `SelectedBloodGroup` varchar(16) DEFAULT NULL,
  `SelectedBridgeId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `SelectedPhoneNumber` varchar(16) DEFAULT NULL,
  `LastDonationRecordId` varchar(64) DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `blood_donation_volunteers_ibfk_21` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `blood_donation_volunteers_ibfk_22` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:
 
 1.
    give the selected blood groups
    - SELECT DISTINCT SelectedBloodGroup FROM blood_donation_volunteers WHERE IsAvailable = 1; -- Optional condition to filter by availability

2.
    give the mobile number of volunteers
    - SELECT SelectedPhoneNumber FROM blood_donation_volunteers WHERE IsAvailable = 1; -- Optional condition to filter by availability

3.
    give the blood groups available in the table
    - SELECT DISTINCT BloodGroup FROM blood_donation_volunteers WHERE IsAvailable = 1; -- Optional condition to filter by availability



9.

CREATE TABLE `blood_donors` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---user id from users table
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---person id from persons table
  `DisplayId` varchar(24) NOT NULL,
  `EhrId` varchar(256) DEFAULT NULL,
  `BloodGroup` varchar(16) DEFAULT NULL, --blood group of donors
  `AcceptorUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `LastDonationDate` datetime DEFAULT NULL,
  `DonorType` varchar(32) NOT NULL DEFAULT 'Blood bridge',
  `MedIssues` varchar(1024) DEFAULT NULL,
  `IsAvailable` tinyint(1) NOT NULL DEFAULT '0',
  `HasDonatedEarlier` tinyint(1) NOT NULL DEFAULT '0',
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `blood_donors_ibfk_21` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `blood_donors_ibfk_22` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots: 

1. 
    donors who are available for this blood group
    - SELECT * FROM blood_donors WHERE BloodGroup = 'desired_blood_group' AND IsAvailable = 1;
2.
    give the donor for particular AcceptorUserId
    - SELECT * FROM blood_donors WHERE AcceptorUserId = 'desired_acceptor_user_id';

3.


10.

    CREATE TABLE `custom_tasks` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --foreign key from users table
  `Task` varchar(128) DEFAULT NULL,  --tasks
  `Description` varchar(256) DEFAULT NULL, --task description
  `Category` varchar(128) DEFAULT 'Custom',
  `ActionType` varchar(64) NOT NULL DEFAULT 'Custom',
  `Details` text NOT NULL,
  `ScheduledStartTime` datetime DEFAULT NULL, --task start time
  `ScheduledEndTime` datetime DEFAULT NULL,-- task end time
  `Started` tinyint(1) NOT NULL DEFAULT '0',
  `StartedAt` datetime DEFAULT NULL,
  `Finished` tinyint(1) NOT NULL DEFAULT '0',
  `FinishedAt` datetime DEFAULT NULL,
  `Cancelled` tinyint(1) NOT NULL DEFAULT '0',
  `CancelledAt` datetime DEFAULT NULL,
  `CancellationReason` varchar(128) DEFAULT NULL,
  `IsRecurrent` tinyint(1) NOT NULL DEFAULT '0',
  `RecurrenceScheduleId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  CONSTRAINT `custom_tasks_ibfk_1` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1.
    task for the particular user
    - SELECT * FROM custom_tasks WHERE UserId = 'desired_user_id';
2.
    task scheduled time for particular user id
    - SELECT Task, ScheduledStartTime, ScheduledEndTime FROM custom_tasks WHERE UserId = 'desired_user_id';
3.
    give the task and description for particular id
    - SELECT Task, Description FROM custom_tasks WHERE UserId = 'desired_user_id';

4.


11.


CREATE TABLE `doctors` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --foreign key from users table
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,-- foreign key from persons table
  `DisplayId` varchar(24) NOT NULL,
  `NationalDigiDoctorId` varchar(32) DEFAULT NULL, --doctors national id
  `EhrId` varchar(256) DEFAULT NULL,
  `About` varchar(1024) DEFAULT NULL,
  `Locality` varchar(32) DEFAULT NULL,
  `Qualifications` varchar(256) DEFAULT NULL,
  `PractisingSince` datetime DEFAULT NULL,
  `Specialities` varchar(1024) DEFAULT NULL,--specialities of doctor
  `ProfessionalHighlights` varchar(2048) DEFAULT NULL,
  `ConsultationFee` float DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `doctors_ibfk_21` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `doctors_ibfk_22` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:

1.
    give the speciality of doctor for this doctor id
    - SELECT Specialities FROM doctors WHERE id = 'desired_doctor_id';

2.
    qualifications of doctor for this particular id
    - SELECT Qualifications FROM doctors WHERE id = 'desired_doctor_id';
3.
    doctors specialized in particular field
    -   SELECT * FROM doctors WHERE Specialities LIKE '%desired_speciality%';

4.
    give the experience or calculate the experience of doctor
    -   SELECT id, PractisingSince, TIMESTAMPDIFF(YEAR, PractisingSince, CURDATE()) AS ExperienceYears FROM doctors;



12.

CREATE TABLE `health_priorities` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --foreign key from users table
  `Source` varchar(32) NOT NULL,
  `Provider` varchar(64) NOT NULL,
  `ProviderEnrollmentId` varchar(32) NOT NULL,
  `ProviderCareplanCode` varchar(64) NOT NULL,
  `ProviderCareplanName` varchar(64) NOT NULL,
  `HealthPriorityType` varchar(64) DEFAULT NULL,
  `StartedAt` datetime DEFAULT NULL,
  `CompletedAt` datetime DEFAULT NULL,
  `Status` varchar(128) DEFAULT NULL,
  `ScheduledEndDate` datetime DEFAULT NULL,
  `IsPrimary` tinyint(1) DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:

1.
    health priority type for this patient user id
    -   SELECT DISTINCT HealthPriorityType FROM health_priorities WHERE PatientUserId = 'desired_patient_id';

2.
    provider for particular id
    - SELECT DISTINCT Provider FROM health_priorities WHERE PatientUserId = 'desired_patient_id';

3.


13.

CREATE TABLE `health_priority_types` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `Type` varchar(256) NOT NULL,
  `Tags` varchar(512) DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shot:

1.
    health_priority_types for particular id
    -   SELECT Type, Tags FROM health_priority_types WHERE id = 'desired_id';
2.
    which are the health priorities types
    -  SELECT Type, Tags FROM health_priority_types;
3.


14.

CREATE TABLE `otp` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `Purpose` varchar(64) DEFAULT NULL,
  `Otp` varchar(8) DEFAULT NULL,
  `ValidFrom` datetime NOT NULL,
  `ValidTill` datetime NOT NULL,
  `Utilized` tinyint(1) NOT NULL DEFAULT '0',
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shot:

1.
     give the otp for particular user id
    - SELECT Otp FROM otp WHERE UserId = 'desired_user_id' AND Utilized = 0 ORDER BY ValidFrom DESC LIMIT 1;

2.
      check the validity of otp for particular user id
    - SELECT * FROM otp WHERE UserId = 'desired_user_id' AND Otp = 'provided_otp' AND Utilized = 0 AND NOW() BETWEEN ValidFrom AND ValidTill;

3.
    



15.

CREATE TABLE `patient_documents` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `EhrId` varchar(128) DEFAULT NULL,
  `DisplayId` varchar(32) NOT NULL,
  `DocumentType` varchar(128) NOT NULL DEFAULT 'Unknown',
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `MedicalPractitionerUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `MedicalPractionerRole` varchar(64) DEFAULT NULL,
  `UploadedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `AssociatedVisitId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `AssociatedVisitType` varchar(64) DEFAULT 'Unknown',
  `AssociatedOrderId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `AssociatedOrderType` varchar(64) DEFAULT NULL,
  `FileName` varchar(512) DEFAULT NULL,
  `ResourceId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `AuthenticatedUrl` varchar(512) NOT NULL DEFAULT '',
  `MimeType` varchar(64) DEFAULT NULL,
  `SizeInKBytes` float DEFAULT NULL,
  `RecordDate` datetime DEFAULT NULL,
  `UploadedDate` datetime DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1.
    which are the documents submitted by particular user id
    - SELECT * FROM patient_documents WHERE PatientUserId = 'desired_user_id';

2.
    give the uploaded date of particular documents
    - SELECT UploadedDate FROM patient_documents WHERE PatientUserId = 'desired_user_id';

3.
    authenticated url for the particular user
    -   SELECT AuthenticatedUrl FROM patient_documents WHERE PatientUserId = 'desired_user_id';

4.



16.

CREATE TABLE `patient_emergency_contacts` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --foreign key from users table
  `ContactPersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `ContactRelation` varchar(64) NOT NULL DEFAULT 'Doctor',
  `AddressId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --address
  `OrganizationId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `IsAvailableForEmergency` tinyint(1) NOT NULL DEFAULT '0',
  `TimeOfAvailability` varchar(256) DEFAULT NULL,
  `Description` varchar(256) DEFAULT NULL,
  `AdditionalPhoneNumbers` varchar(64) DEFAULT NULL, --contact number
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `PatientUserId` (`PatientUserId`),
  KEY `ContactPersonId` (`ContactPersonId`),
  KEY `AddressId` (`AddressId`),
  KEY `OrganizationId` (`OrganizationId`),
  CONSTRAINT `patient_emergency_contacts_ibfk_41` FOREIGN KEY (`PatientUserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `patient_emergency_contacts_ibfk_42` FOREIGN KEY (`ContactPersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `patient_emergency_contacts_ibfk_43` FOREIGN KEY (`AddressId`) REFERENCES `addresses` (`id`) ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT `patient_emergency_contacts_ibfk_44` FOREIGN KEY (`OrganizationId`) REFERENCES `organizations` (`id`) ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:

1.
    phone number for particular user id
    -   SELECT AdditionalPhoneNumbers FROM patient_emergency_contacts WHERE PatientUserId = 'desired_user_id';

2.
    give the address of particular patient 
    -   SELECT AddressId FROM patient_emergency_contacts WHERE PatientUserId = 'desired_user_id';

3.
    give the relation of relative to the particular patient id
    - SELECT ContactRelation FROM patient_emergency_contacts WHERE PatientUserId = 'desired_user_id';

4.
     give the organization of relatives for particular patient id
    - SELECT OrganizationId FROM patient_emergency_contacts WHERE PatientUserId = 'desired_user_id';



17.

CREATE TABLE `patient_goals` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,--foreign key from user
  `ProviderEnrollmentId` varchar(64) DEFAULT NULL,
  `Provider` varchar(255) DEFAULT NULL,
  `ProviderCareplanName` varchar(32) DEFAULT NULL,
  `ProviderCareplanCode` varchar(32) DEFAULT NULL,
  `ProviderGoalCode` varchar(64) DEFAULT NULL,
  `Title` varchar(64) NOT NULL,--goal title
  `Sequence` varchar(64) DEFAULT NULL,
  `HealthPriorityId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `GoalAchieved` tinyint(1) DEFAULT '0',--goal achived
  `GoalAbandoned` tinyint(1) DEFAULT '0',--goal abondoned
  `StartedAt` datetime DEFAULT NULL,--goal started time
  `CompletedAt` datetime DEFAULT NULL,--goal complete time
  `ScheduledEndDate` datetime DEFAULT NULL,-- goal end date
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1.
    give the goal title of particular patient id
    - SELECT Title FROM patient_goals WHERE PatientUserId = 'desired_user_id';

2.
    give the provider who provide the goal to the particular patient
    - SELECT DISTINCT Provider FROM patient_goals WHERE PatientUserId = 'desired_user_id';

3.
    give the complete time of goal for particular patient id
    - SELECT CompletedAt FROM patient_goals WHERE PatientUserId = 'desired_user_id';

4.
    give the goal abondoned time for particular patient id
    - SELECT CompletedAt FROM patient_goals WHERE PatientUserId = 'desired_user_id' AND GoalAbandoned = 1;

5.


18. patient profile

CREATE TABLE `patient_health_profiles` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `BloodGroup` varchar(16) DEFAULT '',--blood group
  `BloodTransfusionDate` datetime DEFAULT NULL,
  `BloodDonationCycle` int DEFAULT NULL,
  `MajorAilment` varchar(128) DEFAULT '',
  `OtherConditions` varchar(512) DEFAULT '',
  `IsDiabetic` tinyint(1) DEFAULT NULL, --diabetic or not
  `HasHeartAilment` tinyint(1) DEFAULT NULL,--heart ailment
  `MaritalStatus` varchar(128) DEFAULT NULL,
  `Ethnicity` varchar(128) DEFAULT NULL,
  `Race` varchar(128) DEFAULT '',
  `StrokeSurvivorOrCaregiver` varchar(128) DEFAULT NULL,
  `LivingAlone` tinyint(1) DEFAULT NULL,
  `WorkedPriorToStroke` tinyint(1) DEFAULT NULL,
  `Nationality` varchar(64) DEFAULT NULL,
  `Occupation` varchar(64) DEFAULT NULL,
  `SedentaryLifestyle` tinyint(1) NOT NULL DEFAULT '0',
  `IsSmoker` tinyint(1) NOT NULL DEFAULT '0',--smoker or not
  `SmokingSeverity` enum('Low','Medium','High','Critical','Unknown') NOT NULL DEFAULT 'Low',
  `SmokingSince` datetime DEFAULT NULL,
  `IsDrinker` tinyint(1) NOT NULL DEFAULT '0',--drinker or not
  `DrinkingSeverity` enum('Low','Medium','High','Critical','Unknown') NOT NULL DEFAULT 'Low',
  `DrinkingSince` datetime DEFAULT NULL,
  `SubstanceAbuse` tinyint(1) NOT NULL DEFAULT '0',
  `ProcedureHistory` varchar(512) DEFAULT NULL,
  `ObstetricHistory` varchar(512) DEFAULT NULL,
  `OtherInformation` varchar(512) DEFAULT NULL,
  `TobaccoQuestion` text,
  `TobaccoQuestionAns` tinyint(1) DEFAULT NULL,
  `TypeOfStroke` varchar(128) DEFAULT NULL,
  `HasHighBloodPressure` tinyint(1) DEFAULT NULL, --blood pressure detail
  `HasHighCholesterol` tinyint(1) DEFAULT NULL, --cholesterol detail
  `HasAtrialFibrillation` tinyint(1) DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `PatientUserId` (`PatientUserId`),
  CONSTRAINT `patient_health_profiles_ibfk_1` FOREIGN KEY (`PatientUserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE


  few shots:

 1.
    give the blood group for particular patient id
    - SELECT BloodGroup FROM patient_health_profiles WHERE PatientUserId = 'your_patient_user_id';

2.
    give the marital status of particular user
    - SELECT MaritalStatus FROM patient_health_profiles WHERE PatientUserId = 'your_patient_user_id';

3.
    give the all details of particular id
    - SELECT * FROM patient_health_profiles WHERE PatientUserId = 'your_patient_user_id';

4.
    give the bloodpressure and cholesterol deatils of particular id
    - SELECT * FROM biometrics_blood_pressure WHERE PatientUserId = 'your_patient_user_id';

    - SELECT * FROM biometrics_blood_cholesterol WHERE PatientUserId = 'your_patient_user_id';
5.
    give the drinking status of particular id
    - SELECT IsDrinker, DrinkingSeverity, DrinkingSince FROM patient_health_profiles WHERE PatientUserId = 'your_patient_user_id';

6.



19. patient insurance details

CREATE TABLE `patient_insurances` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `InsuranceProvider` varchar(64) DEFAULT NULL, --insurance provider
  `InsurancePolicyCode` varchar(64) DEFAULT NULL, ---policy code
  `ValidFrom` datetime DEFAULT NULL,-- insurance valid from
  `ValidTill` datetime DEFAULT NULL,-- insurance valid till
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:

1.
    give the insurance provider to the particular patient id
    - SELECT InsuranceProvider FROM patient_insurances WHERE PatientUserId = 'your_patient_user_id';

2.
    give the insurance policy code for particular patient
    - SELECT InsurancePolicyCode FROM patient_insurances WHERE PatientUserId = 'your_patient_user_id';

3.
    give the validity of insurance to the particular id
    - SELECT ValidFrom, ValidTill FROM patient_insurances WHERE PatientUserId = 'your_patient_user_id';


20. patients

CREATE TABLE `patients` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `DisplayId` varchar(24) NOT NULL,
  `NationalHealthId` varchar(32) DEFAULT NULL, --national id of patient
  `MedicalProfileId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `TerraUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `TerraProvider` varchar(32) DEFAULT NULL,
  `TerraScopes` varchar(256) DEFAULT NULL,
  `EhrId` varchar(256) DEFAULT NULL,
  `HealthSystem` varchar(256) DEFAULT NULL,
  `AssociatedHospital` varchar(256) DEFAULT NULL, --hospital associated
  `DonorAcceptance` enum('Send','NotSend','Accepted') NOT NULL DEFAULT 'NotSend',
  `IsRemindersLoaded` tinyint(1) NOT NULL DEFAULT '0',
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `patients_ibfk_21` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `patients_ibfk_22` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1. 
    give the national health id for particular user
    - SELECT NationalHealthId FROM patients WHERE UserId = 'your_user_id';

2.
    give the associated hospital for particular id
    - SELECT AssociatedHospital FROM patients WHERE UserId = 'your_user_id';

3.
    give the display id for particular user
    - SELECT DisplayId FROM patients WHERE UserId = 'your_user_id';


21. person address 


CREATE TABLE `person_addresses` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --foreign key from persons table
  `AddressId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --foreign key from address table
  `AddressType` varchar(32) DEFAULT NULL,-- person address type
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `PersonId` (`PersonId`),
  KEY `AddressId` (`AddressId`),
  CONSTRAINT `person_addresses_ibfk_21` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `person_addresses_ibfk_22` FOREIGN KEY (`AddressId`) REFERENCES `addresses` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1.
    give the address type for particular person id
    -    SELECT AddressType FROM person_addresses WHERE PersonId = 'your_person_id';

2.
    give the address id for particular person id
    - SELECT AddressId FROM person_addresses WHERE PersonId = 'your_person_id';
 
3.



22.

CREATE TABLE `person_roles` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --foreign key from persons table
  `RoleId` int NOT NULL,
  `RoleName` varchar(32) DEFAULT NULL, --role name
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1.
    give the role for particular person id
    - SELECT RoleName FROM person_roles WHERE PersonId = 'your_person_id'; 


23.

CREATE TABLE `persons` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `Prefix` varchar(16) DEFAULT NULL,
  `FirstName` varchar(70) DEFAULT NULL,
  `MiddleName` varchar(70) DEFAULT NULL,
  `LastName` varchar(70) DEFAULT NULL,
  `Phone` varchar(24) NOT NULL,
  `Email` varchar(128) DEFAULT NULL,
  `TelegramChatId` varchar(64) DEFAULT NULL,
  `Gender` enum('Male','Female','Intersex','Other','Unknown') DEFAULT 'Unknown',
  `SelfIdentifiedGender` varchar(128) DEFAULT NULL,
  `BirthDate` datetime DEFAULT NULL,
  `Age` varchar(28) DEFAULT NULL,
  `ImageResourceId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `NationalId` varchar(64) DEFAULT NULL,
  `NationalIdType` varchar(32) NOT NULL DEFAULT 'Aadhar',
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `NationalId` (`NationalId`),
  UNIQUE KEY `NationalId_2` (`NationalId`),
  UNIQUE KEY `NationalId_3` (`NationalId`),
  UNIQUE KEY `NationalId_4` (`NationalId`),
  UNIQUE KEY `NationalId_5` (`NationalId`),
  UNIQUE KEY `NationalId_6` (`NationalId`),
  UNIQUE KEY `NationalId_7` (`NationalId`),
  UNIQUE KEY `NationalId_8` (`NationalId`),
  UNIQUE KEY `NationalId_9` (`NationalId`),
  UNIQUE KEY `NationalId_10` (`NationalId`),
  UNIQUE KEY `NationalId_11` (`NationalId`),
  KEY `persons__phone` (`Phone`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:

1. 
    give the gender of thid id
    - SELECT Gender FROM persons WHERE id = 'your_person_id';

2.
    give the birthdate of particular person id
    - SELECT BirthDate FROM persons WHERE id = 'your_person_id';

3. 
    give the contact number of particular id
    - SELECT Phone FROM persons WHERE id = 'your_person_id';

4.
    give the full name of this id
    - SELECT CONCAT(FirstName, ' ', MiddleName, ' ', LastName) AS FullName FROM persons WHERE id = 'your_person_id';


5.


24.

CREATE TABLE `role_privileges` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `Privilege` varchar(256) NOT NULL,
  `RoleId` int NOT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;



25.

CREATE TABLE `roles` (
  `id` int NOT NULL AUTO_INCREMENT,
  `RoleName` varchar(32) NOT NULL,--rolenname
  `Description` varchar(256) DEFAULT NULL, --description of the role
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=13 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:

1.
    give the role for particular id
    - SELECT RoleName FROM roles WHERE id = your_specific_id;

2.
    give the description of the role for particular id
    - SELECT Description FROM roles WHERE id = your_specific_id;

3.
    which are the unique roles are available in table
    - SELECT DISTINCT RoleName FROM roles;



26.


CREATE TABLE `shared_document_details` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `DocumentId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `ResourceId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `DocumentType` varchar(128) NOT NULL DEFAULT 'Unknown',
  `OriginalLink` text NOT NULL,
  `ShortLink` varchar(256) NOT NULL,
  `Key` varchar(512) NOT NULL,
  `SharedWithUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `SharedForDurationMin` int NOT NULL DEFAULT '720',
  `SharedDate` datetime DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:

1.
    give the document type for particular patient id
    -   SELECT DocumentType FROM shared_document_details WHERE PatientUserId = 'your_patient_user_id';
 
 
 2.
    give the date of document shared for particular id
    - SELECT SharedDate FROM shared_document_details WHERE id = 'your_document_id';


3.
    give the links for documents to particular id
     - SELECT OriginalLink, ShortLink FROM shared_document_details WHERE PatientUserId = 'your_patient_user_id';


27.

CREATE TABLE `user_device_details` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `Token` varchar(1024) NOT NULL,
  `DeviceName` varchar(512) NOT NULL, --user device name
  `OSType` varchar(256) NOT NULL, --operating system type
  `OSVersion` varchar(64) NOT NULL, --operating system version
  `AppName` varchar(256) NOT NULL, --app name
  `AppVersion` varchar(64) NOT NULL, --app version
  `ChangeCount` int DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  CONSTRAINT `user_device_details_ibfk_1` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:

1.
    give the device name for particular user
    - SELECT DeviceName FROM user_device_details WHERE UserId = 'your_user_id';

2.
    Operating System Type and Version for a Particular User
    - SELECT OSType, OSVersion FROM user_device_details WHERE UserId = 'your_user_id';

3.
    App Name and Version for a Particular User
    - SELECT AppName, AppVersion FROM user_device_details WHERE UserId = 'your_user_id';

4.
    give the token for particular user
    - SELECT Token FROM user_device_details WHERE UserId = 'your_user_id';


28.

CREATE TABLE `user_login_sessions` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `IsActive` tinyint(1) NOT NULL DEFAULT '1', --is user session is active or not
  `StartedAt` datetime DEFAULT NULL, --session started
  `ValidTill` datetime DEFAULT NULL, --session end time
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  CONSTRAINT `user_login_sessions_ibfk_1` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:

1.
    Retrieve Active Sessions for a User
    - SELECT * FROM user_login_sessions WHERE UserId = 'your_user_id' AND IsActive = 1;

2.
    Retrieve Expired Sessions for a User
    - SELECT * FROM user_login_sessions WHERE UserId = 'your_user_id' AND IsActive = 0;

3.
    Retrieve All Sessions for a User
    - SELECT * FROM user_login_sessions WHERE UserId = 'your_user_id';

4.
    Retrieve Sessions that Expired Before a Specific Date
    - SELECT * FROM user_login_sessions WHERE ValidTill < 'your_date';


29.

CREATE TABLE `user_tasks` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---foreign key from user table
  `DisplayId` varchar(128) DEFAULT NULL,
  `Task` varchar(128) DEFAULT NULL,  ---task which is assigned to the user
  `Category` varchar(128) DEFAULT 'Custom', --category of the task
  `Description` varchar(256) DEFAULT NULL,-- description of the task
  `ActionType` varchar(64) DEFAULT NULL,
  `ActionId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `ScheduledStartTime` datetime DEFAULT NULL, --task scheluded start time
  `ScheduledEndTime` datetime DEFAULT NULL, --task scheduled end time
  `Started` tinyint(1) NOT NULL DEFAULT '0',
  `StartedAt` datetime DEFAULT NULL,
  `Finished` tinyint(1) NOT NULL DEFAULT '0',
  `FinishedAt` datetime DEFAULT NULL,
  `Cancelled` tinyint(1) NOT NULL DEFAULT '0',
  `CancelledAt` datetime DEFAULT NULL,
  `CancellationReason` varchar(128) DEFAULT NULL,
  `IsRecurrent` tinyint(1) NOT NULL DEFAULT '0',
  `RecurrenceScheduleId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  CONSTRAINT `user_tasks_ibfk_1` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots:

1.
    Retrieve All Tasks for a User
    - SELECT * FROM user_tasks WHERE UserId = 'your_user_id';

2.
    Retrieve Active Tasks for a User
    - SELECT * FROM user_tasks WHERE UserId = 'your_user_id' AND Finished = 0 AND Cancelled = 0;

3.
    Retrieve Finished Tasks for a User
    - SELECT * FROM user_tasks WHERE UserId = 'your_user_id' AND Finished = 1;

4.
    Retrieve Cancelled Tasks for a User
    - SELECT * FROM user_tasks WHERE UserId = 'your_user_id' AND Cancelled = 1;

5.
    Retrieve Recurrent Tasks for a User
    - SELECT * FROM user_tasks WHERE UserId = 'your_user_id' AND IsRecurrent = 1;


30.


CREATE TABLE `users` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---
  `RoleId` int NOT NULL,
  `UserName` varchar(10) DEFAULT NULL, --username
  `Password` varchar(256) DEFAULT NULL, --password
  `LastLogin` datetime DEFAULT NULL, --last login
  `DefaultTimeZone` varchar(16) NOT NULL DEFAULT '+05:30', --default time zone
  `CurrentTimeZone` varchar(16) NOT NULL DEFAULT '+05:30', --current time zone
  `IsTestUser` tinyint(1) NOT NULL DEFAULT '0',
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `UserName` (`UserName`),
  UNIQUE KEY `UserName_2` (`UserName`),
  UNIQUE KEY `UserName_3` (`UserName`),
  UNIQUE KEY `UserName_4` (`UserName`),
  UNIQUE KEY `UserName_5` (`UserName`),
  UNIQUE KEY `UserName_6` (`UserName`),
  UNIQUE KEY `UserName_7` (`UserName`),
  UNIQUE KEY `UserName_8` (`UserName`),
  UNIQUE KEY `UserName_9` (`UserName`),
  UNIQUE KEY `UserName_10` (`UserName`),
  UNIQUE KEY `UserName_11` (`UserName`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `users_ibfk_1` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


few shots:

1.
    Retrieve User Details by UserName
    - SELECT * FROM users WHERE UserName = 'your_username';

2.
    Retrieve User Details by PersonId
    - SELECT * FROM users WHERE PersonId = 'your_person_id';

3.
    Retrieve Active Users
    - SELECT * FROM users WHERE DeletedAt IS NULL;

4.
    Retrieve Test Users
    - SELECT * FROM users WHERE IsTestUser = 1;

5.
    Retrieve Users by Role
    - SELECT * FROM users WHERE RoleId = 'your_role_id';


31.

CREATE TABLE `addresses` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `Type` varchar(16) NOT NULL DEFAULT 'Work',
  `AddressLine` varchar(64) NOT NULL, --address
  `City` varchar(32) DEFAULT NULL, --city
  `Location` varchar(256) DEFAULT NULL, --location
  `District` varchar(32) DEFAULT NULL, --district
  `State` varchar(32) DEFAULT NULL, --state
  `Country` varchar(128) DEFAULT NULL, --country
  `PostalCode` varchar(16) DEFAULT NULL,--postal code
  `Longitude` float DEFAULT NULL,
  `Lattitude` float DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

few shots;

1.
    Retrieve Address Details by Address ID
    - SELECT * FROM addresses WHERE id = 'your_address_id';

2.
    Retrieve Addresses by Type
    - SELECT * FROM addresses WHERE Type = 'your_address_type';

3.
    Retrieve Addresses in a Specific City
    - SELECT * FROM addresses WHERE City = 'your_city';

4.
    Retrieve Addresses in a Specific Country
    - SELECT * FROM addresses WHERE Country = 'your_country';

5.
    Retrieve Active Addresses
    - SELECT * FROM addresses WHERE DeletedAt IS NULL;
