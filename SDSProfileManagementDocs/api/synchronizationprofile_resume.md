# Resume sync on a synchronization profile

Resume sync of a specific [synchronization profile](../resources/educationsynchronizationprofile.md) in the tenant.

## Permissions
The following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](../../../concepts/permissions_reference.md).

| Permission type | Permissions |
|:-----------|:----------|
| Delegated (work or school account) | EduAdministration.ReadWrite |
|Delegated (personal Microsoft account|Not supported.|
|Application|Not supported.|

## HTTP request
<!-- { "blockType": "ignored" } -->
```http
POST /synchronizationProfiles/{id}/resume
```

## Request headers
| Name       | Type | Description|
|:-----------|:------|:----------|
| Authorization  | string  | Bearer {token}. Required.  |

## Request body
Do not supply a request body for this method.
## Response
If successful, this method returns a `200 OK` response code.

## Example
##### Request
Here is an example of the request.
<!-- {
  "blockType": "request",
  "name": "post_synchronizationProfile_resume"
}-->
```http
POST https://graph.microsoft.com/beta/education/synchronizationProfiles/{id}/resume
```

##### Response

There is no response body.