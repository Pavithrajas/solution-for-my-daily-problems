**Problem:**

While trying to download a file from S3 (AWS Account) using python script (Python Version: 2.7) with boto3 module, got the following error, 
```
ClientError: An error occurred (RequestTimeTooSkewed) when calling the GetObject operation: The difference between the request time and the current time is too large.\n
```

**Cause**

This was because of the time sync mismatch in the client(local - Ubuntu) machine which I was using with the current time itself. 

**Solution**

Ran the time sync in my machine using ntp using the following command, 

`sudo ntpdate ntp.ubuntu.com`
