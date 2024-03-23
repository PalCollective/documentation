# Mobile Location Estimation
The main objective of location verification is to act as a first order of defense to verify the authenticity of users in Gaza. This is done to ensure malicious users aren't using the platform for nefarious purposes.
There are 3 ways to estimate the location of a device. They are listed below in decreasing order of accuracy:
1. Using GPS location.
2. Using cellular network.
3. Using Wi-Fi

#### GPS
Using this method the location coordinates are obtained directly from the GPS receiver from the device, provided the device has one.

##### Preconditions
1. The device must support GPS location.
Android provides an API to check whether the [device supports GPS](https://developer.android.com/reference/android/location/LocationManager#getAllProviders()). The API returns a list of location providers from which we can check if GPS is one of them.

##### Concerns
1. Location can be mocked by enabling developer options in Android using third party applications.
**Solution**- The app can detected whether developer settings are enabled and automatically restrain the user from proceeding with verification. See links to check if Developer Options are enabled:
[Stack overflow example](https://stackoverflow.com/questions/63348116/foolproof-way-to-detect-if-developer-options-are-enabled)
[Official android documentation](https://developer.android.com/reference/android/provider/Settings.Global#getInt(android.content.ContentResolver,%20java.lang.String,%20int))
2. The app can be run from an emulator which can then mock the location provided to the app.
**Solution**- The app may detect the presence of an emulator using various techniques described in this [Medium article](https://ray-chong.medium.com/android-emulator-detection-4d0f994aab5e). Further analysis and more robust solutions may be researched for this.

##### GPS APIs
There are two main APIs that android provides to fetch the device's location:
###### 1. Fused location API ([Official documentation](https://developers.google.com/android/reference/com/google/android/gms/location/FusedLocationProviderClient))
This is a Google Play service API and it derives the location of the device using a combination of GPS, cell networks and device sensors. It has a higher accuracy compared to the location manager API, however it comes with its constraints:
1. This API is supported from Android 5 (API level 21) and above:
This is a significantly older android OS version (9 years old) but there may still be functional devices around with this version installed.
2. The device must have Google Play Store installed with Google play services:
This is a further constrain as certain OEMs like Huawei do not support Google play services and hence might break this API. ([Details](https://www.androidauthority.com/huawei-google-android-ban-988382/#:~:text=Goodbye%20Google%3A%20The%20HUAWEI%20Google%20ban%2C%20explained))

The following relevant details are available from this API (for full list of details see [Location](https://developer.android.com/reference/android/location/Location)):
1. Latitude
2. Longitude
3. Accuracy(Optional)
4. Timestamp
4. Provider(Optional)

###### 2. Location manager API ([Official documentation](https://developer.android.com/reference/android/location/LocationManager#requestLocationUpdates(java.lang.String,%20long,%20float,%20android.app.PendingIntent)))
This is a native android API and was added in Android 1.5 (API level 3) so it supports a much wider range of devices and does not have any dependency on Google play services.

The following relevant details are available from this API (for full list of details see [Location](https://developer.android.com/reference/android/location/Location)):
1. Latitude
2. Longitude
3. Accuracy
4. Timestamp
4. Provider(Optional)

***Note:** This is the recommended approach*

#### Cellular Network
This approach uses the location of nearby cell towers to estimate the location of the mobile device.

##### Pre-conditions
1. The device must support cellular networks
Android provides an API to check whether the [device supports network location](https://developer.android.com/reference/android/location/LocationManager#getAllProviders()). The API returns a list of location providers from which we can check if network is one of them.

##### Network APIs
The same [APIs used for GPS location](#gps-apis) can be reused to obtain cellular network location by changing its provider.

#### Wi-Fi
In this approach the IP address of the device is used to reverse lookup its location using preexisting web services.

##### Concerns
1. The device might be using a VPN service which can change the IP address and location.
**Solution**- The app can check whether a VPN is currently being used. The following [medium document](https://blog.tarkalabs.com/the-ultimate-vpn-detection-guide-for-ios-and-android-313b521186cb) specifies how.

##### Wi-Fi APIs
To obtain the IP address of the following APIs are available:
1. Upto Android 11 -
[WifiManager](https://developer.android.com/reference/android/net/wifi/WifiManager) APIs will return the IP address. See links:
    - [ConnectionInfo](https://developer.android.com/reference/android/net/wifi/WifiManager#getConnectionInfo()).
    - [IP address](https://developer.android.com/reference/android/net/wifi/WifiInfo#getIpAddress())
2. Android 12 and above - 
[ConnectivityManager](https://developer.android.com/reference/android/net/ConnectivityManager) APIs can be used to get the IP address. See links:
    - [LinkProperties](https://developer.android.com/reference/android/net/ConnectivityManager#getLinkProperties(android.net.Network))
    - [TransportInfo](https://developer.android.com/reference/android/net/NetworkCapabilities#getTransportInfo())
    - [IP address](https://developer.android.com/reference/android/net/wifi/WifiInfo#getIpAddress())