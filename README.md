How to run Android Tasks Sample
===============================
Overview
--------
How to build and execute android-tasks-sample using ant

Build and run
-------------
1. Clone sample code

    ```bash
hg clone https://code.google.com/p/google-api-java-client.samples/
    ```
2. Download tasks api client library
  1. Download [google-api-services-tasks-v1-rev41-java-1.19.1.zip](https://developers.google.com/resources/api-libraries/download/tasks/v1/java)
  2. copy lib to sample code project

    ```bash
cp tasks/google-api-services-tasks-v1-rev41-1.19.1.jar tasks/libs/* google-api-java-client.samples/tasks-android-api/libs
    ```
  3. remove library which causes build error (why?)

    ```bash
rm libs/transaction-api-1.1.jar
    ```
3. Copy source of google-api-service_lib

    ```bash
mkdir google-api-java-client.samples/tasks-android-api/libsrc
cp -r ${ANDROID_HOME}/extras/google/google_play_services/libproject/google-play-services_lib 
    ```
4. Update android project

    ```bash
cd google-api-java-client.samples/tasks-android-api/
android update project -p . -t android-10 -s -l libsrc/google-play-services_lib/
cd libsrc/google-play-services_lib/
android update project -p . -t android-10
cd ../..
    ```
5. Add following lines to AndroidManifest.xml in application element.

    ```xml
<meta-data android:name="com.google.android.gms.version" 
           android:value="@integer/google_play_services_version" />
    ````
6. Build debug version

    ```bash
ant debug
    ```
7. Install to device

    ```bash
ant installd
    ```
8. Add api key to Google Developers Console
* Kind: Android App
* Package: com.google.api.services.samples.tasks.android
* Fingerprint of certificate: is printed by following command

    ```bash
keytool -v -list -alias androiddebugkey -keystore ~/.android/debug.keystore -storepass android -keypass android
    ```
Its finterprint is output like "SHA1: xxxx"
9. Run on device

Memo
----
* Source code of google-play-servces_lib is required to create R.java
* Build instruction using gradle 1.6+: [Instructions for the Tasks V1 Android Sample](http://samples.google-api-java-client.googlecode.com/hg/tasks-android-sample/instructions.html)
    * Use gradle 1.6(or 1.8?), not 2.x
    * Use target 8 api or modify buildToolsVersion and compileSdkVersion
    * To compile on the command line, in tasks-android-api directroy run the following command then apk is created in build/apk directory

```bash
gradle assemble
```
