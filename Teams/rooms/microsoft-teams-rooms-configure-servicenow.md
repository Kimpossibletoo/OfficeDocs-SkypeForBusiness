---
title: Configure ServiceNow for Teams Rooms
author: tonysmit
ms.author: tonysmit
manager: kimmatlock
ms.reviewer: kimmatlock
ms.date: 09/19/2023
ms.topic: article
ms.service: msteams
ms.subservice: itpro-rooms
audience: Admin
appliesto: 
  - Microsoft Teams
localization_priority: Normal
description: Learn about configuring ServiceNow in the Teams Rooms Pro Management portal
f1keywords: 
ms.collection: 
  - M365-collaboration
  - teams-rooms-devices
  - Tier3
---

# Configure ServiceNow for Teams Rooms Pro Management

Teams Rooms Pro Management provides a basic integration with ServiceNow using ServiceNow's Table API. This article describes the prerequisites and steps to configure your ServiceNow environment in the Teams Rooms Pro Management portal.

## Watch: Microsoft Teams Rooms Pro Management — Service Now Integration

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4ZK4B]


### Teams Rooms Pro Management prerequisites

- You must have an assigned Pro Manager role. For more information, see [Role-based access control with Microsoft Teams Rooms Pro Management](rooms-pro-rbac.md).

### ServiceNow prerequisites

- A Basic Authorization sign-in, OR an [OAuth2.0](https://docs.servicenow.com/bundle/rome-platform-administration/page/administer/security/concept/c_OAuthApplications.html) sign-in. For more information, see [Creating Credentials](https://developer.servicenow.com/dev.do#!/learn/learning-plans/rome/servicenow_application_developer/app_store_learnv2_rest_rome_creating_credentials) in ServiceNow.
- A ServiceNow instance and its instance host name and API URI  
- A role of incident_manager or higher
- A software version of ServiceNow that supports Table API

## Configure your environment

How your ServiceNow environment is configured can be highly customized and will depend on your organization's needs. The Teams Rooms Pro Management ServiceNow integration must have all your ServiceNow Incident form required (asterisks) field values mapped with the actual database field name and corresponding field values for the integration to work properly. 

The following steps walk through how to map your existing incident form configuration in ServiceNow to the Teams Rooms Pro Management portal.  

1. Open the ServiceNow Incident form in your ServiceNow instance. You'll need to reference your Service Now Incident form's required fields and field values as you complete the configuration form in the Teams Rooms Pro Management portal. 
2. In a new browser tab, go to the [Teams Rooms Pro Management portal](https://portal.rooms.microsoft.com/) and go to **Settings**. Then, select **ServiceNow** in the left navigation menu to open the configuration form.
3. Select an authentication method that the Table API will use to sign in. Both Basic and Oauth2.0 methods are supported.
4. Enter your ServiceNow Instance Host. You will only need the prefix hostname. The URL will be dynamically created. It is best to test the configuration using your ServiceNow's developer or QA instance first.  Once you are satisfied with how the configuration is working within your test environment, you would need to re-assign the configuration to your production instance, if desired.
5. Enter the Incident table's API URI.  The API URI should be api/now/table/incident. If your ServiceNow Incident URI has a different path definition, this integration will not work for you.
6. All Teams Rooms Pro Management required items in the ServiceNow Field column of the Field Mapping section are pre-filled. The table below contains each ServiceNow field and its corresponding Teams Rooms Pro Management field. Complete the action for each row of the Field Mapping section. For definitions of each ServiceNow field, see [ServiceNow field definitions](#servicenow-field-definitions).

| ServiceNow field | Microsoft Teams Rooms field | Action |
| --- | --- | --- |
| short_description | Incident description | No action needed. The Teams Rooms Pro Management field is auto-filled. |
| description | First Message | No action needed. The Teams Rooms Pro Management field is auto-filled. |
| assignment_group | Room group | Enter the assignment_group value from your ServiceNow instance where you want Teams Rooms Pro Management incidents to be routed. If you have more than one assignment_group, select **Add Room Group** for each additional custom value. |
| severity | Rings | Severity is a custom value in ServiceNow. You may or may not use this field but it is necessary to be defined. Enter the value into the ServiceNow value field in the configuration form. If you have more than one severity value, select **Add Ring** for each additional custom value. If you don't use the Severity field, the default value is typically the number three (3). |
| Other Required * fields (optional) | Custom value* | To add other required fields on your Incident form to the configuration form, select **Add** at the top of the field  mapping section. Enter the database field name value. It is case-sensitive. Select Custom Value from the drop down. Enter the field value that should be passed from the configuration. Do this for all remaining required fields. |
| state (resolved) | Custom value* | Copy the resolution state from your ServiceNow instance and paste it into the ServiceNow value field in the configuration form. |
| close_code | Custom value* | In the **Resolution Information** tab of your ServiceNow instance, copy the close code and paste it into the ServiceNow value field into the configuration form. |

*Select custom values from the dropdown menu

>[!NOTE]
>If you can't locate your custom values, contact your ServiceNow administrator.

To add additional required fields to Resolve Incident section, select **Add**.

## Test and enable

After completing the configuration form, select **Test** at the bottom of the page. Testing is required to submit your configuration to be saved.

Once your test passes successfully, select **Submit** to save your changes. Once you're ready to enable ServiceNow for your organization, switch the **Do you want to enable ServiceNow?** toggle to **On**.

## ServiceNow field definitions

- **short_description**: The short description field in ServiceNow is a brief, 160-character alphanumeric value that provides a summary of the incident. Short description is equivalent to incident description in the Teams Rooms Pro Management portal.

- **description**: The description field in ServiceNow is the first value in the conversation history of a ServiceNow incident. Description is equivalent to First message in the Teams Rooms Pro Management portal.

- **assignment_group**: The assignment group field in ServiceNow is used to route tickets to specific queues. Assignment groups are equivalent to Room groups in the Teams Rooms Pro Management portal. By default, there must be one assignment group defined, and more can be added. You decide how many groups there are and how to route your incidents. 

- **severity**: The severity field in ServiceNow is used to organize incidents by priority. The values that designate priority are customizable. Severity is equivalent to the Ring field in the Teams Rooms Pro Management portal. To customize rings in the Teams Rooms Pro Management portal, go to **Updates** in the left navigation menu. Then go to the **Rings** tab and select **Add ring**.

- **comments**: Comments is an optional field in ServiceNow that is used to include custom required fields from your ServiceNow instance in your Teams Rooms Pro Management portal configuration. The equivalent of comments is a custom value in the Teams Rooms Pro Management portal.

- **state (resolved)**: The state (resolved) field in ServiceNow is used to designate how an incident was resolved and is required to close an incident. The state (resolved) value is customizable. The equivalent of state (resolved) is a custom value in the Teams Rooms Pro Management portal.

- **close_code**: A close code must be assigned to an incident once it's completely resolved. This value is customizable in ServiceNow. The equivalent of close code is a custom value in the Teams Rooms Pro Management portal.

  
