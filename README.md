# Watchdog

Newtron Watchdog allows the critical applications you develop for Android to keep running even after an application crash. 

<p align="center">
  <img src="https://github.com/NewtronLabs/Watchdog/blob/master/Diagram.png" width="56%" height="56%" >
</p>

---

## How to Use 

### Step 1

Install 'Newtron Watchdog' from the Google Play store (https://play.google.com/store/apps/details?id=com.newtronlabs.watchdogapp) on your device.


### Step 2

Include the below dependencies in your `build.gradle` project.

```gradle
allprojects {
    repositories {
        jcenter()
         maven { url "http://code.newtronlabs.com:8081/artifactory/libs-release-local" }
    }
}
```

In the `build.gradle` for your app.

```gradle
compile 'com.newtronlabs.watchdog:watchdog:1.0.4'
```

### Step 3

At runtime, register your application with Newtron Watchdog

```java
Intent restartIntent = new Intent(this, SampleActivity.class);

IWatchdog client = WatchdogFactory.getInstance()
        .getClientBuilder(restartIntent)
        .setRegistrationListener(this)
        .build();

client.register(this);
```

Upon registration your listener will be notified with a `ResultCode`, use this code to recommend users solutions like for exmaple in the case where Newtron Watchdog is not installed in their device. 

```java
@Override
public void onRegistrationComplete(@WatchdogResult.ResultCode int resultCode)
{
    Log.d("WatchDog", "Registration Result: "+ resultCode);

    if(resultCode == WatchdogResult.WATCHDOG_REGISTRATION_OK)
    {
	 Log.d("WatchDog", "Registration Successful");
    }
    else if(resultCode == WatchdogResult.WATCHDOG_NOT_INSTALLED)
    {
	 Log.d("WatchDog", "Watchdog not installed on device." 
	     + "Download 'Newtron Watchdog' from App Store");
    }
    else if(resultCode == WatchdogResult.WATCHDOG_UNREGISTERED)
    {
 	 Log.d("WatchDog", "Unregistered Successfully");
    }
    else if(resultCode == WatchdogResult.WATCHDOG_VERSION_MISMATCH)
    {
	Log.d("WatchDog", "Version mismatch." 
	    + "Ensure you have the latest version of Watchdog and Libraries");
    }
    else if(resultCode == WatchdogResult.WATCHDOG_FAILED)
    {
	Log.d("WatchDog", "Unrecoverable Failure.");
    }
}
```

## License

Users may not decompile, reverse engineer, pull apart, or otherwise attempt to dissect the source code, algorithm, technique or other information from the binary code of Newtron Watchdog unless it is authorized by existing applicable law and only to the extent authorized by such law. In the event that such a law applies, user may only attempt the foregoing if: (1) user has contacted Newtron Labs to request such information and Newtron Labs has failed to respond in a reasonable time, or (2) reverse engineering is strictly necessary to obtain such information and Newtron Labs has failed to reply. Any information obtained by user from Newtron Labs may be used only in accordance to the terms agreed upon by Newtron Labs and in adherence to Newtron Labs confidentiality policy. Such information supplied by Newtron Labs and received by user shall not be disclosed to a third party or used to create a software substantially similar to the technique or expression of the Newtron Labs Newtron Watchdog software.
	
## Contact

contact@newtronlabs.com
