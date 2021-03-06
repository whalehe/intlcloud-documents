## API Description

This API (RegisterRepositoryAccountNew) registers a user (with no need to specify the namespace). 

API domain name:
```
ccr.api.qcloud.com
```

## Input Parameters

The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter name | Description | Type | Required |
| -------- | ---- | ------ | ---- |
| password | Password | String | Yes |

## Output Parameters

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| code | Common error code. 0: Successful; other values: Failed. | Int |
| message | Module error message description depending on API | String |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |



## Samples

### Input

```
  https://domain/v2/index.php?Action=RegisterRepositoryAccountNew
  &password="xxxyyyzzz"
  &other common parameters
```

### Output

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success"
}
```
