---
title: 사용자 프로필
feature: Mobile Marketing, Users and Roles
description: Marketo Mobile에서 사용자 프로필 사용
exl-id: 1b2cfb7f-d678-4022-8cd9-a56004a1ac46
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 사용자 프로필

사용자 프로필을 만드는 방법

1. [iOS에서 사용자 프로필 만들기](#ios_user_profiles)
1. [Android에서 사용자 프로필 만들기](#android_user_profiles)

## iOS에서 사용자 프로필 만들기 {#ios_user_profiles}

아래와 같이 사용자 필드를 전송하여 리치 프로필을 만들 수 있습니다.

```
MarketoLead *profile = [[MarketoLead alloc] init];

// Get user profile from network and populate
[profile setEmail:@"jd@makesomething.com"];
[profile setFirstName:@"John"];
[profile setLastName:@"Doe"];
[profile setAddress:@"1234KingFishSt"];
[profile setCity:@"SouthPadreIsland"];
[profile setState:@"CA"];
[profile setPostalCode:@"78596"];
[profile setCountry:@"USA"];
[profile setGender:@"male"];
[profile setLeadSource:@"_facebook_ads"];
[profile setBirthDay:@"01/01/1985"];
[profile setFacebookId:@"facebookid"];
[profile setFacebookProfileURL:@"facebook.com/profile"];
[profile setFacebookProfilePicURL:@"faceboook.com/profile/pic"];
[profile setLinkedInId:@"linkedinid"];
[profile setTwitterId:@"twitterid"];
```

```
let profile =  MarketoLead()

// Get user profile from network and populate
profile.setEmail("jd@makesomething.com")
profile.setFirstName("John")
profile.setLastName("Doe")
profile.setAddress("1234KingFishSt")
profile.setCity("SouthPadreIsland")
profile.setState("CA")
profile.setPostalCode("78596")
profile.setCountry("USA")
profile.setGender("male")
profile.setLeadSource("_facebook_ads")
profile.setBirthDay("01/01/1985")
profile.setFacebookId("facebookid")
profile.setFacebookProfileURL("facebook.com/profile")
profile.setFacebookProfilePicURL("faceboook.com/profile/pic")
profile.setLinkedInId("linkedinid")
profile.setTwitterId("twitterid")
```

[표준 필드](../rest-api/list-of-standard-fields.md)를 더 추가합니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```
// Add other custom fields
[profile setFieldName:@"mobilePhone"withValue:@"123.456.7890"];
[profile setFieldName:@"numberOfEmployees"withValue:@"10"];
[profile setFieldName:@"phone"withValue:@"123.456.7890"];
```

>[!TAB Swift]

```
// Add other custom fields
profile.setFieldName("mobilePhone" , withValue :"123.456.7890");
profile.setFieldName("numberOfEmployees", withValue: "10");
profile.setFieldName("phone", withValue:"123.456.7890");
```

>[!ENDTABS]

보고서 사용자 프로필.

>[!BEGINTABS]

>[!TAB 목표 C]

```
Marketo *sharedInstance = [Marketo sharedInstance];

// This method will update user profile
[sharedInstance associateLead:profile];
```

>[!TAB Swift]

```
let marketo = Marketo.sharedInstance()

// This method will update user profile
marketo.associateLead(profile)
```

>[!ENDTABS]

## Android에서 사용자 프로필 만들기 {#android_user_profiles}

1. 사용자 프로필을 만듭니다.

   아래와 같이 사용자 필드를 전송하여 리치 프로필을 만들 수 있습니다.

   ```java
   MarketoLead profile = new MarketoLead();
   
   // Get user profile from network and populate
   try {
       profile.setEmail("htcone3@gmail.com");
       profile.setFirstName("Mike");
       profile.setLastName("Gray");
       profile.setFacebookId("facebookid");
       profile.setAddress("1234 King Fish Blvd");
   }
   catch (MktoException e) {
       e.printStackTrace();
   }
   ```

1. [표준 필드](../rest-api/list-of-standard-fields.md)를 더 추가합니다.

   ```java
   // Add other custom fields
   profile.setCustomField("mobilePhone", "123.456.7890");
   profile.setCustomField("numberOfEmployees", "10");
   profile.setCustomField("phone", "123.456.7890");
   profile.setCustomField("rating", "R");
   profile.setCustomField("facebookDisplayName", "mini");
   profile.setCustomField("facebookReach", "10");
   profile.setCustomField("facebookReferredEnrollments", "100");
   profile.setCustomField("facebookReferredVisits", "9998");
   profile.setCustomField("lastReferredEnrollment", "03/01/2015");
   profile.setCustomField("lastReferredVisit", "03/01/2015");
   profile.setCustomField("linkedInDisplayName", "Android");
   ```

1. 보고서 사용자 프로필.

   ```java
   MarketoLead profile = new MarketoLead();
   
   // This method will update user profile
   marketoSdk.associateLead(profile);
   ```
