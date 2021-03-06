### Does COS have a limit on the upload and download bandwidth?

No. The upload and download speed depends on your local bandwidth.


### How can I directly preview a file in my browser without downloading it?

A bucket endpoint in the format of `<BucketName-APPID>.cos.<Region>.myqcloud.com` is an XML endpoint. You can directly preview a file of supported file type in your browser by accessing the object URL in this endpoint format.

A bucket endpoint in the format of `<BucketName-APPID>.<region>.myqcloud.com` is a JSON endpoint. If you access the object URL in this endpoint format in your browser, a download window will pop up, and there are two ways to preview the file in the browser:

1. Upgrade your COS Console to [the latest version](https://console.cloud.tencent.com/cos5) and use the object URL in the XML endpoint format for access (strongly recommended).
2. Bind a custom endpoint, enable static website, and access the file with the custom endpoint. For more information, see [Endpoint Management for JSON](https://intl.cloud.tencent.com/document/product/436/18424) and [Static Website Settings for JSON](https://intl.cloud.tencent.com/document/product/436/14984).

#### Sample:

Take the picture.jpg file in the root directory of the bucket examplebucket-1250000000 in Beijing for example:

- If the object endpoint is in the format of `https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/picture.jpg`, you can directly access it to preview the picture.jpg file in your browser.
- If the object endpoint is in the format of `https://examplebucket-1250000000.cosbj.myqcloud.com/picture.jpg`, there are two ways to directly preview the object in your browser:
  1. Upgrade your COS Console to [the latest version](https://console.cloud.tencent.com/cos5) and use the object link in the XML endpoint format for access (strongly recommended).
  2. Bind a custom endpoint, enable static website, and access the file with the custom endpoint. For more information, see [Endpoint Management for JSON](https://intl.cloud.tencent.com/document/product/436/18424) and [Static Website Settings for JSON](https://intl.cloud.tencent.com/document/product/436/14984).

### How can I directly download a file in my browser without previewing it?

You can set the value of the Content-Disposition parameter in the custom object headers to "attachment" in the [COS console](https://console.cloud.tencent.com/cos5). For more information on how to do so in the console, see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).

You can also let your browser pop up a window for the file to be downloaded by setting the value of the request parameter `response-content-disposition` in the GET Object API to "attachment". For more information, see [GET Object](https://intl.cloud.tencent.com/document/product/436/7753).

>! To use the `response-*` parameter in a request, the request must be signed.

### How to determine if I am accessing COS over the private network?

The access endpoints of COS adopt intelligent DNS resolution. For COS access via Internet (including different ISPs), we will detect and select the optimal linkage for you to access COS. If you have deployed a service in Tencent Cloud to access COS, the access in the same region will be automatically directed to the private network address. The cross-region access is not supported in the private network and the COS endpoint is resolved to the public network address by default.

#### How to determine an access over private network

Tencent Cloud products within the same region access each other over a private network by default, incurring no traffic fees. Therefore, it is recommended to choose the same region when you purchase different Tencent Cloud products to save costs.

The following shows how to determine an access over private network:

For example, when a CVM access COS, to determine whether a private network is used to access COS, use the `nslookup` command on the CVM to resolve the COS endpoint. If a private network IP is returned, the access between CVM and COS is over a private network; otherwise, it is over a public network.

>?Generally, a private IP address takes the form of `10.*.*.*` or `100.*.*.*`, and a VPC IP address takes the form of `169.254.*.*`.

Assume that `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com` is the address of destination bucket, and the `Address: 10.148.214.13` below it indicates the access is over the private network.

```shell
nslookup examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com

Server:         10.138.224.65
Address:        10.138.224.65  #53

Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.13
Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.14
```

For more information on private and public network access and connectivity testing, see [COS Access via Private Network and Public Network](https://intl.cloud.tencent.com/document/product/436/30613).

For the private DNS server addresses of CVM, see [Private Network DNS](https://intl.cloud.tencent.com/document/product/213/5225).

>!There are differences between the private IP address of CPM (common format: `9.*.*.*`) and the IP address of CVM (common format: `10.*.*.*`). If you have any questions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### How to download a folder?

You can log in to the [COSBrowser](https://intl.cloud.tencent.com/document/product/436/11366), select the folder to be downloaded, and click **Download** to download the folder or files in batches. You can also download the folder using the COSCMD tool. For more information, see [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).

### What should I do if the error "403 Forbidden" occurs or the permission is rejected when I perform upload/download and other operations?

Troubleshoot the problems by following the steps below:

1. Check whether your following configuration information is correct:
   BucketName, APPID, Region, SecretId, SecretKey, etc.
2. If the above information is correct, check whether a sub-account is used for operation, and if yes, check whether the sub-account has been authorized by the root account. If it hasn't yet, log in using the root account to authorize the sub-account. For more information on authorization, see [Cases of Permission Settings](https://intl.cloud.tencent.com/document/product/436/12514).
3. If a temporary key is used, check whether the current operation is in the policy set when the temporary key is obtained, and if no, modify the relevant policy settings. For more information, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
4. If the problem persists after all the above steps are completed, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1).


### How can I upload or download multiple files using COS?

COS allows you to upload or download multiple files through various methods such as the console, APIs/SDKs, and tools.

- Using the console: for detailed directions, see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).
- Using APIs/SDKs: COS allows you to operate on multiple files  programmatically by repeatedly calling an API or SDK. For more information, see [APIs for object uploads](https://intl.cloud.tencent.com/document/product/436/10111) 和 [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).
- Using tools: [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976) and [COSBrowser](https://intl.cloud.tencent.com/document/product/436/11366) for batch operations.


### When I upload a new file to the bucket in which another file with the same name exists, will the another file be overwritten or the new file be saved with a different version name?

The versioning feature is now available in COS. If versioning is not enabled for the bucket, when you upload a new file to the bucket where another file with the same name already exists, the latter will be directly overwritten; if versioning is enabled, multiple versions of the object will co-exist.

### What is the lower limit of part size for multipart upload in COS?

1 MB. For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### When uploading large files using multipart upload, can I replace an invalid signature to continue the multipart upload?

Yes.


### What should I do if I upload a file in the console and "Failed to upload. System error." is displayed?
This error may occur due to your unstable local network environment. You are recommended to upload again in a different network environment.


### How to prevent others from downloading my COS files?

To do so, you can set your bucket permission to private read/write. For more information, see [Setting Access Permission] (https://intl.cloud.tencent.com/document/product/436/13315). You can also configure a hotlink protection allowlist to block any access to your default bucket endpoint from domain names not in the list. For more information, see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319).


### What should I do if the error "your policy or acl has reached the limit (Status Code: 400; Error Code: PolicyFull)" occurs when I upload files or create a bucket?

COS allows each root account to have up to 1,000 bucket ACLs. This error occurs if you configure more bucket ACLs than this figure. Therefore, it is recommended to delete your useless bucket ACLs.
>?We do not recommend using ACLs or policies at the object level. When you call APIs or SDKs, if you do not need ACL control over files, it is recommended to leave the ACL-related parameters (such as x-cos-acl and ACL) empty to inherit the bucket permissions.
