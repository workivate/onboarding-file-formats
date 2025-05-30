# Telus Health Automated Onboarding - Supported File formats

## Purpose
Few file types can be used by clients to upload user and/or company data:
 - companies data (originator upload) --> supported via SFTP
 - companies + users data --> supported via SFTP
 - users data --> supported via Admin-Panel (Zeus) and SFTP

File schemas are defined in this repository:
 - `full_import.schema.json` --> used by SFTP uploads
 - `user_import.schema.json` --> used by FFU uploads (Full File Uploads via Admin-Panel / Zeus)

File schemas are used to validate field names and record values of uploaded files.

Note: .csv schemas are prepared, but not currently in use by the onboarding apps


## Supported file formats
Onboarding pipeline supports file formats:
 - `csv` / `tsv` --> comma / tab separated values as text files
 - `xls` / `xlsx` --> excel files

You can access schemas and example files [here](json/).

Fields description, examples and validation rules are below. Passed validation of field names and file records doesn't guarantee successful import, but it eliminates the vast majority of potential user errors.

## File requirements
* Text files should be either encoded in UTF-8 / UTF-16 or use only English characters with ANSI encoding
* Files must have `.csv` / `.tsv` / `.xls` / `.xlsx` extension indicating their format
* File should always contain ALL user records (including inactive/terminated users)
* Files should be added as new files and should not overwrite existing files held on the SFTP, therefore we recommend using a date & timestamp in the filename generation process

## Properties

 Property           | Description                                                                     | Format                                                        | Examples                                                                   | Originator import required           | User only import required            | Notes
