GME currently provides voice chat and voice messaging and speech-to-text features at the following prices.


## Voice Chat Service
General quality is billed by voice DAU and HD quality is billed by voice duration.

- General quality is recommended for battle and leisure games.
- HD quality is recommended for voice live streaming and online karaoke.
- If you need to be billed by PCU, please contact your Tencent Cloud rep.

### Notes for free tier
Voice chat has two billing modes with the following free tier:
- Billed by voice DAU: free of charge if the daily DAU is below 100.
- Billed by voice duration: free of charge if the daily duration is below 300 minutes.

If the free tier above is exceeded, fees will be charged based on the usage.

> If an application has a voice duration of 150 minutes (< 300 minutes) on a day, no fees will be charged. If the voice duration on the day is 1,000 minutes, the billable voice duration will be 1,000 minutes, and the fees will be 0.94 USD (priced at 0.94 USD/1,000 minutes).


### Price list
<table>
   <tr>
      <td rowspan="6">General Quality</td>
      <td rowspan="3">Billed by voice DAU</td>
      <td rowspan="2">Unit price</td>
      <td>In Mainland China (USD/DAU/day)</td>
      <td>Outside Mainland China (USD/DAU/day)</td>
   </tr>
   <tr>
      <td>0.0015</td>
      <td>0.0072</td>
   </tr>
   <tr>
      <td >Free tier</td>
      <td colspan="4">DAU ≤ 100</td>
   </tr>
   <tr>
      <td rowspan="3">Billed by voice PCU</td>
      <td rowspan="2">Unit price</td>
      <td colspan="4">Service region - globally uniform price (USD/PCU/day)</td>
   </tr>
   <tr>
      <td colspan="4">0.14</td>
   </tr>
   <tr>
      <td rowspan="1">Free tier</td>
      <td colspan="4">Please consult your Tencent Cloud rep</td>
   </tr>
</table>



<table>
   <tr>
      <td rowspan="6">HD quality</td>
      <td rowspan="3">Billed by voice duration</td>
      <td rowspan="2">Unit price</td>
      <td colspan="4">Unit price (USD/1,000 minutes)</td>
   </tr>
   <td colspan="2">0.94</td>
   <tr>
      <td>Free tier</td>
      <td >Duration ≤ 300 minutes</td>
   </tr>
   <tr>
      <td rowspan="3">Billed by voice PCU</td>
      <td rowspan="2">Unit price</td>
      <td colspan="2">Service region - globally uniform price (USD/PCU/day)</td>
   </tr>
   <tr>
      <td colspan="2">0.56</td>
   </tr>
    <tr>
      <td rowspan="">Free tier</td>
      <td colspan="2">Please consult your Tencent Cloud rep</td>
   </tr>
</table>



>
>- A user who enters the room in the application is counted as a voice DAU, and the total number of voice DAUs is calculated based on the deduplicated `openID` (openID is a unique identifier of a user in an application, and one user corresponds to one `openID`).
>- Voice duration is calculated based on the time when a user enters and exits the room. If user A enters a voice room at 12:00, user B enters the room at 12:30, and both of them exit the room at 12:40, the duration of voice use will be 50 minutes in total (40 minutes for user A and 10 minutes for user B).

## Voice Messaging and Speech-to-Text Service
The voice messaging and speech-to-text service is billed by voice message DAU.

### Price list

<table>
   <tr>
      <td>Billing Mode</td>
      <td>Supported Languages</td>
      <td>Unit Price (USD/DAU/day)</td>
   </tr>
   <tr>
      <td  rowspan="2">Billed by voice message DAU</td>
      <td >Simplified Chinese and English only</td>
      <td>0.0019 </td>
   </tr>
   <tr>
      <td >All languages</td>
      <td>0.078 </td>
   </tr>
   </tr>
</table>



>A user who receives or sends a voice message in the application is counted as a voice message DAU, and the total number of voice message DAUs is calculated based on the deduplicated `openID` (`openID` is a unique identifier of a user in an application, and one user corresponds to one `openID`).

## Service Suspension/Release Policy
Your GME service will be suspended 24 hours after your account falls into arrears. Your GME resources will be terminated and repossessed 168 hours (7 days) after the service is suspended. For service continuity, please make sure that your account balance is always sufficient. 


## Alert for Arrears
Alert notifications for arrears will be sent through email, SMS, and Message Center to the Tencent Cloud account creator and all collaborators on the day of and after expiration of the daily pay-as-you-go GME resources.


