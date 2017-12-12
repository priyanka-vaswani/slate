---
title: EyeCareLive API Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
 

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/acme'>Client libraries</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - patientuserprofile
  - doctors
  - videovisits
  - treatmentplan
  - messaging
  - errors

search: true
---

# Introduction

Patient is the main user of the Eyecarelive mobile app. Eyecarelive app is designed to guide the users to use the app for appropriate conditions only. There are four modules currently supported in the app. Each module addresses a specific type of a virtual visit and is backed by a self-guiding questionnaire to collect relevant information for the doctors. The modules in current release of the app are:

*  General consultation - Generic and non-urgent conditions such as garden variety pink eye or a quick question about trivial condition

* Dry eye visit - Patients take a validated SPEEDTM test to self-evaluate their dry eye condition. Doctors recommend patients to use the app for Dry eye test during their in-office visit. Dry eye test series can be tracked by the patients and the doctors by using the SPEED test scores.  
* Contact Lens consultation - Patients can use the app related to contact lens questions, concerns or follow-up with their doctors. Contact lens module is designed to collect subjective data from the patient which allows doctors to evaluate seriousness of their condition

* Post-Op or Lasik follow-up care - Lasik surgeons may recommend patients to use the app for scheduled post-op follow ups. Post-op follow-up module is designed by Lasik specialist to collect pertinent information for follow-up care.

#Create User

## New User

```shell
curl -k -i -H "Content-Type: application/json" "http://52.7.202.98:8080/DoctorOnDemand/api/auth/signup" -X POST -d '{"email":"patientuser@cooldoctors.io","password":"demo1234","aboutMe":{"firstName":"Patient","lastName":"Name","address":"Kallam Anji Reddy Campus,","city":"Hyderabad","country":"India","birthDate":"08/23/1991","state":"Telangana","pincode":"500034","gender":"Male"},"role":{"id":"551ad2a4e4b0b59ff0ccecc9","name":"patient"},"contactInfo":{"email":"patientuser@cooldoctors.io","phone":"8806900740"}}'
 
```
> The above command returns JSON structured like this:

```json
{
  "id": "5a2c0a69e4b0e4fa266e0180",
  "email": "patientuser@cooldoctors.io",
  "pharmacyName": null,
  "pharmacyAddress": null,
  "profileImageId": null,
  "profileImageName": null,
  "aboutMe": {
    "id": "5a2c0a69e4b0e4fa266e017d",
    "firstName": "Patient",
    "lastName": "Name",
    "birthDate": null,
    "address": "Kallam Anji Reddy Campus, Banjara Hills",
    "city": "Hyderabad",
    "country": "India",
    "pincode": "500034",
    "gender": "Female",
    "languagesSpeak": null,
    "additionalInfo": null,
    "state": "Telangana"
  },
  "contactInfo": {
    "id": "5a2c0a69e4b0e4fa266e017f",
    "email": "patientuser@cooldoctors.io",
    "phone": "610-469-4012",
    "smsNotification": false,
    "countryCode": null,
    "country": null,
    "emlNt": false
  },
  "patientInfo": null,
  "doctorInfo": null,
  "role": {
    "id": "551ad2a4e4b0b59ff0ccecc9",
    "name": "patient"
  },
  "timezone": {
    "id": "55f283b4e4b029528c27d0c5",
    "timezone": "Asia/Kolkata",
    "displayName": "India Standard Time"
  },
  "createdAt": "2017-12-09 08:08 AM PST",
  "forgotPasswordToken": null,
  "familyMembers": null,
  "parentUser": null,
  "parentUserRelation": null,
  "password": null,
  "rating": null,
  "preferredPharmacies": null,
  "kandyUserName": null,
  "kandyUserPassword": null,
  "kandyFullUserId": null,
  "oldPassword": null,
  "loginStatus": null,
  "stripeCustId": null,
  "profileImagePath": null,
  "isReferredDoctor": null,
  "randomtoken": "5Ys5Ad",
  "isEmailVerified": false,
  "doctorsGroups": null,
  "preferredDoctors": null,
  "isAcceptTC": false,
  "insurenceCards": null,
  "notificationSettings": {
    "id": "5a2c0a69e4b0e4fa266e017e",
    "addTestreport": true,
    "addTreatmentPlan": true,
    "sendReminderForEyeTest": true,
    "sendReminderForMedicine": true,
    "sentMessage": true
  },
  "clinics": null,
  "passCode": null,
  "emrId": null,
  "ssnId": null,
  "clinicInfo": null,
  "ref": null,
  "docOrg": null,
  "doctorsOrg": null,
  "twilioAccessToken": null,
  "invited": false,
  "validated": true,
  "activated": true,
  "managedUser": false,
  "addedByCpm": false,
  "pilotDoc": false
}
```
> Make sure to replace `meowmeowmeow` with your API key.

