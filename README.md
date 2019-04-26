# LifeWorks Automated Onboarding - Supported File formats

The purpose of this repository is to provide assistance for producing valid input files for the onboarding process in a number of different formats. 

Currently we support [Comma-separated values (CSV)](csv/) format, but [JavaScript Object Notation (JSON)](json/) and [Extensible Markup Language (XML)](xml/) is on the way.
  
There is an explanation on what fields to use with what kind of contents, as well as examples, and schemas to validate an input file against. Although it is not guaranteed that an input file that is valid against the correct schema will be imported without errors, the schema validation can eliminate the vast majority of the potential errors so it could be a helpful part of the process.

## File requirements
* All files regardless of the file format must be UTF-8 encoded without BOM
* Files should have one of the following extensions: (xml, json, csv) indicating its format
* File should always contain ALL user records (including inactive/terminated users)
* Records in file should be sorted by `company_id` and then User primary key field (either `employee_id` or `email`)
* Files should be added as new files and should not overwrite existing files held on the SFTP, therefore we recommend using a date & timestamp in the filename generation process

## Properties

 Property         | Description                                          | Format                                                         | Examples           | Required                             | Notes
----------------- | ---------------------------------------------------- | ---------------------------------------------------------------| ------------------ | ------------------------------------ | --------------------------------
 company_id       | Unique company identifier                            | Text, Max length 36                                            | C121523245         | True                                 |
 company_name     | Name of the Company as it should appear on platform  | Text, Max length 255                                           | Example Inc        | True                                 |
 employee_id      | Unique Employee Id                                   | Text, Max length 36                                            | EID123456          | True, if User email address is empty |
 email            | User email address                                   | Email address as defined in RFC 5322                           | email@example.com  | True, if Unique Employee Id is empty |
 first_name       | User first name                                      | Text, Max length 255                                           | Jon                | False                                |
 last_name        | User Last name                                       | Text, Max length 255                                           | Doe                | False                                |
 activation_date  | User activation date                                 | Date from which account should be active in ISO 8601 format    | 2018-10-23         | False                                | Default current date if empty
 termination_date | User termination date                                | Date on which account should be terminated in ISO 8601 format  | 2020-10-23         | False                                |
 country_code     | User country code                                    | 2 letters ISO 3166-1 country code                              | GB                 | False                                |
 locale           | User locale                                          | ISO 3166-1 Country code and ISO 639-1 language code            | en_GB              | False                                |
 job_title        | Job title                                            | Text, Max length 255                                           | Sales manager      | False                                |
 group            | Group name to which user should be assigned          | Text, Max length 255                                           | HR, Sales          | False                                | Used only if grouping is enabled
 gender           | Gender                                               | Choice: female, male, other                                    | female             | False                                | 
 phone_mobile     | Mobile phone of the user                             | Phone number in international format                           | +447474747474      | False                                | 
 phone_work       | Work phone of the user                               | Phone number in international format                           | +447474747474      | False                                | 
 birthday         | User birth date                                      | Date in ISO 8601 format                                        | 2018-10-23         | False                                | 
 work_start       | User employment start date                           | Date in ISO 8601 format                                        | 2018-10-23         | False                                | 


### Activation and termination dates
Those fields have a special meaning in our platform, and there is additional logic around those values:

**Activation date**:
 * can be edited only if current activation date is in future (user hasn't been activated yet)
 * activation date can't be set in past, (you can set any date that is later or equal to the current date)

**Termination date**:
 * can be edited only if current termination date is in future (account is still active)
 * termination date can be set only to future counting from midnight UTC on the day file has been sent for processing

### Primary key

**User** - Our system supports two types of primary keys - `employee_id` and `email`, at least one of those fields must be present and not empty. Our system will first try to use `employee_id` and then tailback to `email` if value of `employee_id` is empty. You MUST always use same primary key for all records. Changing the primary key without separate agreements cannot be supported. A change in primary key may result in account duplication or permanent removal. 

**Company** - Company is always identified by `company_id`.  `company_id` must not change, as that will trigger the removal of the existing network and creation of a new one.

## User-only files

There are schemas for user-only files as well. These schemas are named `user_import.*`. These are meant for validation of files that contain only employee records for a single company. The use case for these files is different to the full import. One use case is for example the file uploads in the admin panel where the company details will depend on which company's employee accounts is the user managing, so the company details come from another source and are not in the same scope as the data to be imported.
