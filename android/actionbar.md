### 서브 페이지 들어갔다가 뒤로가기 버튼 달아주는법
- AndroidManifest.xml 파일에서 서브 액티비티에 부모관계를 설정해주고, 부모 액티비티에는 singleTop으로 설정(뒤로 돌아갔을때 액티비티를 다시 생성하지 않도록 해주는 속성 
```xml
<application>

        <activity
            android:name=".activities.MainActivity"
            android:launchMode="singleTop"
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity
            android:name=".activities.SubActivity"
            android:parentActivityName=".activities.MainActivity"/>
</application>
```
- 매니페스트 설정이 끝났으면, 서브 액티비티에서 액션바를 설정해준다
```java
public class SettingsActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_settings);

        ActionBar actionBar = getSupportActionBar();

        if(actionBar != null) {
            actionBar.setDefaultDisplayHomeAsUpEnabled(true);
        }

    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {

        if(item.getItemId() == R.id.home) {
            NavUtils.navigateUpFromSameTask(this);
        }

        return super.onOptionsItemSelected(item);
    }
    
}
```
