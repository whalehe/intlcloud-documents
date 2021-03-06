## Overview

You can use the lifecycle management feature when you need to change the storage class or delete specified objects regularly to reduce costs. COS will automatically change the storage class or delete specified objects within the specified time frame according to the rules you set. For more information, see [Lifecycle Overview](https://intl.cloud.tencent.com/document/product/436/17028).

>
> A lifecycle can be set to as long as 3,650 days.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List** to enter the bucket list page.
3. Locate the bucket for which you want to enable the lifecycle feature. Click the bucket name to enter its details page.
   ![](https://main.qcloudimg.com/raw/675c47831752107616076859e57e54ad.png)
4. Click **Advanced Configuration** on the left, scroll down to **Lifecycle**, and then click **Add a Rule**.
   ![](https://main.qcloudimg.com/raw/3610ab8aaa27d8541d46cca70546388d.png)
5. Add lifecycle rules as needed. The configuration items are described as follows:
	- **Rule ID**: enter a name for the lifecycle rule.
	- **Applied to**: this lifecycle rule can be applied to the entire bucket or just objects with a specific prefix, such as `example`. If you select **Prefix name**, you need to enter a prefix.
	- **Prefix**: For information on object keys (or prefixes), see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) in Object Overview. For lifecycle configuration rules, see [Rule Description](https://intl.cloud.tencent.com/document/product/436/17029).
	- **Managing the current version**: you can transition or delete the current version of an object using this option. It allows you to transition objects in your bucket from COS STANDARD to COS STANDARD_IA or ARCHIVE, or delete objects upon expiration.
		COS storage classes are **STANDARD**, **STANDARD_IA**, and **ARCHIVE** in order from hot to cold storage. You can transition objects only from a hot storage class to a colder one, not vice versa. Time is measured for a file starting from the moment it is modified (i.e., re-uploaded) in COS.
	- **Managing historical versions**: you can transition or delete previous versions of an object using this option. If it is not enabled, only the latest version of an object is processed by default.
	- **Removing delete markers with no noncurrent versions**: if an object has a delete marker as its latest version, with all of its noncurrent versions deleted, the delete marker will also be deleted once you enable this option. It cannot be enabled with the option to delete upon expiration under **Managing the current version** at the same time.
	- **Deleting incomplete multipart uploads**: allows you to delete expired incomplete multipart uploads that have failed due to any reason.
		![](https://main.qcloudimg.com/raw/5e8c5d09b78537b77c25c7594aa6ec11.png)
6. After the lifecycle rule is configured, click **OK**, and it will be listed instantly.
   ![](https://main.qcloudimg.com/raw/ad7ef4119bfeae82ee7bc4635e7bab38.png)
7. When you want to disable a lifecycle rule, click **Edit** to change the rule state to **Off**, or simply delete the rule.
   ![](https://main.qcloudimg.com/raw/c45c3fc56a6d358b4f8d7f4228521e9b.png)
