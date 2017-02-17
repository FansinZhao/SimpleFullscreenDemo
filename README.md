# SimpleFullscreenDemo
Simple FullScreen demo

##这是根据Android studio的Fullscreen的模板简化的,非常简单,仅当参考记录.
  根据模板的建议,抽取主要内容,将全屏的设置要点提出来.
##第一点,配置部分
  1,文件res/values/styles.xml添加两个style

    <style name="FullscreenTheme" parent="AppTheme">
        <item name="android:actionBarStyle">@style/FullscreenActionBarStyle</item>
        <item name="android:windowActionBarOverlay">true</item>
        <item name="android:windowBackground">@null</item>
        <item name="metaButtonBarStyle">?android:attr/buttonBarStyle</item>
        <item name="metaButtonBarButtonStyle">?android:attr/buttonBarButtonStyle</item>
    </style>

    <style name="FullscreenActionBarStyle" parent="Widget.AppCompat.ActionBar">
        <item name="android:background">@color/black_overlay</item>
    </style>
  
  2,添加属性文件res/values/attrs.xml,用于提供样式属性,缺失会报错.
  <resources>

    <!-- Declare custom theme attributes that allow changing which styles are
         used for button bars depending on the API level.
         ?android:attr/buttonBarStyle is new as of API 11 so this is
         necessary to support previous API levels. -->
    <declare-styleable name="ButtonBarContainerTheme">
        <attr name="metaButtonBarStyle" format="reference" />
        <attr name="metaButtonBarButtonStyle" format="reference" />
    </declare-styleable>

  </resources>

  3,修改文件src/main/AndroidManifest.xml
  <activity
            android:name=".FullscreenActivity"
            android:configChanges="orientation|keyboardHidden|screenSize"
            android:label="@string/app_name"
            android:theme="@style/FullscreenTheme">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
  替换theme为 android:theme="@style/FullscreenTheme"
##第二点,代码部分
  在activity中添加下面两段代码:
  
    @Override
    protected void onResume() {
        hideUI();
        super.onResume();
    }

    private void hideUI() {
        mContentView.setSystemUiVisibility(View.SYSTEM_UI_FLAG_LOW_PROFILE
                | View.SYSTEM_UI_FLAG_FULLSCREEN
                | View.SYSTEM_UI_FLAG_LAYOUT_STABLE
                | View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY
                | View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION
                | View.SYSTEM_UI_FLAG_HIDE_NAVIGATION);

        ActionBar actionBar = getSupportActionBar();
        if (actionBar != null) {
            actionBar.hide();
        }
    }
