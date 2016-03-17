# React Native AMap Location
高得安卓定位SDK的Reac Native版本. [AMap Android Location SDK](http://lbs.amap.com/api/android-location-sdk/).

在国内由于众所周知的原因，安卓机子在国内几乎没法使用wifi定位，导致LBS应用很难通过RN自带的geoloc实现。所以在国内还是用个SDK比较好。


## Example
```
...
componentDidMount() {
  this.unlisten = AMapLocation.addEventListener((data) => console.log('data', data));
  AMapLocation.startLocation({
    accuracy: 'HighAccuracy',
    killProcess: true,
    needDetail: true,
  });
}

componentWillUnmount() {
  this.unlisten();
}
...

/*
result:
{
  accuracy: 29
  adCode: "310114"
  address: "上海市嘉定区嘉三路靠近同济大学嘉定校区华楼"
  altitude: 0
  bearing: 0
  city: "上海市"
  cityCode: "021"
  country: "中国"
  district: "嘉定区"
  latitude: 31.285728
  locationDetail: "-1"
  locationType: 4
  longitude: 121.217404
  poiName: "同济大学嘉定校区华楼"
  provider: "lbs"
  province: "上海市"
  satellites: 0
  speed: 0
  street: "嘉松北路"
  streetNum: "6128号"
}
*/
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

### Step 5 - Add service apik key and permissions
```
// file: android/srsettings.gradle
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
      <service android:name="com.amap.api.location.APSService"></service>
      <meta-data
         android:name="com.amap.api.v2.apikey"
         android:value="Your api key here"/>
...
```


### Functions
startLocation(options)

stopLocation()

unlistenFn = addEventListener(Callback(result))

### Options
```
默认设置
{
  needDetail: false, // 显示详细信息
  needMars: false, // 是否需要火星坐标，默认将火星坐标转为地球坐标
  accuracy: 'HighAccuracy', // BatterySaving or DeviceSensors
  needAddress: true,
  onceLocation: false,
  wifiActiveScan: true,
  mockEnable: false,
  interval: 2000,
  gpsFirst: false,
  httpTimeOut: 30000,
}
```
