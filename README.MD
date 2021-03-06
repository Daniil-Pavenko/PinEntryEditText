[![Build Status](https://travis-ci.org/Daniil-Pavenko/PinEntryEditText.svg?branch=master)](https://travis-ci.org/Daniil-Pavenko/PinEntryEditText)

[![](https://jitpack.io/v/Daniil-Pavenko/PinEntryEditText.svg)](https://jitpack.io/#Daniil-Pavenko/PinEntryEditText)

### Fixes
- Fix change color of text programmatically.

# PinEntryEditText for Android

This repository contains `PinEntryEditText` which extends the behaviour
of `EditText` and implement features that are otherwise not available.

![PinEntryEditText](http://i.giphy.com/3o7qDVApSTFl8DCU4E.gif)

## Features

### PinEntryEditText

- Number of pin characters is configurable. You can use the `maxLength` property to define however long you want your pin to be.
- PinEntryEditText which supports text animating in.
- Lets you specify any unicode character to be used as a mask for input.
- Specify drawable as the foreground/background.

## Usage

Below is a fast guide to getting started. However, if you need to read about these widgets in
details. Read more about
[PinEntryEditText](https://medium.com/@ali.muzaffar/building-a-pinentryedittext-in-android-5f2eddcae5d3#.tka93qm3d).

NOTE: Make sure `jcenter()` is one of the repositories mentioned in your build.gradle.
This used to be the default repository for Android but since then has changed the `google()`
This needs to be set in your top level build.gradle: `<project root>/build.gradle`

```
buildscript {
    repositories {
        jcenter()
        ...
    }
    ...
}
```

## STEP-1

### Gradle


**Jetpack** support in version 2.0 [![](https://jitpack.io/v/Daniil-Pavenko/PinEntryEditText.svg)](https://jitpack.io/#Daniil-Pavenko/PinEntryEditText)

    dependencies {
        implementation ('com.alimuzaffar.lib:pinentryedittext:2.0.8') {
            // Exclude is only needed if you already have
            // androidx.appcompat as a dependency in your app.
            exclude group: 'androidx.appcompat', module: 'appcompat'
        }
    }

If you don't use Jetpack, use version 1.3.X [ ![Download](https://api.bintray.com/packages/alphamu/customwidgets/PinEntryEditText/images/download.svg?version=1.3.10) ](https://bintray.com/alphamu/customwidgets/PinEntryEditText/1.3.10/link)

    dependencies {
        implementation ('com.alimuzaffar.lib:pinentryedittext:1.3.10') {
            // Exclude is only needed if you already have
            // any of the following as a dependency in your project.
            exclude group: 'com.android.support', module: 'support-v4'
            exclude group: 'com.android.support', module: 'appcompat-v7'
            exclude group: 'com.android.support', module: 'support-v13'
        }
    }

**Note:** You don't need to exclude all the support groups. However, it's a good idea to do this
as your code is likely to use a different version from the library.

## STEP-2

### Setup PinEntryEditText in your layout

```xml
<com.alimuzaffar.lib.pin.PinEntryEditText
    android:id="@+id/txt_pin_entry"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:cursorVisible="false" 
    android:digits="1234567890"
    android:inputType="number"
    android:maxLength="4" 
    android:textIsSelectable="false" 
    android:textSize="20sp"
    app:pinBackgroundDrawable="@drawable/bg_pin" 
    app:pinAnimationType="popIn|fromBottom|none" 
	app:pinCharacterMask="*" 
	app:pinSingleCharHint="#"
	app:pinTextBottomPadding="@dimen/space" 
	app:pinLineStroke="2dp" 
	app:pinLineStrokeSelected="4dp" 
	app:pinBackgroundIsSquare="true|false" 
    app:pinLineColors="@color/pin_line_colors" 
    android:layoutDirection="ltr|rtl"
    />
```

### Listen for pin entry

```java
final PinEntryEditText pinEntry = (PinEntryEditText) findViewById(R.id.txt_pin_entry);
if (pinEntry != null) {
    pinEntry.setOnPinEnteredListener(new PinEntryEditText.OnPinEnteredListener() {
        @Override
        public void onPinEntered(CharSequence str) {
            if (str.toString().equals("1234")) {
                Toast.makeText(AnimatedEditTextWidgetsActivity.this, "SUCCESS", Toast.LENGTH_SHORT).show();
            } else {
                Toast.makeText(AnimatedEditTextWidgetsActivity.this, "FAIL", Toast.LENGTH_SHORT).show();
                pinEntry.setText(null);
            }
        }
    });
}
```

## Use your own Drawable as a pin character background

You can use your own drawable for the pin entry background by specifying the `app:pinBackgroundDrawable`
attribute in the xml. If you want to specify the empty and filled states using your background drawable
you can set the `textColor` to transparent and setup your drawable as follows:

```xml
<!--
    Please look at the sample app's bg_pin.xml
    or bg_pin_round.xml for all available options
-->
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- Space contains text -->
    <item android:state_focused="true" android:state_checked="true">
        <shape android:shape="rectangle">
            <solid android:color="@android:color/holo_green_light"/>
        </shape>
    </item>
    <!--Space is the next space for character input -->
    <item android:state_focused="true" android:state_selected="true">
        <shape android:shape="rectangle">
            <solid android:color="@android:color/holo_blue_bright"/>
        </shape>
    </item>
    <!-- PinEntryEditText is focused -->
    <item android:state_focused="true">
        <shape android:shape="rectangle">
            <solid android:color="@android:color/white"/>
        </shape>
    </item>
    <!-- PinEntryEditText is not focused -->
    <item>
        <shape android:shape="rectangle">
            <solid android:color="@android:color/darker_gray"/>
        </shape>
    </item>
</selector>
```

**Note** that in this setup, the size of the drawable will be determined by the `textSize` and and the `pinTextBottomPadding`
which is the space between the character and the line below (or the bottom of the `pinBackgroundDrawable`).
For good measure, set `pinAnimationType` to none as well.

## Effects :

1. PopIn (default)
2. Bottom Up

License
=======

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.