# React Native AMap Location
高得安卓定位SDK的Reac Native版本. [AMap Android Location SDK](http://lbs.amap.com/api/android-location-sdk/).

## Example
```
...
componentDidMount() {
  this.unlisten = AMapLocation.addEventListener((data) => console.log('data', data));
  AMapLocation.startLocation({
    accuracy: 'HighAccuracy',
    killProcess: true,

  });
}

componentWillUnmount() {
  this.unlisten();
}
...
```

## Install

### Step 1 - NPM install

```
npm install react-native-amap-location --save
```

### Step 2 - Update Gradle Settings

```
// file: android/settings.gradle
...

include ':reactamaplocation'
project(':reactamaplocation').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-amap-location')
```

### Step 3 - Update app Gradle Build

```
// file: android/app/build.gradle
...

dependencies {
    ...
    compile project(':reactamaplocation')
}
```

### Step 4 - Register React Package

```
import com.xiaobu.amap.AMapLocationReactPackage;
...
   /**
   * A list of packages used by the app. If the app uses additional views
   * or modules besides the default ones, add more packages here.
   */
    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
        new MainReactPackage(),
        new AMapLocationReactPackage()); // <-- Register package here
    }
...
```

### Step 5 - Add manifest
```
<!--用于进行网络定位-->
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"></uses-permission>
<!--用于访问GPS定位-->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"></uses-permission>
<!--获取运营商信息，用于支持提供运营商信息相关的接口-->
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
<!--用于访问wifi网络信息，wifi信息会用于进行网络定位-->
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"></uses-permission>
<!--这个权限用于获取wifi的获取权限，wifi信息会用来进行网络定位-->
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"></uses-permission>
<!--用于访问网络，网络定位需要上网-->
<uses-permission android:name="android.permission.INTERNET"></uses-permission>
<!--用于读取手机当前的状态-->
<uses-permission android:name="android.permission.READ_PHONE_STATE"></uses-permission>
<!--写入扩展存储，向扩展卡写入数据，用于写入缓存定位数据-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"></uses-permission>
<uses-permission android:name="android.permission.INTERNET" />

...
 <application
      android:allowBackup="true"
      android:label="@string/app_name"
      android:icon="@mipmap/ic_launcher"
      android:theme="@style/AppTheme">
      <service android:name="com.amap.api.location.APSService"></service>  <--- Add service
...
```


### Functions
startLocation(option)

stopLocation()

addEventListener(Callback)


### Options

needMars | false | 是否需要火星坐标
accuracy | HighAccuracy, BatterySaving or DeviceSensors
needAddress | true
onceLocation | false
wifiActiveScan | true
mockEnable | false
interval | 2000
gpsFirst | false
httpTimeOut | 30000
