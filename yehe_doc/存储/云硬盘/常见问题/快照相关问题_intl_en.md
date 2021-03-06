### A cloud disk has adopted a three-copy redundancy mechanism for data security. Why do we still need to use snapshots?
In situations where a logic-level data error occurs, for example, suppose a user deletes data by mistake, or if the data is damaged by a virus or file system exceptions, all three copies of the data stored will be affected and historical data cannot be restored. If you have created a snapshot previously, you can use the snapshot to restore data to the point in time the snapshot was created.
![](https://main.qcloudimg.com/raw/824b34d077d2e58114e08de86edae2b8.png)
Suppose an administrator created snapshot A for a cloud disk at 11:00, and the cloud disk was infected with a virus at 12:00, which caused that data to be unusable. In this case, the three copies of the data would have been updated to status 2, and the data cannot be restored. To restore data to the uninfected status 1, you have to use the snapshot A created at 11:00.

### Why does the used disk capacity displayed in the file system differ from the snapshot size?
A cloud disk snapshot is a block-level clone or backup. In general, the snapshot capacity will be larger than the data capacity displayed in the file system because:
- The underlying data block stores the metadata of the file system.
- Some data are deleted. Deleting data modifies the written-in data block, which will be backed up to snapshots.


### What are the differences between snapshots and images?
If no data disk is mounted to an instance and all data is written on the system disk, the data on the system disk cannot be protected by creating an image. Images cannot be scheduled for continuous backup. Once the system disk data is damaged, you can only recover the data to the state when the image was initially created. Therefore, images are not suitable for data protection. Specific differences are as follows:

<table>
		<tr>
		<th width="10%">Name</th>
		<td width="45%">Snapshots</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">Images</a></td>
		</tr>
		<tr>
		<th>Characteristics</th>
			<td>Backup data of a cloud disk at a certain point in time</td>
	   	<td>CVM software configuration template, which contains information about the operating system and pre-installed programs</td>
		</tr>
		<tr>
		<th>Use Cases</th>
		<td>
			<ul>
				<li>Regularly back up important business data</li>
				<li>Back up data before major operations</li>
				<li>Produce multiple copies of data</li>
			</ul>
		</td>
		<td>
			<ul>
				<li>Back up systems that will remain unchanged in the short term</li>
				<li>Deploy applications in batches</li>
				<li>Migrate the system</li>
			</ul>
		</td>
		</tr>
</table>


### Why can’t I use the snapshot to create an image?
You can create snapshots on both the system disk and the data disk. However, you can only create a custom image from the snapshot of the system disk, and then use the custom image to create instances with the same environment.

### Why can’t I delete the snapshot?
Confirm that the snapshot you want to delete does not associate with any image or the associated image has been deleted. The image is binding to the snapshot by default when a custom snapshot is created. You have to first delete the associate image and then delete the snapshot. To query associated snapshots of an image, go to the [image] (https://console.cloud.tencent.com/cvm/image) page and click the ID/Name of the image.

### How are snapshots created from an image billed?
Images use the CBS snapshot service for data storage. The associated snapshots of a custom image will be billed by the used capacity. To view the total capacity of the snapshot, see [Snapshot Capacity](https://console.cloud.tencent.com/cvm/snapshot/overview).

### How are shared images billed?
Only the account that shares the image with another account will be charged, while the recipient account will not be charged. For more information about the snapshot billing, see [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415).



### What is a scheduled snapshot?
A scheduled snapshot is automatically created for the cloud disk according to the associated scheduled snapshot policy. To use this feature, you must first create a scheduled snapshot policy and associate it with the cloud disk.


### What limits do scheduled snapshots have?
A maximum of 30 scheduled snapshot policies can be created in one region. Each scheduled snapshot policy can be associated with up to 200 cloud disks. In addition, snapshots created according to the scheduled snapshot policies must comply with snapshot quota. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/362/32406).

### How do I create a cloud disk snapshot?
You can create a snapshot using the following methods:
- Custom snapshot: you can manually create a snapshot to quickly save data of the cloud disk at a specified point in time. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- Scheduled snapshot: you can associate the scheduled snapshot policies with the cloud disk to periodically create and delete snapshots. For more information, see [Scheduled Snapshot](https://intl.cloud.tencent.com/document/product/362/35238).

### Is snapshot available in all availability zones?
Yes.

## How are snapshots billed?
Snapshots are billed according to your total snapshot storage capacity in each region. CBS is a **pay-as-you-go** service billed on the hour. For more information about billing, see [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415) and [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

### Do I need to unmount the disk or interrupt all reads and writes before creating snapshots?
No. You can create a real-time snapshot while the disk is connected and in use, without affecting the normal operation of your business. However, the snapshot can only capture the written data but not cached data of the cloud disk. To ensure all application data is captured, we recommend that you suspend all disk I/O operations before creating a snapshot. For a cloud disk that is used as a system disk, we recommend that you shut down the CVM to create a more complete snapshot.

### Will creating a snapshot affect the disk performance?
Creating a snapshot will occupy a small amount of the cloud disk I/O. We recommend creating snapshots when business is slow.

### How long does it take to create a snapshot?
The time it takes to create a snapshot is influenced by factors such as the number of disk writes and the underlying read-write operations. Creating a snapshot will not affect your disk use.

### How do I create a cloud disk using a snapshot?
For more information, see [Creating Cloud Disks using Snapshots](https://intl.cloud.tencent.com/document/product/362/5757).

### How do I roll back snapshots?
For more information, see [Rolling Back Snapshots](https://intl.cloud.tencent.com/document/product/362/5756).

### Do I need to shut down the CVM to roll back a snapshot?
- For a cloud disk that has been mounted to a CVM, you have to shut down the CVM to roll back snapshots.
- For a cloud disk that has not been mounted, you can directly roll back snapshots.

### Can I read a previous snapshot to restore a cloud disk?
Yes. You can use an existing snapshot created at any point in time to restore data, regardless of the snapshot’s point in time.

### Can I delete the source snapshot when it is being replicated?
No. It can only be deleted after the replication is complete.

### Is the new snapshot still associated with the source snapshot’s source disk after the replication is complete?
After the cross-region replication, the new snapshot is no longer associated with the source disk of the source snapshot. The rollback feature is unavailable for replicated snapshot.

### Will associated snapshots be deleted when the CVM is terminated?
No. You need to delete snapshots via the Console or APIs. For more information, see [Deleting Snapshots](https://intl.cloud.tencent.com/document/product/362/5758).

### How do I delete snapshots?
- For cloud disk snapshots, you can delete them directly via the Console or APIs. For more information, see [Deleting Snapshots](https://intl.cloud.tencent.com/document/product/362/5758).
- For snapshots associated with custom images, you must first delete the custom images and then [delete the snapshots](https://intl.cloud.tencent.com/document/product/362/5758).
