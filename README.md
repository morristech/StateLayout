# StateLayout
[![](https://jitpack.io/v/erkutaras/StateLayout.svg)](https://jitpack.io/#erkutaras/StateLayout)
[![](https://img.shields.io/badge/build%20for-android-green.svg)](https://www.android.com)
[![](https://img.shields.io/badge/made%20with-kotlin-blue.svg)](https://kotlinlang.org)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

<img src="https://raw.githubusercontent.com/erkutaras/StateLayout/develop/gifs/statelayout.gif" width="250">

StateLayout is a simple-use Android layout library which handles Loading, Content and Error/Info states for the activity/fragment/view. 

This library is developed to show main states of the related screens/views. These main states are: **LOADING**, **DISPLAY CONTENT**, **LOADING WITH CONTENT** and **ERROR/INFO**. When developing any Android project, the states aren't clear for many of the developers except CONTENT. To solve state problem, this layout-library can be implemented easily. 

With using StateLayout in your layout resources as a root view, you can easily change states of the views with calling functions of StateLayout like loading(), content(), info(), etc.

The structure of StateLayout bases on view visibility changing. The layout has three container(loading, info, loading with content) and just one direct child can be placed in as content. This one direct child architecture(like [ScrollView][3]) is selected for preventing state confusion.

Loading layout(layout_state_loading.xml) is a simple layout that has just one ProgressBar with accent color at the center of the screen. Loading-with-Content layout(layout_state_loading_with_content.xml) has also one ProgressBar, but this one is horizantal and placed on top of the screen. Info layout(layout_state_info.xml) can be used both for info and error states that has image, title, message and a button.

## Gradle

**Step 1.** Add the JitPack repository to your root build.gradle at the end of repositories:
```
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```

**Step 2.** Add the library dependency to your project build.gradle:
```
dependencies {
    implementation 'com.github.erkutaras:StateLayout:1.0.4'
}
```

## Usage

Simple flow for your application: First of all, add StateLayout to where you want to change states and add one direct child within that layout. After that, when your releated screen is opened, call stateLayout.loading() and request the API. After the response, change the state accocrding to the response. If there is no error, call stateLayout.content(), otherwise call info state's functions. If you want to show loading and request to API, when the content is visible, call stateLayout.loadingWithContent() and request. When the api call ended, you can change the state. 

- If you want to change or update design of the layouts(layout_state_loading.xml, layout_state_loading_with_content.xml, layout_state_info.xml), create layouts with **SAME** name in your project. 

- To use info state functions like stateLayout.infoImage(), please use **same ids** fot the views.

**Sample code:**
```
<com.erkutaras.statelayout.StateLayout
    android:id="@+id/stateLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_marginBottom="8dp"
    android:layout_marginTop="8dp">

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        
        <!-- CONTENT -->
        
    </RelativeLayout>

</com.erkutaras.statelayout.StateLayout>
```   
```
val stateLayout = findViewById<StateLayout>(R.id.stateLayout)
        
// loading 
stateLayout.loading()
        
// content 
stateLayout.content()
        
// loading with content
stateLayout.loadingWithContent()
        
// error/info
stateLayout.infoImage(R.drawable.ic_android_black_64dp)
                .infoTitle("Ooops.... :(")
                .infoMessage("Unexpected error occurred. Please refresh the page!")
                .infoButton("Refresh", onStateLayoutListener)
// error/info 
stateLayout.info()
``` 

## Issues

If you've found an error in this library, please file an [issue][1].

## Contributing

Patches and new features are encouraged, and may be submitted by [forking this project][2] and submitting a pull request through GitHub. 

[1]: https://github.com/erkutaras/StateLayout/issues
[2]: https://github.com/erkutaras/StateLayout/fork
[3]: https://developer.android.com/reference/android/widget/ScrollView


# License

    Copyright 2018 erkutaras

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
