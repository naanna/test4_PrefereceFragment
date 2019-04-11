# 实现设置Activity 

## 使用PrefereceFragment实现设置页面

基本要求：实现如下两个图拼接而成的设置界面

![tu](https://img-blog.csdnimg.cn/20190411143856378.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ3OTEzNA==,size_16,color_FFFFFF,t_70)

设置项说明

![tu1](https://img-blog.csdnimg.cn/20190411144040765.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ3OTEzNA==,size_16,color_FFFFFF,t_70)

1. 关键代码

    1. PreFragment.java
    ```java
    public class PreFragment extends PreferenceFragment {
    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        addPreferencesFromResource(R.xml.perference);
        }
    }
    ```
    1. MainActivity.java
    ```java
    public class MainActivity extends AppCompatActivity {
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            FragmentManager fragmentManager=getFragmentManager();
            //开启一个新事物
            FragmentTransaction transaction=fragmentManager.beginTransaction();
            PreFragment preFragment=new PreFragment();
            transaction.add(R.id.p1,preFragment);
            transaction.commit();
        }
    }
    ```
    1. perference.xml
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">
        <PreferenceCategory android:title="In-line preferences">
            <CheckBoxPreference
                android:key="Checkbox_preference"
                android:title="Checkbox_preference"
                android:summary="This a checkbox">
            </CheckBoxPreference>
        </PreferenceCategory>

        <PreferenceCategory android:title="Dialog-based preferences">
            <EditTextPreference
                android:title="EditTextPreference"
                android:key="EditTextPreference"
                android:summary="An example that uses an edit text dialog"
                android:dialogTitle="Enter your favortie animal">
            </EditTextPreference>
            <ListPreference
                android:key="list"
                android:title="List preference"
                android:summary="An example that use a list dialog"
                android:dialogTitle="Choose one"
                android:entries="@array/options"
                android:entryValues="@array/options">
            </ListPreference>
        </PreferenceCategory>

        <PreferenceCategory android:title="Launch preferences">
        <PreferenceScreen
                android:key="screen_preference"
                android:title="Screen preference"
                android:summary="Shows another screen of preferences">
                    <CheckBoxPreference
                        android:key="s_checkbox"
                        android:summary="Preference that is on the next screen but same hierarchy"
                        android:title="Toggle preference">
                    </CheckBoxPreference>
        </PreferenceScreen>
        <PreferenceScreen
            android:summary="Launches an Activity from an intent"
            android:title="Intent preference" >
            <intent
                android:action="android.intent.action.VIEW"
                android:data="http://www.google.com">
            </intent>
        </PreferenceScreen>
        </PreferenceCategory>
        <PreferenceCategory android:title="Preference attributes">
            <CheckBoxPreference
                android:key="parent_checkbox_preference"
                android:summary="This is visually parent"
                android:title="Parent checkbox preference">
            </CheckBoxPreference>
            <CheckBoxPreference
                android:key="child_checkbox_preference"
                android:summary="This is visually a child"
                android:title="Child checkbox preference"
                android:dependency="parent_checkbox_preference"/>
        </PreferenceCategory>
    </PreferenceScreen>
    ```
    1. arrays.xml
    ```xml
    <resources>
        <string-array name="options">
            <item>Alpha Option 01</item>
            <item>Beta Option 02 </item>
            <item>Charie Option 03</item>
        </string-array>
    </resources>
    ```
    1. activity_main.xml
    ```xml
    <fragment
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/p1"
        android:name="com.example.a54667.test4_preferecefragment.PreFragment"/>
    ```
1. 模拟器截图

    1. 主界面
    
        ![answer1](https://img-blog.csdnimg.cn/20190411144948499.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ3OTEzNA==,size_16,color_FFFFFF,t_70)

        ![answer2](https://img-blog.csdnimg.cn/20190411144852447.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ3OTEzNA==,size_16,color_FFFFFF,t_70)

    1. In-line preferences  

        CheckBoxPreference

        ![answer3](https://img-blog.csdnimg.cn/20190411144754459.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ3OTEzNA==,size_16,color_FFFFFF,t_70)

    1. Dialog-based preferences

        EditTextPreference

        ![answer4](https://img-blog.csdnimg.cn/20190411145104238.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ3OTEzNA==,size_16,color_FFFFFF,t_70)

        ListPreference

        ![answer5](https://img-blog.csdnimg.cn/20190411145154463.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ3OTEzNA==,size_16,color_FFFFFF,t_70)

    1. Launch preferences

        PreferenceScreen: 跳转到另一个PreferenceScreen

        ![answer6](https://img-blog.csdnimg.cn/20190411145239860.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ3OTEzNA==,size_16,color_FFFFFF,t_70)

        PreferenceScreen: 启动一个网页

        ![answer7](https://img-blog.csdnimg.cn/20190411145636843.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ3OTEzNA==,size_16,color_FFFFFF,t_70)

    1. Preference attributes

        CheckBox: 父选项
        CheckBox: 子选项，当父选项勾选时呈现

        ![answer8](https://img-blog.csdnimg.cn/20190411145330689.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ3OTEzNA==,size_16,color_FFFFFF,t_70)