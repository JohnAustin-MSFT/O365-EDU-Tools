# List assignments

Retrieve a list of assignment objects. A teacher is allowed to see all assignment objects for the class. Students can only see assignments that are assigned to them.

Due to a bug, the graph will return educationItemBody for the instructions property.  This is an exact duplicate of the itemBody that 
is already found on the graph.   When the code moves to prodution, this will be updated.  For clients who simply use the json being
sent back and forth to the graph, there should be no work necessary to handle this change.


## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](../../../concepts/permissions_reference.md).

|Permission type      | Permissions (from least to most privileged)              |
|:--------------------|:---------------------------------------------------------|
|Delegated (work or school account) | EduAssignments.ReadBasic, EduAssignments.ReadWriteBasic, EduAssignments.Read, EduAssignments.ReadWrite   |
|Delegated (personal Microsoft account) |  Not supported.  |
|Application | Not supported. | 

## HTTP request
<!-- { "blockType": "ignored" } -->
```http
GET /education/classes/<id>/assignments
```
## Optional query parameters
This method supports the [OData Query Parameters](http://graph.microsoft.io/docs/overview/query_parameters) to help customize the response.

## Request headers
| Header       | Value |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |

## Request body
Do not supply a request body for this method.
## Response
If successful, this method returns a `200 OK` response code and collection of [educationAssignment](../resources/educationassignment.md) objects in the response body.
## Example
##### Request
Here is an example of the request.
<!-- {
  "blockType": "request",
  "name": "get_assignments"
}-->
```http
GET https://graph.microsoft.com/beta/education/classes/<id>/assignments
```
##### Response
Here is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.educationAssignment",
  "isCollection": true
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json
Content-length: 344

{
  "value": [
    {
      "id": "String (identifier)",
      "allowLateSubmissions": true,
      "allowStudentsToAddResourcesToSubmission": true,
      "assignDateTime": "String (timestamp)",
      "assignTo": {"@odata.type": "microsoft.graph.educationAssignmentRecipient"},
      "assignedDateTime": "String (timestamp)",
      "classId": "String",
      "createdBy": {"@odata.type": "microsoft.graph.identitySet"},
      "createdDateTime": "String (timestamp)",
      "displayName": "String",
      "dueDateTime": "String (timestamp)",
      "grading": {"@odata.type": "microsoft.graph.educationAssignmentGradeType"},
      "instructions": {"@odata.type": "microsoft.graph.itemBody"},
      "lastModifiedBy": {"@odata.type": "microsoft.graph.identitySet"},
      "lastModifiedDateTime": "String (timestamp)",
      "resourcesFolderUrl": "String",
      "status": "string"
    }
  ]
}
```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "List assignments",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->