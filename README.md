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
        maven { url "https://newtronlabs.jfrog.io/artifactory/libs-release-local"
            metadataSources {
                artifact()
            }
        }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.5.2'
        classpath 'com.newtronlabs.android:plugin:4.0.5'
    }
}

allprojects {
    repositories {
        jcenter()
        maven { url "https://newtronlabs.jfrog.io/artifactory/libs-release-local"
            metadataSources {
                artifact()
            }
        }
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

https://gist.github.com/NewtronLabs/216f45db2339e0bc638e7c14a6af9cc8
	
## Contact

solutions@newtronlabs.com