Create new user with email address and password. This user is referred as Primary user of the app. Eyecarelive supports two roles of users - Patients and Doctors. When creating a new user, Role option must be specified. For creating a patient user, a fixed id# is required to be specified in the API

### HTTP Request

`POST
http://localhost:8080/DoctorOnDemand/api/auth/signup
`
### Query Parameters

Parameter |  Description | Type | Optional/Required
--------- | ------------ | ---- | ----------------
Email | User’s Email address | String | Required
Password | User’s Password | String | Required
  | **About Me** |   |
FirstName | User’s First Name | String | Required
LastName | User’s Last Name | String | Required
Address | User’s Address | String | Optional
City | City | String | Optional
Country | Country | String | Optional
BirthDate | Date of Birth (MM/DD/YYYY) | String | Optional
Pincode | Zip code | Integer | Optional
Gender | Gender (M,F) | String | Optional
 | **Role** | |
ID | Role (ID) Always use “551ad2a4e4b0b59ff0ccecc9” | Integer | Required
Name | Role Name Always Use “patient” | String | Required
 | **Contact Info** |  |
Email | Contact Email Address | String | Optional
Phone | Contact Number | Integer | Optional

### Response

Parameter | Description | Type 
--------- | ----------- | ----
ID | User id# | Integer
Email | User Email address | String
Preferred Pharmacy [{}] | Preferred Pharmacy | String
profileImagePath | Profile photo URL | String
About Me :[{}] | About me info for the user | String
Contact Info:[{}] | Contact person Info | String
Patient Info :[{}] | Patient info | String
Time zone | Time zone | String
Created At:[{}] | Date and Time Created at | String


<aside class="success">
Patient is signed up successfully!
</aside>



# Authentication

User authentication is implemented by email address and password

## Login - Login User - Logs the user in the app

```shell
curl -i -H "Content-Type: application/json" "http://52.7.202.98:8080/DoctorOnDemand/api/auth/login" -X POST -d '{"email" : "patientuser@cooldoctors.io","password" : "demo1234"}'
```
> The above command returns JSON structured like this:

```json
{
  "id": "5a2c0c91e4b0e4fa266e0181",
  "userId": "5a2c0a69e4b0e4fa266e0180",
  "token": "patientuser@cooldoctors.io:patient:1515428241291:5eb24f92a4160a1864abb7738802e449",
  "dateTime": "2017-12-09 08:17 AM PST"
}
```
### HTTP Request

`POST http://localhost:8080/DoctorOnDemand/api/auth/login
`
### Query Parameters

Parameter |  Description | Type | Optional/Required
--------- | ------------ | ---- | ----------------
Email | Patient’s Email address | String | Required
Password | Patient’s Password | String | Required

### Response

Parameter |  Description | Type 
--------- | ------------ | ---- 
ID | Internal system id#. Deprecated | Integer 
USER ID | User ID of Patient | Integer
TOKEN | Authentication Token | String
Date Time | User account created date and time | String

<aside class="success">
 Correct Email and Password leads to successful login!
</aside>

## Logout - User logout - Logs the user out of the patient app

```shell
curl -i -H "Content-Type: application/json" -H "X-Auth-Token:patientuser@cooldoctors.io:patient:1515428241291:5eb24f92a4160a1864abb7738802e449" "http://52.7.202.98:8080/DoctorOnDemand/api/auth/logout"  -X POST
```
> The above command returns JSON structured like this:

```json
{"success":true}
```
### HTTP Request

`POST http://localhost:8080/DoctorOnDemand/api/auth/logout
`
### Query Parameters

Parameter |  Description | Type | Optional/Required
--------- | ------------ | ---- | ----------------
ID | User’s ID | Integer | Required
Token | User’s authentication token | Integer | Required


### Response

Parameter |  Description | Type
--------- | ------------ | ----
Success | Logout successful True OR False | String

<aside class="notice">
ID and Token are must to be successfully logged out!
</aside>


