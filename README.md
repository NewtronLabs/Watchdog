# Watchdog

Newtron Watchdog allows the critical applications you develop for Android to keep running even after an application crash. 

<p align="center">
  <img src="https://github.com/NewtronLabs/Watchdog/blob/master/Diagram.png" width="60%" height="60%" >
</p>

---

## How to Use 

### Step 1

Install 'Newtron Watchdog' from the Google Play store (https://play.google.com/store/apps/details?id=com.newtronlabs.watchdogapp) on your device.


### Step 2

Include the below dependencies in your `build.gradle` project.

```gradle
buildscript {
    repositories {
        jcenter()
        maven { url "http://code.newtronlabs.com:8081/artifactory/libs-release-local" }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.3'
        classpath 'com.newtronlabs.android:plugin:2.0.1'
    }
}

allprojects {
    repositories {
        jcenter()
        maven { url "http://code.newtronlabs.com:8081/artifactory/libs-release-local" }
    }
}

subprojects {
    apply plugin: 'com.newtronlabs.android'
}
```

In the `build.gradle` for your app.

```gradle
dependencies {
    compileOnly 'com.newtronlabs.watchdog:watchdog:2.0.0'
}
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

Newtron Watchdog binaries and source code can only be used in accordance with Freeware license. That is, freeware may be used without payment, but may not be modified. The developer of Newtron Watchdog retains all rights to change, alter, adapt, and/or distribute the software. Newtron Watchdog is not liable for any damages and/or losses incurred during the use of Newtron Watchdog.

You may not decompile, reverse engineer, pull apart, or otherwise attempt to dissect the source code, algorithm, technique or other information from the binary code of Newtron Watchdog unless it is authorized by existing applicable law and only to the extent authorized by such law. In the event that such a law applies, user may only attempt the foregoing if: (1) user has contacted Newtron Labs to request such information and Newtron Labs has failed to respond in a reasonable time, or (2) reverse engineering is strictly necessary to obtain such information and Newtron Labs has failed to reply. Any information obtained by user from Newtron Labs may be used only in accordance to the terms agreed upon by Newtron Labs and in adherence to Newtron Labs confidentiality policy. Such information supplied by Newtron Labs and received by user shall not be disclosed to a third party or used to create a software substantially similar to the technique or expression of the Newtron Labs Newtron Watchdog software.

You are solely responsible for determining the appropriateness of using Newtron Watchdog and assume any risks associated with Your use of Newtron Watchdog. In no event and under no legal theory, whether in tort (including negligence), contract, or otherwise, unless required by applicable law (such as deliberate and grossly negligent acts) or agreed to in writing, shall Newtron Labs be liable to You for damages, including any direct, indirect, special, incidental, or consequential damages of any character arising as a result of this License or out of the use or inability to use the Newtron Watchdog (including but not limited to damages for loss of goodwill, work stoppage, computer failure or malfunction, or any and all other commercial damages or losses), even if Newtron Labs has been advised of the possibility of such damages. 
	
## Contact

solutions@newtronlabs.com
