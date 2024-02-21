Few shots for particular table:

1. biometrics_body_temperature

``` sql
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
```




2. biometrics_body_height
``` sql
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
```




3. biometrics_blood_pressure
``` sql
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
```


4. biometrics_blood_oxygen_saturation
``` sql
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
```



5. biometrics_blood_glucose
``` sql
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
```



6. biometrics_blood_cholesterol
``` sql
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
```



7. biometrics_body_weight
``` sql
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
```



8. blood_donation_volunteers
``` sql
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
```





9. blood_donors
``` sql
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
```


10. custom_tasks
``` sql
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
```



11. doctors
``` sql
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
```





12. health_priorities
``` sql
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
```



 
13. health_priority_types
``` sql
CREATE TABLE `health_priority_types` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `Type` varchar(256) NOT NULL,
  `Tags` varchar(512) DEFAULT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```



14. otp
``` sql
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
```


    
15. patient_documents
``` sql
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
```




16. patient_emergency_contacts
``` sql
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
```




17. patient_goals
``` sql
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
```


18. patient_health_profiles
``` sql
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
```

 



19. patient_insurances
``` sql
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
```



20. patients
``` sql
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
```



21. person_addresses 
``` sql
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
```




22. person_roles
``` sql
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
```


23. persons
``` sql
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
```




24. role_privileges
``` sql
CREATE TABLE `role_privileges` (
  `id` char(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `Privilege` varchar(256) NOT NULL,
  `RoleId` int NOT NULL,
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```


25. roles
``` sql
CREATE TABLE `roles` (
  `id` int NOT NULL AUTO_INCREMENT,
  `RoleName` varchar(32) NOT NULL,--rolenname
  `Description` varchar(256) DEFAULT NULL, --description of the role
  `CreatedAt` datetime DEFAULT NULL,
  `UpdatedAt` datetime NOT NULL,
  `DeletedAt` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=13 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```




26. shared_document_details
``` sql
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
```



27. user_device_details
``` sql
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
```



28. user_login_sessions
``` sql
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
```



29. user_tasks
``` sql
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
```



30. users
``` sql
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
```



31. addresses
``` sql
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
```
