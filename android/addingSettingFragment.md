### 설정 페이지 만들기
- 액티비티 만들기까지는 actionbar.md 참조

- 의존성 라이브러리 추가하기
```gradle
compile 'com.android.support:preference-v7:25.3.1'
```

- SettingsFragment extends PreferenceFragmentCompat {} 클래스 만들기
```java
public class SettingFragment extends PreferenceFragmentCompat {

    @Override
    public void onCreatePreferences(Bundle savedInstanceState, String rootKey) {

        addPreferencesFromResource(R.xml.pref_visualizer);

    }

}
```

- res 디렉터리 안에 xml 디렉터리 만들고, pref_visualizer.xml 파일 만들기(최상위 태그가 PreferenceScreen이어야함)
```xml
<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <CheckBoxPreference
        android:defaultValue="true"
        android:key="show_bass"
        app:title="Show bass"
        android:summaryOff="Hidden"
        android:summaryOn="Shown"
        />

</PreferenceScreen>
```

- 새로 띄워지는 액티비티의 레이아웃 설정하기(fragment 태그)
```xml
<?xml version="1.0" encoding="utf-8"?>
<fragment
    android:id="@+id/activity_setting"
    android:name="android.example.com.visualizerpreferences.AudioVisuals.SettingFragment"
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

- PreferenceFragmentsCompact 라이브러리를 사용하기 때문에, styles.xml 파일에 theme을 설정해주어야한다.
```xml
<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
        <!-- TODO (6) Add a theme for the preference -->
        <item name="preferenceTheme">@style/PreferenceThemeOverlay</item>
    </style>

</resources>

```
