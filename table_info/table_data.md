

1. biometrics_body_temperature , body_temperature ,  temperature, this table  contains information about the body temperature of a person

``` sql
CREATE TABLE `biometrics_body_temperature` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each biometrics_body_temperature
  `EhrId` varchar(128) DEFAULT NULL,
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --patient id of patient test performed on
  `TerraSummaryId` varchar(128) DEFAULT NULL,
  `Provider` varchar(128) DEFAULT NULL, ---provider who performed test on patient
  `BodyTemperature` float NOT NULL, --- temperature of patient 
  `Unit` varchar(8) NOT NULL DEFAULT '°F', ---unit of temperature
  `RecordDate` datetime DEFAULT NULL, ---body temperature record date
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---id of user who recorded the temperature
  `CreatedAt` datetime DEFAULT NULL, --- created at timestamp
  `UpdatedAt` datetime NOT NULL,  --- updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,    -- deleted if set to not null
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```
##


2. biometrics_body_height, body height, height, this  table stores the data about a person's height
``` sql
CREATE TABLE `biometrics_body_height` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each biometrics_body_height
  `EhrId` varchar(128) DEFAULT NULL, --- Electronics  Health Record ID
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---id of person
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --- id of patient
  `BodyHeight` float NOT NULL, --- height of patient
  `Unit` varchar(8) NOT NULL DEFAULT 'cm', ---measured unit of height 
  `RecordDate` datetime DEFAULT NULL, ---recorded date of patient height
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---id of user who recorded the height
  `CreatedAt` datetime DEFAULT NULL, ---created time stamp
  `UpdatedAt` datetime NOT NULL,    ---updated time stamp
  `DeletedAt` datetime DEFAULT NULL,    --set to not null when data is deleted
  PRIMARY KEY (`id`),
  KEY `PersonId` (`PersonId`),
  KEY `PatientUserId` (`PatientUserId`),
  CONSTRAINT `biometrics_body_height_ibfk_21` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON DELETE SET NULL ON UPDATE CASCADE,
  CONSTRAINT `biometrics_body_height_ibfk_22` FOREIGN KEY (`PatientUserId`) REFERENCES `users` (`id`) ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
##



3. biometrics_blood_pressure, blood pressure, low blood pressure, high blood pressure, pulse and respiration are stored in this table, heart rate, systolic blood pressure, diastolic blood pressure 
``` sql
CREATE TABLE `biometrics_blood_pressure` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each biometrics_blood_pressure
  `EhrId` varchar(128) DEFAULT NULL, --- electronics  health records id
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, -- id of person
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, -- id of patient
  `TerraSummaryId` varchar(128) DEFAULT NULL,  -- terra summary id for this data
  `Provider` varchar(128) DEFAULT NULL,          -- provider who recorded the data
  `Systolic` float NOT NULL, --maximum blood presure recorded
  `Diastolic` float NOT NULL, --minimum blood pressure recorded
  `Unit` varchar(8) NOT NULL DEFAULT 'mm-Hg',     --unit of measurement
  `RecordDate` datetime DEFAULT NULL,              --date when the reading was taken
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,    --user who took the record
  `CreatedAt` datetime DEFAULT NULL,                -- created timestamp
  `UpdatedAt` datetime NOT NULL,                    -- updated timestamp
  `DeletedAt` datetime DEFAULT NULL,                 -- deleted timestamp
  PRIMARY KEY (`id`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `biometrics_blood_pressure_ibfk_1` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

##


4. biometrics_blood_oxygen_saturation, blood_oxygen_saturation, oxygen in blood, oxygen level in blood, it's a measure of how much oxygen, details of oxygen in blood
``` sql
  CREATE TABLE `biometrics_blood_oxygen_saturation` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each biometrics_blood_oxygen_saturation
  `EhrId` varchar(128) DEFAULT NULL,  ---Electronics  Health Record ID
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of patient
  `TerraSummaryId` varchar(128) DEFAULT NULL, --- ID from Terra's system
  `Provider` varchar(128) DEFAULT NULL,  --- provider name
  `BloodOxygenSaturation` float NOT NULL, ---oxygen level in blood
  `Unit` varchar(8) NOT NULL DEFAULT '%',     ---unit of oxygen saturation
  `RecordDate` datetime DEFAULT NULL,         ---date when the measurement was taken
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---user who took the measurement
  `CreatedAt` datetime DEFAULT NULL,            ---created time stamp
  `UpdatedAt` datetime NOT NULL,                 ---updated time stamp
  `DeletedAt` datetime DEFAULT NULL, -- deleted timestamp
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```




##


5. biometrics_blood_glucose, blood glucose, blood sugar, sugar in blood, glucose in blood, diabetes management tool records
``` sql
 CREATE TABLE `biometrics_blood_glucose` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each biometrics_blood_glucose
  `EhrId` varchar(128) DEFAULT NULL, ---Electronics  Health Record Id
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---id of person
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---id of patient
  `TerraSummaryId` varchar(128) DEFAULT NULL,  ---summary id for data source
  `Provider` varchar(128) DEFAULT NULL, ---provider  name who provide this glucose record
  `BloodGlucose` float NOT NULL,  ---glucose quantity in users blood
  `A1CLevel` float DEFAULT NULL,      --percentage of total hemoglobin
  `Unit` varchar(8) NOT NULL DEFAULT 'mg/dL', ---unit of  measurement
  `RecordDate` datetime DEFAULT NULL,     ---date when the glucose was taken
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---user who recorded it
  `CreatedAt` datetime DEFAULT NULL,        ---creation time stamp
  `UpdatedAt` datetime NOT NULL,             ---update time stamp
  `DeletedAt` datetime DEFAULT NULL,            ---deletion timestamp
  PRIMARY KEY (`id`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `biometrics_blood_glucose_ibfk_1` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```


##

6. biometrics_blood_cholesterol, blood cholesterol, hdl and ldl levels, cholesterols, LDL, HDL
``` sql
CREATE TABLE `biometrics_blood_cholesterol` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each biometrics_blood_cholesterol
  `EhrId` varchar(128) DEFAULT NULL, ---electronic  health record id
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---id of person
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of user
  `TotalCholesterol` float DEFAULT NULL,  ---patient cholesterol 
  `HDL` float DEFAULT NULL,              --good cholestrol
  `LDL` float DEFAULT NULL,                --bad cholestrol
  `TriglycerideLevel` float DEFAULT NULL, ---triglycerides in the blood
  `Ratio` float DEFAULT NULL,              ---ratio between good and bad chol
  `A1CLevel` float DEFAULT NULL,            ---a1c level in the blood
  `Unit` varchar(8) DEFAULT 'mg/dl',        ---unit for all values
  `RecordDate` datetime DEFAULT NULL,        ---date when test was done
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,    --user who took the test
  `CreatedAt` datetime DEFAULT NULL,          --created timestamp
  `UpdatedAt` datetime NOT NULL,                 --updated timestamp
  `DeletedAt` datetime DEFAULT NULL,             --deleted timestamp
  PRIMARY KEY (`id`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `biometrics_blood_cholesterol_ibfk_1` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

##

7. biometrics_body_weight,  body weight measurements, body weight, weight, table contains the body weight related details
``` sql
CREATE TABLE `biometrics_body_weight` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each biometrics_body_weight
  `EhrId` varchar(128) DEFAULT NULL,  ---electronic health record id
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---patient user id 
  `BodyWeight` float NOT NULL, --- body weight of patient
  `Unit` varchar(8) NOT NULL DEFAULT 'Kg', ---unit   of measurement for body weight
  `RecordDate` datetime DEFAULT NULL,  --date when the data was recorded
  `RecordedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,  ---user who recorded this data
  `CreatedAt` datetime DEFAULT NULL,     --timestamp when created
  `UpdatedAt` datetime NOT NULL,           --timestamp when updated
  `DeletedAt` datetime DEFAULT NULL,        --timestamp when deleted
  PRIMARY KEY (`id`),
  KEY `PatientUserId` (`PatientUserId`),
  CONSTRAINT `biometrics_body_weight_ibfk_1` FOREIGN KEY (`PatientUserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```


##




8. blood_donation_volunteers, volunteer, this table contains  information about people who have donated blood voluntarily
``` sql
  CREATE TABLE `blood_donation_volunteers` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each blood_donation_volunteers
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --id of user
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, -- id of person
  `DisplayId` varchar(24) NOT NULL,  -- display name for volunteer
  `EhrId` varchar(256) DEFAULT NULL,  -- ehr id from other system
  `BloodGroup` varchar(16) DEFAULT NULL, -- blood group of patient
  `LastDonationDate` datetime DEFAULT NULL,  -- last donation date
  `MedIssues` varchar(1024) DEFAULT NULL,  -- medical issues that the volunteer has
  `IsAvailable` tinyint(1) NOT NULL DEFAULT '0',  -- is available to donate or not
  `SelectedBloodGroup` varchar(16) DEFAULT NULL,   -- selected blood group by volunteer
  `SelectedBridgeId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,    -- bridge id which will be used if there
  `SelectedPhoneNumber` varchar(16) DEFAULT NULL,     -- phone number of volunteer
  `LastDonationRecordId` varchar(64) DEFAULT NULL,      -- record id of last donation
  `CreatedAt` datetime DEFAULT NULL,                     -- timestamp when created
  `UpdatedAt` datetime NOT NULL,                           -- timestamp when updated
  `DeletedAt` datetime DEFAULT NULL,                         -- timestamp when deleted
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `blood_donation_volunteers_ibfk_21` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `blood_donation_volunteers_ibfk_22` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

##

9. blood_donors, donor, blood donor, potential donor, eligible donor, registered donor, plasma donor, universal donor
``` sql
CREATE TABLE `blood_donors` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each blood_donors
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---user id user 
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --- id of person
  `DisplayId` varchar(24) NOT NULL,                                --- display id
  `EhrId` varchar(256) DEFAULT NULL,                                --- ehr id
  `BloodGroup` varchar(16) DEFAULT NULL, --blood group of donors  
  `AcceptorUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---acceptor user id if any
  `LastDonationDate` datetime DEFAULT NULL,                           --- last donation date and time
  `DonorType` varchar(32) NOT NULL DEFAULT 'Blood bridge',            --- Donor type can be Blood Bridge or
  `MedIssues` varchar(1024) DEFAULT NULL,                              --- Medical issues if any
  `IsAvailable` tinyint(1) NOT NULL DEFAULT '0',                           --- Is available to donate now?
  `HasDonatedEarlier` tinyint(1) NOT NULL DEFAULT '0',                      --- Has the user ever donated before
  `CreatedAt` datetime DEFAULT NULL,                                         --- created at timestamp
  `UpdatedAt` datetime NOT NULL,                                                 --- updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,                                                 --- delete at timestamp
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `blood_donors_ibfk_21` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `blood_donors_ibfk_22` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

##

10. custom_tasks, custom activities, defined tasks, this table contains custom tasks
``` sql
CREATE TABLE `custom_tasks` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each custom_tasks
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --id of user
  `Task` varchar(128) DEFAULT NULL,  -- task
  `Description` varchar(256) DEFAULT NULL, --task description
  `Category` varchar(128) DEFAULT 'Custom', --category of the task
  `ActionType` varchar(64) NOT NULL DEFAULT 'Custom', --type of action like Custom, Reminder etc
  `Details` text NOT NULL,  --details about the task
  `ScheduledStartTime` datetime DEFAULT NULL, --task start time
  `ScheduledEndTime` datetime DEFAULT NULL,-- task end time
  `Started` tinyint(1) NOT NULL DEFAULT '0', --is started or not
  `StartedAt` datetime DEFAULT NULL,   --started at timestamp
  `Finished` tinyint(1) NOT NULL DEFAULT '0', -- is finished or not
  `FinishedAt` datetime DEFAULT NULL,     --finished at timestamp
  `Cancelled` tinyint(1) NOT NULL DEFAULT '0',  -- cancelled by user or system
  `CancelledAt` datetime DEFAULT NULL,        --cancelled at timestamp
  `CancellationReason` varchar(128) DEFAULT NULL,     --reason for cancelling the task
  `IsRecurrent` tinyint(1) NOT NULL DEFAULT '0',         --if it's recurring task
  `RecurrenceScheduleId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,     --recurrence schedule id if any
  `CreatedAt` datetime DEFAULT NULL,                 --created at timestamp
  `UpdatedAt` datetime NOT NULL,                           --updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,                                --delete at timestamp
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  CONSTRAINT `custom_tasks_ibfk_1` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

##

11. doctors, physician, surgeon, specialist, cardiologist, radiologist, neurologist, gynecologist
``` sql
CREATE TABLE `doctors` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each doctors
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --- id of user
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,-- id of person
  `DisplayId` varchar(24) NOT NULL,                             ----display name to show in UI
  `NationalDigiDoctorId` varchar(32) DEFAULT NULL, --doctors national id
  `EhrId` varchar(256) DEFAULT NULL,                ------ehr system unique id
  `About` varchar(1024) DEFAULT NULL,                --about doctor
  `Locality` varchar(32) DEFAULT NULL,                --locality where the doctor is located
  `Qualifications` varchar(256) DEFAULT NULL,           --qualification and specialization
  `PractisingSince` datetime DEFAULT NULL,             --year when started practicing
  `Specialities` varchar(1024) DEFAULT NULL,--specialities of doctor
  `ProfessionalHighlights` varchar(2048) DEFAULT NULL, --professional highlights/achievements
  `ConsultationFee` float DEFAULT NULL,                --consultation fee per minute or hour
  `CreatedAt` datetime DEFAULT NULL,                     --created at timestamp
  `UpdatedAt` datetime NOT NULL,                             --updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,                                --delete at timestamp
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `doctors_ibfk_21` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `doctors_ibfk_22` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```


##


12. health_priorities, condition, symptom, disease, problem, Health Goals
``` sql
CREATE TABLE `health_priorities` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each health_priorities
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --- id of patient
  `Source` varchar(32) NOT NULL, ---source of the priority 
  `Provider` varchar(64) NOT NULL, ---provider who set this priority
  `ProviderEnrollmentId` varchar(32) NOT NULL, ---enrollment number in provider system
  `ProviderCareplanCode` varchar(64) NOT NULL,  ---code that identifies care plan in provider system
  `ProviderCareplanName` varchar(64) NOT NULL, ---name of care plan in provider system
  `HealthPriorityType` varchar(64) DEFAULT NULL, ---type of health priority: chronic disease,
  `StartedAt` datetime DEFAULT NULL,  ---when user started to have this health priority
  `CompletedAt` datetime DEFAULT NULL, --- when user completed treatment for this health priority
  `Status` varchar(128) DEFAULT NULL, ---status of health priority: active,completed
  `ScheduledEndDate` datetime DEFAULT NULL, ---date when treatment should be finished
  `IsPrimary` tinyint(1) DEFAULT NULL, ---is primary health priority or not
  `CreatedAt` datetime DEFAULT NULL,          ----created at timestamp
  `UpdatedAt` datetime NOT NULL,                -----updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,                 -------delete at timestamp
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

##



 
13. health_priority_types, Health category, health concern category, this table contains the health priority types
``` sql
CREATE TABLE `health_priority_types` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each health_priority_types
  `Type` varchar(256) NOT NULL, --- Type of Health Priority Type
  `Tags` varchar(512) DEFAULT NULL,  --- Comma separated list of Tags associated with this
  `CreatedAt` datetime DEFAULT NULL,      -- Created At Timestamp
  `UpdatedAt` datetime NOT NULL,              -- Updated At Timestamp
  `DeletedAt` datetime DEFAULT NULL,             -- Delete At Timestamp
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```



##


14. otp, one time password, verification code, auth code, token, temp password, this table contains the one time password
``` sql
CREATE TABLE `otp` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each otp
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,  --- id of user
  `Purpose` varchar(64) DEFAULT NULL,                                 -- what is the purpose of this O
  `Otp` varchar(8) DEFAULT NULL,                                     -- One Time Password
  `ValidFrom` datetime NOT NULL,                                     -- Valid from and till when it
  `ValidTill` datetime NOT NULL,                                     -- will be valid
  `Utilized` tinyint(1) NOT NULL DEFAULT '0',                         -- Is this Otp has been used
  `CreatedAt` datetime DEFAULT NULL,                                   -- created at timestamp
  `UpdatedAt` datetime NOT NULL,                                         -- updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,                                         -- delete at timestamp
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


```


##

    
15. patient_documents,medical records, patient files, health records, clinical documents, medical history, documents submitted by patient, this tabel contains details related to patient documentation
``` sql
CREATE TABLE `patient_documents` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each patient_documents
  `EhrId` varchar(128) DEFAULT NULL,  ---electronic  health record id
  `DisplayId` varchar(32) NOT NULL,    --displayed document Id to the user
  `DocumentType` varchar(128) NOT NULL DEFAULT 'Unknown', ---type of document
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---user who uploaded this document
  `MedicalPractitionerUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---user who uploaded this document
  `MedicalPractionerRole` varchar(64) DEFAULT NULL,    ---doctor's role in this document
  `UploadedByUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---user who uploaded the document
  `AssociatedVisitId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---visit related to this document
  `AssociatedVisitType` varchar(64) DEFAULT 'Unknown', ---visit type associated with this document
  `AssociatedOrderId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---order id if any
  `AssociatedOrderType` varchar(64) DEFAULT NULL,        ---order type if any
  `FileName` varchar(512) DEFAULT NULL,                   ---file name as per client system
  `ResourceId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---unique resource id from cloud storage provider
  `AuthenticatedUrl` varchar(512) NOT NULL DEFAULT '',       ---authenticated url to access the file
  `MimeType` varchar(64) DEFAULT NULL,                 ----mimetype of the file
  `SizeInKBytes` float DEFAULT NULL,                       ---size of the file in KB
  `RecordDate` datetime DEFAULT NULL,                       ---date when the document was added/
  `UploadedDate` datetime DEFAULT NULL,                       ---date when the document was uploaded by
  `CreatedAt` datetime DEFAULT NULL,                            ---created at timestamp
  `UpdatedAt` datetime NOT NULL,                                  ---updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,                                  ---delete at timestamp
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```


##


16. patient_emergency_contacts, Emergency contacts, Primary contact, contact details in case of emergency, details of patient relatives contacts
``` sql
CREATE TABLE `patient_emergency_contacts` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each patient_emergency_contacts
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --id of patient
  `ContactPersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,  --id of contact person
  `ContactRelation` varchar(64) NOT NULL DEFAULT 'Doctor',                       --relation to the patient
  `AddressId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,    --address id
  `OrganizationId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --organization id
  `IsAvailableForEmergency` tinyint(1) NOT NULL DEFAULT '0',                       --is available for emergencies?
  `TimeOfAvailability` varchar(256) DEFAULT NULL,                                --time available to be called or visited
  `Description` varchar(256) DEFAULT NULL,                                       --description about emergency contact
  `AdditionalPhoneNumbers` varchar(64) DEFAULT NULL, --contact number
  `CreatedAt` datetime DEFAULT NULL,                  --created at timestamp
  `UpdatedAt` datetime NOT NULL,                        --updated at timestamp
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
```


##


17. patient_goals, Health targets, Desired health outcomes, details of patient goals
``` sql
CREATE TABLE `patient_goals` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each patient_goals
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,-- patient id 
  `ProviderEnrollmentId` varchar(64) DEFAULT NULL, -- provider enrollement Id if any
  `Provider` varchar(255) DEFAULT NULL,  -- Provider name
  `ProviderCareplanName` varchar(32) DEFAULT NULL, -- care plan name
  `ProviderCareplanCode` varchar(32) DEFAULT NULL, --care plan code
  `ProviderGoalCode` varchar(64) DEFAULT NULL, -- Goal Code
  `Title` varchar(64) NOT NULL,--goal title
  `Sequence` varchar(64) DEFAULT NULL, --sequence in which goal is set by the user
  `HealthPriorityId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, -- id of health priority
  `GoalAchieved` tinyint(1) DEFAULT '0',--goal achived
  `GoalAbandoned` tinyint(1) DEFAULT '0',--goal abondoned
  `StartedAt` datetime DEFAULT NULL,--goal started time
  `CompletedAt` datetime DEFAULT NULL,--goal complete time
  `ScheduledEndDate` datetime DEFAULT NULL,-- goal end date
  `CreatedAt` datetime DEFAULT NULL,   -- created at timestamp
  `UpdatedAt` datetime NOT NULL,        -- updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,       -- deleted at timestamp
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```

##



18. patient_health_profiles, profile of patient health, Medical history, Patient records, Individual health data
``` sql
CREATE TABLE `patient_health_profiles` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each patient_health_profiles
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,  ---id of patient
  `BloodGroup` varchar(16) DEFAULT '',--blood group
  `BloodTransfusionDate` datetime DEFAULT NULL,  --last blood transfusion date
  `BloodDonationCycle` int DEFAULT NULL,         --how many times donated in a life
  `MajorAilment` varchar(128) DEFAULT '',         --major health issue
  `OtherConditions` varchar(512) DEFAULT '',       --other health issues
  `IsDiabetic` tinyint(1) DEFAULT NULL, --diabetic or not
  `HasHeartAilment` tinyint(1) DEFAULT NULL,--heart ailment
  `MaritalStatus` varchar(128) DEFAULT NULL,       --marrital status
  `Ethnicity` varchar(128) DEFAULT NULL,            --ethinicity
  `Race` varchar(128) DEFAULT '', 
  `StrokeSurvivorOrCaregiver` varchar(128) DEFAULT NULL,    --stroke survivor or care giver
  `LivingAlone` tinyint(1) DEFAULT NULL,              --living alone or with family/spouse
  `WorkedPriorToStroke` tinyint(1) DEFAULT NULL,      --worked before stroke
  `Nationality` varchar(64) DEFAULT NULL,              --nationality
  `Occupation` varchar(64) DEFAULT NULL,                 --occupation
  `SedentaryLifestyle` tinyint(1) NOT NULL DEFAULT '0', ---sedantary lifestyle or active lifestyle
  `IsSmoker` tinyint(1) NOT NULL DEFAULT '0',             --smoking or not
  `SmokingSeverity` enum('Low','Medium','High','Critical','Unknown') NOT NULL DEFAULT 'Low', --smoking severity level
  `SmokingSince` datetime DEFAULT NULL,                 --start smoking from
  `IsDrinker` tinyint(1) NOT NULL DEFAULT '0',            --drinking alcohol or not
  `DrinkingSeverity` enum('Low','Medium','High','Critical','Unknown') NOT NULL DEFAULT 'Low', --alcohol drinking severity
  `DrinkingSince` datetime DEFAULT NULL,                 --start drinking from
  `SubstanceAbuse` tinyint(1) NOT NULL DEFAULT '0',      --substance abuse or not
  `ProcedureHistory` varchar(512) DEFAULT NULL,           --history of procedures done
  `ObstetricHistory` varchar(512) DEFAULT NULL,           --obstrtric history
  `OtherInformation` varchar(512) DEFAULT NULL,             --any other important information about the user
  `TobaccoQuestion` text,                                      --tobacco questionnaire data
  `TobaccoQuestionAns` tinyint(1) DEFAULT NULL,                --answers to the questions
  `TypeOfStroke` varchar(128) DEFAULT NULL,                      --type of stroke
  `HasHighBloodPressure` tinyint(1) DEFAULT NULL, --blood pressure detail
  `HasHighCholesterol` tinyint(1) DEFAULT NULL, --cholesterol detail
  `HasAtrialFibrillation` tinyint(1) DEFAULT NULL,      --atrial fibrillation detail
  `CreatedAt` datetime DEFAULT NULL, ---created at timestamp     
  `UpdatedAt` datetime NOT NULL,     ---updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,     --deleted at timestamp
  PRIMARY KEY (`id`),
  KEY `PatientUserId` (`PatientUserId`),
  CONSTRAINT `patient_health_profiles_ibfk_1` FOREIGN KEY (`PatientUserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
)

```
##





19. patient_insurances, patient insurance details, health_insurance, insurance_coverage, insurance_plan
``` sql
CREATE TABLE `patient_insurances` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each patient_insurances
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of patient
  `InsuranceProvider` varchar(64) DEFAULT NULL, --insurance provider name
  `InsurancePolicyCode` varchar(64) DEFAULT NULL, ---policy code
  `ValidFrom` datetime DEFAULT NULL,-- insurance valid from
  `ValidTill` datetime DEFAULT NULL,-- insurance valid till
  `CreatedAt` datetime DEFAULT NULL,  --- created at timestamp
  `UpdatedAt` datetime NOT NULL,         --- updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,         --- deleted at timestamp
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```




##




20. patients, details of patient
``` sql
CREATE TABLE `patients` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each patients
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of user
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of person
  `DisplayId` varchar(24) NOT NULL, ---display id of patient
  `NationalHealthId` varchar(32) DEFAULT NULL, --- national health id of patient
  `MedicalProfileId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --- medical profile id
  `TerraUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,  --- Terra User Id
  `TerraProvider` varchar(32) DEFAULT NULL,  --- Terra Provider Name
  `TerraScopes` varchar(256) DEFAULT NULL,   --- Terra Scopes
  `EhrId` varchar(256) DEFAULT NULL,           --- Electronic Health Record Id
  `HealthSystem` varchar(256) DEFAULT NULL,     --- Health System Name
  `AssociatedHospital` varchar(256) DEFAULT NULL, --hospital associated
  `DonorAcceptance` enum('Send','NotSend','Accepted') NOT NULL DEFAULT 'NotSend', -- donor acceptance status
  `IsRemindersLoaded` tinyint(1) NOT NULL DEFAULT '0', -- is reminder loaded or not
  `CreatedAt` datetime DEFAULT NULL,              --- created at timestamp
  `UpdatedAt` datetime NOT NULL,                   --- updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,                 --- deleted at timestamp
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  KEY `PersonId` (`PersonId`),
  CONSTRAINT `patients_ibfk_21` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `patients_ibfk_22` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

##



21. person_addresses, details of person's addresses, 
``` sql
CREATE TABLE `person_addresses` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each person_addresses
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of person
  `AddressId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --- address id of person
  `AddressType` varchar(32) DEFAULT NULL,-- person address type
  `CreatedAt` datetime DEFAULT NULL,               --- created at timestamp
  `UpdatedAt` datetime NOT NULL,                      --- updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,                  --- deleted at timestamp
  PRIMARY KEY (`id`),
  KEY `PersonId` (`PersonId`),
  KEY `AddressId` (`AddressId`),
  CONSTRAINT `person_addresses_ibfk_21` FOREIGN KEY (`PersonId`) REFERENCES `persons` (`id`) ON UPDATE CASCADE,
  CONSTRAINT `person_addresses_ibfk_22` FOREIGN KEY (`AddressId`) REFERENCES `addresses` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```


##

22. person_roles, roles of person, details related to person roles
``` sql
CREATE TABLE `person_roles` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each person_roles
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of person
  `RoleId` int NOT NULL, ---id  of roles
  `RoleName` varchar(32) DEFAULT NULL, --role name
  `CreatedAt` datetime DEFAULT NULL,              ---created at timestamp
  `UpdatedAt` datetime NOT NULL,                      ---updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,                    ---deleted at timestamp
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```


##


23. Persons_details, This is persons sql table. This table represents personal details such as firstname, lastname, email, phone, gender and birthdate. 
``` sql
CREATE TABLE `persons` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each persons
  `Prefix` varchar(16) DEFAULT NULL, ---prefix of person
  `FirstName` varchar(70) DEFAULT NULL, ---first name of person
  `MiddleName` varchar(70) DEFAULT NULL, ---middle name of person
  `LastName` varchar(70) DEFAULT NULL, ---last name of person
  `Phone` varchar(24) NOT NULL, ---phone of person
  `Email` varchar(128) DEFAULT NULL, ---email of person
  `TelegramChatId` varchar(64) DEFAULT NULL, ---telegramchat id of person
  `Gender` enum('Male','Female','Intersex','Other','Unknown') DEFAULT 'Unknown', ---gender of person
  `SelfIdentifiedGender` varchar(128) DEFAULT NULL, 
  `BirthDate` datetime DEFAULT NULL, ---persons birthdate
  `Age` varchar(28) DEFAULT NULL,    ---age of person
  `ImageResourceId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `NationalId` varchar(64) DEFAULT NULL,  ---persons national id
  `NationalIdType` varchar(32) NOT NULL DEFAULT 'Aadhar', ---national id type of person
  `CreatedAt` datetime DEFAULT NULL,               ---created at timestamp
  `UpdatedAt` datetime NOT NULL,                  ---updated at timestamp
  `DeletedAt` datetime DEFAULT NULL,                  ---deleted at timestamp
  PRIMARY KEY (`id`),

  KEY `persons__phone` (`Phone`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```


##



24. role_privileges, role_permissions ,user_privileges , permission details for particular roles
``` sql
CREATE TABLE `role_privileges` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each role_privileges
  `Privilege` varchar(256) NOT NULL, ---privilages to particular role
  `RoleId` int NOT NULL, ---id of role
  `CreatedAt` datetime DEFAULT NULL,                ---timestamp when record was created
  `UpdatedAt` datetime NOT NULL,                       ---timestamp when record was updated
  `DeletedAt` datetime DEFAULT NULL,                       ---timestamp when record was deleted
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```


##


25. roles, roles details 
``` sql
CREATE TABLE `roles` (
  `id` int NOT NULL AUTO_INCREMENT,
  `RoleName` varchar(32) NOT NULL,  ---Unique ID for each roles
  `Description` varchar(256) DEFAULT NULL, --description of the role
  `CreatedAt` datetime DEFAULT NULL,          ---timestamp when record was created
  `UpdatedAt` datetime NOT NULL,                 ---timestamp when record was updated
  `DeletedAt` datetime DEFAULT NULL,                 ---timestamp when record was deleted
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=13 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```


##



26. shared_document_details, shared  document details, documents which are shared by patient  
``` sql
CREATE TABLE `shared_document_details` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each shared_document_details
  `DocumentId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --- id of document
  `ResourceId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,  ---resource id of document
  `PatientUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of patient
  `DocumentType` varchar(128) NOT NULL DEFAULT 'Unknown', ---type of document
  `OriginalLink` text NOT NULL,   ---original document link
  `ShortLink` varchar(256) NOT NULL, ---short link of document
  `Key` varchar(512) NOT NULL, ---key of document
  `SharedWithUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---document shared to userid
  `SharedForDurationMin` int NOT NULL DEFAULT '720', ---duration of document shared
  `SharedDate` datetime DEFAULT NULL,             ---date and time when document is shared
  `CreatedAt` datetime DEFAULT NULL,                ---creation timestamp
  `UpdatedAt` datetime NOT NULL,                       ---update timestamp
  `DeletedAt` datetime DEFAULT NULL,                         ---delete timestamp if document is removed from
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```


##


27. user_device_details, details of user device or mobile phone
``` sql
CREATE TABLE `user_device_details` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each user_device_details
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of user
  `Token` varchar(1024) NOT NULL, --- unique token of device
  `DeviceName` varchar(512) NOT NULL, --- user device name
  `OSType` varchar(256) NOT NULL, --- operating system type
  `OSVersion` varchar(64) NOT NULL, --- operating system version
  `AppName` varchar(256) NOT NULL, --- app name
  `AppVersion` varchar(64) NOT NULL, --- app version
  `ChangeCount` int DEFAULT NULL,      -- number of times the device has been used
  `CreatedAt` datetime DEFAULT NULL,      -- creation date-time stamp
  `UpdatedAt` datetime NOT NULL,            -- update date-time stamp
  `DeletedAt` datetime DEFAULT NULL,            -- delete date-time stamp if record is
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  CONSTRAINT `user_device_details_ibfk_1` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```


##


28. user_login_sessions,  records login sessions of users, login session details of user
``` sql
CREATE TABLE `user_login_sessions` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each user_login_sessions
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of user
  `IsActive` tinyint(1) NOT NULL DEFAULT '1', --- is user session is active or not
  `StartedAt` datetime DEFAULT NULL, -- session started time
  `ValidTill` datetime DEFAULT NULL, --session end time
  `CreatedAt` datetime DEFAULT NULL,       --creation date-time stamp
  `UpdatedAt` datetime NOT NULL,             --update date-time stamp
  `DeletedAt` datetime DEFAULT NULL,             --delete date-time stamp if record is
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  CONSTRAINT `user_login_sessions_ibfk_1` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```


##


29. user_tasks, records tasks assigned to a user, task related to user
``` sql
CREATE TABLE `user_tasks` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --- Unique ID for each user_tasks
  `UserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---id of user
  `DisplayId` varchar(128) DEFAULT NULL, ---display id for user
  `Task` varchar(128) DEFAULT NULL,  --- task which is assigned to the user
  `Category` varchar(128) DEFAULT 'Custom', --- category of the task
  `Description` varchar(256) DEFAULT NULL,--- description of the task
  `ActionType` varchar(64) DEFAULT NULL, ---action type of task
  `ActionId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---actionid of task 
  `ScheduledStartTime` datetime DEFAULT NULL, --task scheluded start time
  `ScheduledEndTime` datetime DEFAULT NULL, --task scheduled end time
  `Started` tinyint(1) NOT NULL DEFAULT '0',---flag for task started or not
  `StartedAt` datetime DEFAULT NULL,
  `Finished` tinyint(1) NOT NULL DEFAULT '0', ---flag for task finished or not
  `FinishedAt` datetime DEFAULT NULL,   
  `Cancelled` tinyint(1) NOT NULL DEFAULT '0',---flag for task cancelled or not
  `CancelledAt` datetime DEFAULT NULL,
  `CancellationReason` varchar(128) DEFAULT NULL, ---cancellation reason
  `IsRecurrent` tinyint(1) NOT NULL DEFAULT '0',
  `RecurrenceScheduleId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --recurring schedule Id
  `CreatedAt` datetime DEFAULT NULL,          --creation date-time stamp
  `UpdatedAt` datetime NOT NULL,                --update date-time stamp
  `DeletedAt` datetime DEFAULT NULL,              --delete date-time stamp if record is deleted
  PRIMARY KEY (`id`),
  KEY `UserId` (`UserId`),
  CONSTRAINT `user_tasks_ibfk_1` FOREIGN KEY (`UserId`) REFERENCES `users` (`id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```

##



30. users, user details, registeration details of user, user credential, user profile information
``` sql
CREATE TABLE `users` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each users
  `PersonId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, --- id of person
  `RoleId` int NOT NULL, --roleid of user
  `UserName` varchar(10) DEFAULT NULL, -- unique username
  `Password` varchar(256) DEFAULT NULL, --password of user
  `LastLogin` datetime DEFAULT NULL, ---last login date and time
  `DefaultTimeZone` varchar(16) NOT NULL DEFAULT '+05:30', ---default time zone
  `CurrentTimeZone` varchar(16) NOT NULL DEFAULT '+05:30', ---current time zone
  `IsTestUser` tinyint(1) NOT NULL DEFAULT '0', -- flag for test user or not
  `CreatedAt` datetime DEFAULT NULL,             --creation date-time stamp
  `UpdatedAt` datetime NOT NULL,                   --update date-time stamp
  `DeletedAt` datetime DEFAULT NULL,                 --delete date-time stamp if record is
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
```


##


31. addresses, this tabel contain the  address detail of a user, address table
``` sql
CREATE TABLE `addresses` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each addresses
  `Type` varchar(16) NOT NULL DEFAULT 'Work', ---type of address
  `AddressLine` varchar(64) NOT NULL, -- full address for particular
  `City` varchar(32) DEFAULT NULL, --city of address
  `Location` varchar(256) DEFAULT NULL, --location of address
  `District` varchar(32) DEFAULT NULL, --district of address
  `State` varchar(32) DEFAULT NULL, --state of address
  `Country` varchar(128) DEFAULT NULL, --country
  `PostalCode` varchar(16) DEFAULT NULL,--postal code of address
  `Longitude` float DEFAULT NULL, ---longitute of address
  `Lattitude` float DEFAULT NULL, ---lattitude of address
  `CreatedAt` datetime DEFAULT NULL,          --creation date-time stamp
  `UpdatedAt` datetime NOT NULL,                --update date-time stamp
  `DeletedAt` datetime DEFAULT NULL,                --delete date-time stamp if record is
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

##



32. organizations, details related to organizations, organization table, organization profile
``` sql
CREATE TABLE `organizations` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL, ---Unique ID for each organizations
  `Name` varchar(64) DEFAULT '',
  `Type` enum('Clinic','Hospital','Diagnostic Lab','Diagnostic Lab - Pathology','Diagnostic Lab - Imaging','Pharmacy','Ambulance Service','Government Primary Health Care Centre','Government Nodal Hospital','Government District Hospital','Municipal Hospital','Blood Bank','Nursing Home','Specialized Care Centre','Ambulatory Procedure Centre','Social Health','Unknown') NOT NULL DEFAULT 'Unknown', ---name of organization
  `ContactUserId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, --- contactid of user from organization's member
  `ContactPhone` varchar(16) NOT NULL, ---contact number of organization's member
  `ContactEmail` varchar(50) DEFAULT NULL, ---contact email of organization's member
  `About` varchar(512) DEFAULT NULL, ---organizations detail
  `ParentOrganizationId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL, ---parentorganizationid of this orgnization
  `OperationalSince` datetime DEFAULT NULL, ---date from organization is working
  `ImageResourceId` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `IsHealthFacility` tinyint(1) NOT NULL DEFAULT '1', 
  `NationalHealthFacilityRegistryId` varchar(64) DEFAULT NULL, ---id of national facility registry
  `CreatedAt` datetime DEFAULT NULL,           --creation date-time stamp
  `UpdatedAt` datetime NOT NULL,                 --update date-time stamp
  `DeletedAt` datetime DEFAULT NULL,               --delete date-time stamp if record is
  PRIMARY KEY (`id`),
  KEY `organizations__contact_phone` (`ContactPhone`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```
``` sql 
---users.PersonId can be joined with persons.id
---user_tasks.UserId can be joined with users.id
---user_login_sessions.UserId can be joined with users.id
---user_device_details.UserId can be joined with users.id
-- role_privileges.RoleId can be joined with roles.id
-- person_roles.PersonId can be joined with persons.id
-- person_addresses.PersonId can be joined with persons.id
--  person_addresses.AddressId can be joined  with addresses.id
-- patients.PersonId can be joined with persons.id
--  patients.UserId can be joined with users.id
-- patient_insurances.PatientUserId can be joined with patients.id
-- patient_health_profiles.PatientUserId can be joined with users.id
-- patient_goals.PatientUserId can be joined with users.id
-- patient_emergency_contacts.PatientUserId can be joined with users.id
-- patient_emergency_contacts.ContactPerson can be joined with persons
-- patient_emergency_contacts.AddressId  can be joined with addresses.id
-- patient_emergency_contacts.OrganizationId can be joined with organizations.id
-- patient_documents.PatientUserId can be joined with users.id
-- otp.UserId can be joined with users.id
-- health_priorities.PatientUserId can be joined with users.id
-- health_priorities.UserId can be joined with users.id
-- doctors.PersonId  can be joined with persons.id
-- custom_tasks.UserId can be joined with users.id
-- blood_donors.UserId can be joined with users.id
--  blood_donors.PersonId can  be joined with persons.id
-- blood_donation_volunteers.UserId can be joined with users.id
-- blood_donation_volunteers.PersonId  can be joined with persons.id
--- biometrics_body_weight.PatientUserId can be joined with users.id
--- biometrics_blood_cholesterol.PersonId can be joined with persons.id
--- biometrics_blood_glucose.PersonId can be joined with persons.id
--- biometrics_blood_oxygen_saturation.PatientUserId can be joined with users.id
--- biometrics_blood_pressure.PersonId can be joined with persons.id
--- biometrics_body_height.PersonId can be joined with persons.id
---  biometrics_body_height.PatientUserId can be joined with users.id
--- biometrics_body_temperature.PatientUserId can be joined with users.id
```