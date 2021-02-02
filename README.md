# splashscreen-demo
A simple app to show various approaches to implement splash screen in android.

## Splash screen using themes only

This is the most efficient approach as it doesn’t require any layout inflation and theme is generally initialized at the early stage of application launch. So, the users will see the splash screen as soon as they tap the launcher icon.

For this just add a new theme in your styles.xml and set the attribute windowBackground to your drawable (normally your app logo).

```xml
<style name="SplashTheme" parent="Theme.AppCompat.Light.NoActionBar">
    <item name="android:windowBackground">@drawable/splash</item>
</style>
```

The `splash` drawable is defined using `layer-list`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@android:color/white" />
    <item
        android:drawable="@mipmap/ic_launcher_round"
        android:gravity="center" />
</layer-list>
```

After that set the theme to your `SplashActivity` in the `AndroidManifest.xml` file.

```xml
<activity android:name=".SplashActivity" android:theme="@style/SplashTheme">
<intent-filter>
    <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

Remember not to inflate the layout file in onCreate() of the SplashActivity . You can also remove the layout file for SplashActivity if you are not going to use it.

```java
package com.softly.activities;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class SplashActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        startActivity(new Intent(this, MenuActivity.class));
        finish();
    }
    
}
```