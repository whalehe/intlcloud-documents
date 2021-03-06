On the API Debugging page, you can verify the correctness of the API right after it is configured, simulate an API call and view the specific call log and the request response. If the API does not work the way you designed, you can modify the configurations based on the log and response as needed.

1. In the API Management tab of the Service page, select the API to be debugged and click **API Debugging** in the upper right corner to enter the Debugging page.
![Debugging](https://main.qcloudimg.com/raw/cf834572a641542ec6688c68360b0d6f.png)

2. On the debugging page, you can find the frontend configuration information of the API to be debugged, including the path, the request method and request parameters. For the request parameters, if you specify default values for the parameters, these values will be filled into the input box by default. If you specify that the parameters are required, the system will check whether the required parameters have been entered before testing. If your request method is POST, PUT or DELETE, you must enter the Body parameter.
![Debugging](https://main.qcloudimg.com/raw/8b36a0a5a93f1d15dbeb9e720c8161c9.png)
> If the parameters are optional and the user does not enter any values for the parameters, API Gateway will send a null to the backend by default.

3. Click **Send Request**, and you can find two outputs:
   1) Request log: The log outputs the request records in detail, including the request path constructed based on the frontend parameters and the request method, the Headers parameters, the configurations actually called by the backend, the process of initiating the request to the backend, and the response code and data returned from the backend. 
   2) Response: The response code and data actually returned to the frontend after the API call.
![Debugging Result](https://main.qcloudimg.com/raw/5abda22982681132c9d963bed71dd38e.png)
