# Firebase

All about Firebase and things it can do for us 🙏

## Log Soft Errors

For logging non fatal errors, we can use utility `logError`.

Which accepts: `errorType` (number) and `additionalParams`.

## Debug push notifications

> To get device token, console.log this variable: `firebase.messaging().getToken()`

We can simulate push notification through this endpoint: `https://fcm.googleapis.com/fcm/send` and setting
payload (iOS):

```json
{
  "to": "{{DEVICE_TOKEN}}",
  "notification": {
    "title": "Amazing Brother 🚀",
    "body": "This guys is our rockstar, follow him!",
    "data": {
      "taggable_type": "TrendingInsightProvider",
      "taggable_id": "123",
      "message_group_id": null,
      "insight_id": null,
      "insight_tagline": null
    }
  }
}
```

!> Every time app got uninstalled/User log out the token changes

### In case something doesn't work

* Check Push Notifications under Capabilities in Xcode to see if any errors
  * Sometimes error is shown, for variables, but thats fine
* Check GoogleService-Info.plist - should match the file from firebase
* Verify your app in settings is allowed to send notifications
* Check if you have correct firebase token of device
* The queue at backend is cleared (sometimes notification will get delayed)
  * This will not affect simulated firebase push notifications
