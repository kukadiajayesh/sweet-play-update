[![](https://jitpack.io/v/therajanmaurya/sweet-play-update.svg)](https://jitpack.io/#therajanmaurya/sweet-play-update)

Usage
-----

In order to use the library

**1. Gradle dependency** 

  -  Add the following to your project level `build.gradle`:
 
```gradle
allprojects {
	repositories {
		 maven { url 'https://jitpack.io' }
	}
}
```
  -  Add this to your app `build.gradle`:
 
```gradle
dependencies {
	implementation 'com.github.therajanmaurya:sweet-play-update:1.4.7'
}
```

**2. Usage** 

For Sweet Play Update using Bottom sheet 

```kotlin
SweetPlayAppUpdaterBottomSheet.newInstant(
            "App Update Available",
            "We have fixed some issues and added some cool feature in this update",
            R.drawable.ic_android_black_24dp
        ).apply { isCancelable = false }
            .show(supportFragmentManager, "Check Update")
```

For Sweet Play Update on somewhere dashboard

```xml
<androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <include layout="@layout/layout_sweet_update" />

        <---- Add your layout here --->
 
    </androidx.constraintlayout.widget.ConstraintLayout>
```

```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var sweetAppUpdater: SweetPlayAppUpdater

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val binding =
            DataBindingUtil.setContentView<ActivityMainBinding>(this, R.layout.activity_main)
                .apply {
                    lifecycleOwner = this@MainActivity
                    mainActivity = this@MainActivity
                }
        sweetAppUpdater = SweetPlayAppUpdater(this, binding.root).apply {
            initAppUpdaterAndCheckForUpdate()
        }
    }

    override fun onResume() {
        super.onResume()
        // Check all update is already downloaded or not if then show install update ui only
        sweetAppUpdater.ifUpdateDownloadedThenInstall()
    }

    // If user ignore the update then re-check update as user may want to install the update later
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        if (requestCode == REQUEST_CODE_FLEXIBLE_UPDATE
            && resultCode != Activity.RESULT_OK
        ) {
            sweetAppUpdater.checkUpdateAvailable()
        }
    }

    override fun onDestroy() {
        super.onDestroy()
        sweetAppUpdater.unregisterListener()
    }
}
```

For proper example, please checkout [this](https://github.com/therajanmaurya/sweet-play-update/blob/master/app/src/main/java/com/github/sweet/play/update/demo/MainActivity.kt)

### Google Play Store
<a href='https://play.google.com/store/apps/details?id=com.github.sweet.play.update.demo'><img alt='Get it on Google Play'
src='https://play.google.com/intl/en_us/badges/images/generic/en_badge_web_generic.png' width='180'/></a>

 A Simple android library to handle google play udpate.

## Sweet Play Designs
<table>
  <td><img src="https://raw.githubusercontent.com/therajanmaurya/Sweet-Play-Update/master/art/home.png"></td>
  <td><img src="https://raw.githubusercontent.com/therajanmaurya/Sweet-Play-Update/master/art/dashboard.png"></td>
</table>

# Design Inspiration

Self developing projects

# Developers

* [Rajan Maurya](https://github.com/therajanmaurya)

# License

```
Copyright 2020 Rajan Maurya

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

```



