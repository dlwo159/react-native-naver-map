react-native-naver-map [![npm version](https://badge.fury.io/js/react-native-nmap.svg)](https://badge.fury.io/js/react-native-nmap)
-----

개인 버전수정요

네이버맵의 리액트 네이티브 브릿지입니다.

## 설치

```
npm install react-native-nmap --save;
```

- **React Native 0.60+**

```bash
$ cd ios/ && pod install
```

- **React Native <= 0.59**

```bash
$ react-native link react-native-nmap
$ cd ios/ && pod install
```

### 안드로이드 추가 설정

`/android/build.gradle` 파일에 아래와 같이 레포지터리를 추가합니다

```
allprojects {
    repositories {
        ...        
        maven { url 'https://repository.map.naver.com/archive/maven' } // 네이버 지도 저장소
    }
}
```

`/android/app/src/AndroidManifest.xml`에 아래와 같이 추가하고 발급받은 클라이언트 아이디로 바꿔줍니다.
```xml
<manifest>
    <application>
        <meta-data
            android:name="com.naver.maps.map.CLIENT_ID"
            android:value="YOUR_CLIENT_ID_HERE" />
    </application>
</manifest>
```

### IOS 추가 설정

`/ios/Podfile` 파일에 아래와 같이 레포지터리를 추가합니다

```
target 'projectName' do
    ...
    pod 'NMapsMap'  #네이버 지도 저장소
    ...
end
```

`info.plist`에 아래와 같이 발급받은 클라이언트 아이디를 추가해줍니다.

![image](https://user-images.githubusercontent.com/49827449/66392740-b2fd5f00-ea0b-11e9-8c38-23e604b1009d.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
...
    <key>NMFClientId</key>
    <string>YOUR_CLIENT_ID_HERE</string>
...
<dict>
<plist>
```

## 예제

```tsx
import NaverMapView, { Marker } from "react-native-nmap";

function MyMap() {
    const P0 = {latitude: 37.564362, longitude: 126.977011};
    const P1 = {latitude: 37.565051, longitude: 126.978567};
    const P2 = {latitude: 37.565383, longitude: 126.976292};

    return <NaverMapView style={{width: '100%', height: '100%'}}
                         showsMyLocationButton={true}
                         center={{...P0, zoom: 16}}
                         onTouch={e => console.warn('onTouch', JSON.stringify(e.nativeEvent))}
                         onCameraChange={e => console.warn('onCameraChange', JSON.stringify(e))}
                         onMapClick={e => console.warn('onMapClick', JSON.stringify(e))}>
        <Marker coordinate={P0} onClick={() => console.warn('onClick! p0')}/>
        <Marker coordinate={P1} pinColor="blue" onClick={() => console.warn('onClick! p1')}/>
        <Marker coordinate={P2} pinColor="red" onClick={() => console.warn('onClick! p2')}/>

    </NaverMapView>
}
```