Windows Azure Notification Hubs with Tags plugin for Apache Cordova
==================================

Exposes Windows Azure [Notification Hubs](http://www.windowsazure.com/en-us/services/notification-hubs/) functionality as Apache Cordova Plugin. Support of Windows8, Windows Phone8, iOS and Android.

*This sample will register for the hubs and allow messages to be sent using tags on Windows and Android BUT only the Windows version shows toasts. *

### A better approach ...
I suggest you check out a more complete cross platform plugin at, including Windows, iOS and Android support for push, hubs, tags and toasts at :

 	https://github.com/ParamountVentures/ventures-paramount-phonegap-plugin-notificationhubs*

There is a full demo using this at:

	https://github.com/ParamountVentures/AzureNotificationHubsCrossPlatformDemo


### Sample usage ###

    var connectionString = "Endpoint=sb://[service bus name space].servicebus.windows.net/;SharedAccessKeyName=DefaultFullSharedAccessSignature;SharedAccessKey=[notification hub full key]",
        notificationHubPath = "[notification hub name]";
    var senderId = 123456789; // your android sender id

    var hub = new WindowsAzure.Messaging.NotificationHub(notificationHubPath, connectionString, senderId);

    hub.registerApplicationAsync().then(function (result) {
        console.log("Registration successful: " + result.registrationId);
    });

    hub.onPushNotificationReceived = function (msg) {
        console.log("Push Notification received: " + msg);
    };;

### Platform Quirks ###
**iOS**

On iOS the following code must be manually added to AppDelegate.m in order to have plugin to functional correctly.
~~~
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken
{
    [[NSNotificationCenter defaultCenter] postNotificationName:@"UIApplicationDidRegisterForRemoteNotifications" object:deviceToken];
}

- (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error
{
    [[NSNotificationCenter defaultCenter] postNotificationName:@"UIApplicationDidFailToRegisterForRemoteNotifications" object:error];
}

- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo
{
    [[NSNotificationCenter defaultCenter] postNotificationName:@"UIApplicationDidReceiveRemoteNotification" object:userInfo];
}

- (void)application:(UIApplication *)application didRegisterUserNotificationSettings:(UIUserNotificationSettings *)notificationSettings
{
    [[NSNotificationCenter defaultCenter] postNotificationName:@"UIApplicationDidRegisterUserNotificationSettings" object:notificationSettings];
}
~~~~
### Copyrights ###
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
