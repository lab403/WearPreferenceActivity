[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-WearPreferenceActivity-brightgreen.svg?style=flat)](http://android-arsenal.com/details/1/1643)

# WearPreferenceActivity
A preferences framework for Android Wear apps. Equivalent to Android's `PreferenceActivity`, but for Android Wear.

![Preference List](/screenshots/preference_list.png) ![Preference List](/screenshots/language_select.png)

Basic Use
-------
`WearPreferenceActivity` works much the same way as Android's `PreferenceActivity` framework.

Start by defining which preferences to display. This is done in a layout xml file, as shown below. This is much like creating a preferences xml file for Android's `PreferenceActivity`, but a layout resource file is created instead (in `/res/layout` not `/res/xml`). This layout is never actually added to the window; it is just being used as a familiar way to define the structure of the preferences page.
```xml
<preference.PreferenceScreen
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >

    <preference.BooleanPreference
        app:pref_key="use_location"
        app:pref_title="Location"
        app:pref_iconOn="@drawable/ic_location_on"
        app:pref_iconOff="@drawable/ic_location_off"
        app:pref_summaryOn="@string/location_summary_on"
        app:pref_summaryOff="@string/location_summary_off"
        app:pref_defaultValue="true"
        app:pref_icon="@drawable/ic_launcher"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

    <preference.BooleanPreference
        app:pref_key="backup_data"
        app:pref_title="Data Backup"
        app:pref_iconOn="@drawable/ic_cloud_queue_white_24dp"
        app:pref_iconOff="@drawable/ic_cloud_off_white_24dp"
        app:pref_defaultValue="true"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

    <preference.ListPreference
        app:pref_key="language"
        app:pref_title="Language"
        app:pref_icon="@drawable/ic_language_white_24dp"
        app:pref_entries="@array/entries_language"
        app:pref_entryValues="@array/values_language"
        app:pref_defaultValue="en"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

    <preference.BooleanPreference
        app:pref_key="full_screen"
        app:pref_title="Full Screen"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

</preference.PreferenceScreen >
```

Next, create an `Activity` that extends `WearPreferenceActivity`, and add the preferences from the xml resource using the `addPreferencesFromResource` method. Don't forget to define the `Activity` in your `AndroidManifest.xml` file.

```java
public class MySettingsActivity extends WearPreferenceActivity {

    @Override protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        addPreferencesFromResource(R.layout.preferences);
    }

}
```

That's it! The preferences page is created. It will load and save the corresponding preference values, and it will automatically listen for external changes to preference values and update the view accordingly.

Build Configuration
--------
Add the following line to the gradle dependencies for your module.
```groovy
compile 'me.denley.wearpreferenceactivity:wearpreferenceactivity:0.4.0'
```

Preference Types
--------

This library includes two pre-build preference types: `BooleanPreference` and `ListPreferenece`, which behave in a similar fashion to their Android counterparts (`android.preference.CheckBoxPreference` and `android.preference.ListPreference`).

Other custom types can be added by extending the `Preference` class, and defining its behaviour in its implementation of the `onPreferenceClick()` method. You may also want to override `getSummary()` to have it show the current value of the preference.

If you would like to see any additional preference types included in this library, don't hesitate to submit an issue or a pull request.

License
-------

    Copyright 2015 Denley Bihari

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.