------------------  |---------------------------------------------------------------------------------|---------------------------------------------------------------|----------------------------------------------------------------------------|--------------------------------------|--------------------------------------| --------------------------------
 company_id         | Unique company identifier                                                       | Text, Max length 36                                           | C121523245                                                                 | True                                 | False                                |
 company_name       | Name of the Company as it should appear on platform                             | Text, Max length 255                                          | Example Inc                                                                | True                                 | False                                |
 employee_id        | Unique Employee Id                                                              | Text, Max length 36                                           | EID123456                                                                  | True, if User email address is empty | True, if User email address is empty |
 email              | User email address                                                              | Email address as defined in RFC 5322                          | email@example.com                                                          | True, if Unique Employee Id is empty | True, if Unique Employee Id is empty |
 first_name         | User first name                                                                 | Text, Max length 255                                          | Jon                                                                        | False                                | False                                |
 last_name          | User Last name                                                                  | Text, Max length 255                                          | Doe                                                                        | False                                | False                                |
 activation_date    | User activation date                                                            | Date from which account should be active in ISO 8601 format   | 2018-10-23                                                                 | False                                | False                                | Default current date if empty
 termination_date   | User termination date                                                           | Date on which account should be terminated in ISO 8601 format | 2020-10-23                                                                 | False                                | False                                |
 country_code       | User country code                                                               | 2 letters ISO 3166-1 country code                             | GB                                                                         | False                                | False                                |
 locale             | User locale                                                                     | ISO 3166-1 Country code and ISO 639-1 language code           | en_GB                                                                      | False                                | False                                |
 job_title          | Job title                                                                       | Text, Max length 255                                          | Sales manager                                                              | False                                | False                                |
 group              | Group name to which user should be assigned                                     | Text, Max length 255                                          | HR, Sales                                                                  | False                                | False                                | Used only if grouping is enabled
 gender             | Gender                                                                          | Choice: female, male, other                                   | female                                                                     | False                                | False                                |
 phone_mobile       | Mobile phone of the user                                                        | Phone number in international format                          | +447474747474                                                              | False                                | False                                |
 phone_work         | Work phone of the user                                                          | Phone number in international format                          | +447474747474                                                              | False                                | False                                |
 birthday           | User birth date                                                                 | Date in ISO 8601 format                                       | 2018-10-23                                                                 | False                                | False                                |
 work_start         | User employment start date                                                      | Date in ISO 8601 format                                       | 2018-10-23                                                                 | False                                | False                                |
 region             | Region of work of the individual                                                | Text, Max length 255                                          | Europe, Africa, Canada, Pennsylvania, Western USA                          | False                                | False                                |
 sub_region         | Sub region of work of the individual                                            | Text, Max length 255                                          | Canada/US, Middle America, South America, Southern Ontario, Niagara Region | False                                | False                                |
 city               | City of work of the individual                                                  | Text, Max length 255                                          | New York, London, Toronto                                                  | False                                | False                                |
 location_site      | Location or site out of which the individual works                              | Text, Max length 255                                          | Head office, Bay Office, Don Mills Office                                  | False                                | False                                |
 work_status        | Work status of the individual (e.g. Active, STD, LTD, leave, terminated, etc)   | Text, Max length 255                                          | Active, terminated, STD, LTD, Family Leave                                 | False                                | False                                |
 management_status  | Designation of whether or not the person manages individuals                    | Text, Max length 255                                          | Manager, Employee, Individual Contributor, Member                          | False                                | False                                |
 job_level          |                                                                                 | Text, Max length 255                                          | Executive, management, employee                                            | False                                | False                                |
 division           | Highest level department/division/group of the individual                       | Text, Max length 255                                          | Finance, IT, Corporate                                                     | False                                | False                                |
 division_sub1      | Second highest level department/division/group of the individual                | Text, Max length 255                                          | Billing                                                                    | False                                | False                                |
 division_sub2      | Third highest level department/division/group of the individual                 | Text, Max length 255                                          | Accounts Payable, Accounts Receivable                                      | False                                | False                                |
 division_sub3      | Fourth highest level department/division/group of the individual                | Text, Max length 255                                          | See row 8-10 for examples                                                  | False                                | False                                |
 division_sub4      |                                                                                 | Text, Max length 255                                          | See row 8-10 for examples                                                  | False                                | False                                |
 division_sub5      |                                                                                 | Text, Max length 255                                          | See row 8-10 for examples                                                  | False                                | False                                |
 occupation         | Occupation of the individual                                                    | Text, Max length 255                                          | Lawyer, doctor, accountant                                                 | False                                | False                                |
 union_status       | Union status of the individual (e.g. union, non-union)                          | Text, Max length 255                                          | Non union, Local 538, Local 358                                            | False                                | False                                |
 pay_type           | Pay type of the individual (e.g. hourly, salary, commission)                    | Text, Max length 255                                          | Salary, Hourly, Commission                                                 | False                                | False                                |
 salary             | Salary of the individual                                                        | Text, Max length 255                                          | 35,235                                                                     | False                                | False                                |
 preferred_language | Preferred language of communication for the individual (e.g. English, etc)      | Text, Max length 255                                          | English, French, Spanish                                                   | False                                | False                                |
 custom_cut1        | First custom demographic field of  the individual (unique to the organization)  | Text, Max length 255                                          | Blue, green, purple                                                        | False                                | False                                |
 custom_cut2        | Second custom demographic field of  the individual (unique to the organization) | Text, Max length 255                                          | Health, financial                                                          | False                                | False                                |
 custom_cut3        | Third custom demographic field of  the individual (unique to the organization)  | Text, Max length 255                                          | Yes, no                                                                    | False                                | False                                |
 custom_cut4        | Fourth custom demographic field of  the individual (unique to the organization) | Text, Max length 255                                          | 31Wing                                                                     | False                                | False                                |
 custom_cut5        | Fifth custom demographic field of  the individual (unique to the organization)  | Text, Max length 255                                          | Could be anything                                                          | False                                | False                                |
 sso                | Indicates whether the user should be accessing by SSO or not                    | Choice: yes, no                                               | yes                                                                        | False                                | False                                |
 roles              | Set of user roles                                                               | Text, Max length 255, comma-separated                         | "admin,user"                                                               | False                                | False                                | If more than 1 role -> string in "" to escape comma
 otp                | One time password, provided by the employer, which has to be confirmed by user  | Text, Max length 32                                           | abc-ABC/123                                                                | False                                | False                                | Only letters and numbers "/" and "-"
 invitecode         | This is added to the company's prefix to generate the unique registration code. | Text                                                          | example@code                                                               | False                                | False                                | DO NOT include the registration code prefix!
 telemed_eligible   | Indicates whether the user can have telemed or not                              | Choice: yes, no                                               | yes                                                                        | False                                | False                                |
 company_type       | Describes the type of company it is (optional)                                  | Text, Max length 255                                          | Non EAP, Endorsed, Embedded, etc                                           | True                                 | False                                | Originators who want to use this are free to set their own labels
 authentication_id  | Additional internal user ID, potentially used for reporting (optional)          | Text, Max length 36                                           | "123abc", Any string                                                       | False                                | False                                |
 restricted_access                | Indicates whether the users from outside of a given region should be restricted from accessing the platform                    | Choice: yes, no                                               | yes                                                                        | False                                | False                                |
 policy_id          | Additional company field that can be used to group companies(optional)          | Text, Max length 255                                          | "123abc", Any string                                                       | True                                 | False                                |

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

The schemas for user-only files are named `user_import.*`. These are meant for validation of files that contain only employee records for a single company, so the `company_id` and `company_name` properties are not applicable in this case and should not be in the file.
