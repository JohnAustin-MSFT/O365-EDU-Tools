# Create a profile using the school data sync profile APIs

You can use the school data sync profile management APIs to enable automated profile and roster sync management. Setting up a profile for sync using an API connector involves two steps.

|   Operation	                            |  REST call 	|   Description                             	|   	
|------	                                    |---	        |---	                                        |
|[Create Profile](../api/synchronizationprofile_post.md) (Required)|   POST|   Set up a profile for SDS Sync |   	
| [Monitor Provisioning ](../api/synchronizationprofile_get.md) (Required)|GET|   Verify that the profile is provisioned by checking the state property.  |
| [Get Status](../api/synchronizationprofilestatus_get.md) (Optional)         	                    |   GET	        |   Get the status of the ongoing sync.|   	


## Step 1: Create profile

First, create profile that you want to sync. After you create the profile, you can use it for all future syncs.

For information about how to create a profile, see [Create profile](../api/synchronizationprofile_post.md). Make sure that you have the appropriate permissions, as listed in the topic.

Most of the options for CreateProfile with API format are similar to CSV format with one key difference - sync format type which is API instead of CSV.

#### Sync format:

  To use Create Profile support with the API format specify the corresponding Data provider. SDS currently supports PowerSchool Data Provider. In future the support will expand to more data providers.

     Here is the sample code snippet:

         @odata.type":"#microsoft.graph.powerSchoolDataProvider",
         "connectionUrl":"http://contoso.cloudapp.net",
         "clientId":"37e81c3f-73a2-4ecd-a314-xxxxxxxxx",
         "clientSecret":"secret",
         "schoolsIds":[  
            "55"
         ],

Create Profile returns the following:
  - Http/1.1 202 Accepted
  - Http 400 If model validation fails
  - Http 500 otherwise

Once the profile with API provider is created successfully, sync is started automatically.

#### Create Profile with Powerschool API Provider:
Powerschool is one of the custom API provider that's currently supported, to integrate with that specify #microsoft.graph.powerSchoolDataProvider" as the data type. Once profile is created, it starts syncing automatically.

      "dataProvider":{  
           "@odata.type":"#microsoft.graph.powerSchoolDataProvider",
           "connectionUrl":"http://contoso.clouddapp.net",
           "clientId":"37e81c3f-73a2-4ecd-a314-40eab50f68b8",
           "clientSecret":"secret",
           "schoolsIds":[  
              "55"
      }

## Step 2 : Monitor profile provisioning.

After a profile creation is accepted, it is provisioned by the system. The object returned in the response by the Create Profile API has a state of 'provisioning' and an 'id' which will be the unique identifier for the profile. To monitor the provisioning, perform a [GET operation on the profile](../api/synchronizationprofile_get.md) and check the profile state in the response. As soon as the state returned is 'provisioned', the profile is ready to sync.

### Step 2 : Get Sync Status
Once sync is started in the background you can query the sync status using the GetSyncStatus API


|  Method    |  Request URI                                                              |   
|---         |---                                                                        |
| GET        | /{serviceroot}/SynchronizationProfiles/{profileId}/Status


Profile Management provides the  following upload status:

      <EnumType Name="status">
        <Member Name="paused" Value="0" />
        <Member Name="inProgress" Value="1" />
        <Member Name="success" Value="2" />
        <Member Name="error" Value="3" />
        <Member Name="validationError" Value="4" />
        <Member Name="quarantined" Value="5" />

A status of 'validationError' indicates that sync was automatically paused as potential errors were detected. To ignore and continue, [Resume Sync](../api/synchronizationprofile_resume.md) on the profile.
