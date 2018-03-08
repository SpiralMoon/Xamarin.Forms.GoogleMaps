## ![](logo.png) Xamarin.Forms.GoogleMaps 

![](https://img.shields.io/nuget/v/Xamarin.Forms.GoogleMaps.svg) ![](https://img.shields.io/nuget/dt/Xamarin.Forms.GoogleMaps.svg) [![Build status](https://build.mobile.azure.com/v0.1/apps/99e6fb9e-fe8c-49df-b190-8aa1732a0ad2/branches/master/badge)](https://mobile.azure.com) [![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/Xamarin-Forms-GoogleMaps/public)

[English README is here！](README.md)

[日本語の README はこちら！](README-ja.md)

Xamarin.Forms 전용 Google Maps 라이브러리입니다.

사용법은 [Xamarin.Forms.Maps](https://www.nuget.org/packages/Xamarin.Forms.Maps) 과 거의 동일합니다, [Xamarin.Forms.Maps - github](https://github.com/xamarin/Xamarin.Forms) 에서 fork 되었기 때문입니다.

## 데모 앱

데모 앱에서 Android와 iOS에 대한 이 라이브러리의 모든 기능을 사용해 볼 수 있습니다.
[데모 앱 소스코드](https://github.com/amay077/Xamarin.Forms.GoogleMaps/tree/master/XFGoogleMapSample).

* [Android 예제](https://install.mobile.azure.com/users/okuokuoku/apps/xfgooglemapsample/distribution_groups/trial) - 이 링크는 Android 브라우저에서 열어주세요.
* iOS 예제 - [Gitter](https://gitter.im/Xamarin-Forms-GoogleMaps/public) 에 요청 해주세요. (디바이스의 UUID가 필요합니다.)

![screenshot](screenshot01.png)

## 왜 이걸 만들었나

기존의 자마린 공식 [Xamarin.Forms.Map](https://developer.xamarin.com/guides/xamarin-forms/user-interface/map/)  라이브러리는 최소한의 기능만을 지원하고 있습니다.

특히, Bing Maps SDK 는 벡터 타일도 아니며 마커의 infowindow 기능도 없는 매우 구식입니다.

Android 와 iOS 가 모바일 앱 시장을 독점하고 있습니다. 그래서 굳이 Bing Maps 가 지원될 필요는 없다고 생각합니다.

더 나아가, iOS 에서도 MapKit 대신 Google Maps 를 사용하는 것이 Android 와 iOS 를 공통화하기 쉽다고 생각합니다.

**Xamarin.Forms.GoogleMaps 는 Xamarin.Forms 환경에서 Google maps 의 기능을 최대한 지원하고 있습니다!!**

## Xamarin.Forms.Maps 와 비교

|Feature|X.F.Maps|X.F.GoogleMaps|
| ------------------- | :-----------: | :-----------: |
|Map types|Yes|Yes|
|Traffic map|-|Yes|
|Map events|-|Yes|
|Panning with animation|Yes|Yes|
|Panning directly|-|Yes|
|Pins|Yes|Yes|
|Custom Pins|-|Yes|
|Pin drag & drop|-|Yes|
|Polygons|-|Yes|
|Lines|-|Yes|
|Circles|-|Yes|
|Custom map tiles|-|Yes|

더 많은 정보는 [Comparison with Xamarin.Forms.Maps](https://github.com/amay077/Xamarin.Forms.GoogleMaps/wiki/Comparison-with-Xamarin.Forms.Maps) 이곳에 있습니다.

## 구성

* NuGet 에서 사용할 수 있습니다. : https://www.nuget.org/packages/Xamarin.Forms.GoogleMaps/ [![NuGet](https://img.shields.io/nuget/v/Xam.Plugin.Geolocator.svg?label=NuGet)](https://www.nuget.org/packages/Xamarin.Forms.GoogleMaps/)
* NuGet을 통하여 자마린 프로젝트에 설치해주세요.

## 지원 플랫폼

|플랫폼|지원 여부|
| ------------------- | :-----------: |
|iOS Unified|Yes|
|Android|Yes|
|Windows 10 UWP|Yes (Bing map)|
|Others|No|

## 사용법

* [Map Control - Xamarin](https://developer.xamarin.com/guides/xamarin-forms/user-interface/map/)

iOS에서는 [Google Maps API for iOS](https://developers.google.com/maps/documentation/ios-sdk/) 와 같은 방법으로 API KEY를 가져올 수 있으며, KEY는 ``AppDelegate.cs`` 의 ``Init`` 함수 안에 매개변수로 넣어주어야 합니다.  

```csharp
// AppDelegate.cs
[Register("AppDelegate")]
public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
{
    public override bool FinishedLaunching(UIApplication app, NSDictionary options)
    {
        global::Xamarin.Forms.Forms.Init();
        Xamarin.FormsGoogleMaps.Init("your_google_maps_ios_api_key");
        LoadApplication(new App());

        return base.FinishedLaunching(app, options);
    }
}
``` 

UWP 에서는, Xamarin.Forms.GoogleMaps.UWP.dll 의 rendererAssemblies 를 ``Xamarin.Forms.Forms.Init()`` 에 파라미터로 넣어주세요.

```csharp
// App.xaml.cs
protected override void OnLaunched(LaunchActivatedEventArgs e)
{
    Frame rootFrame = Window.Current.Content as Frame;

    if (rootFrame == null)
    {
        rootFrame = new Frame();
        rootFrame.NavigationFailed += OnNavigationFailed;

        // Should add UWP side assembly to rendererAssemblies
        var rendererAssemblies = new []
        {
            typeof(Xamarin.Forms.GoogleMaps.UWP.MapRenderer).GetTypeInfo().Assembly
        };
        Xamarin.Forms.Forms.Init(e, rendererAssemblies);
        
        Xamarin.FormsGoogleMaps.Init("your_bing_maps_api_key");

        Window.Current.Content = rootFrame;
    }

    if (rootFrame.Content == null)
    {
        rootFrame.Navigate(typeof(MainPage), e.Arguments);
    }
    Window.Current.Activate();
}
```

네임스페이스는 ``Xamarin.Forms.Maps`` 대신에 ``Xamarin.Forms.GoogleMaps`` 를 사용합니다. 

아래 주소는 예제입니다.

* [XFGoogleMapSample](https://github.com/amay077/Xamarin.Forms.GoogleMaps/tree/master/XFGoogleMapSample)

## 패치 내용

[Releases](https://github.com/amay077/Xamarin.Forms.GoogleMaps/releases) 나 [RELEASE_NOTES](RELEASE_NOTES.md) 에 쓰여 있습니다.

## 향후 계획

되도록이면 Xamarin.Forms.Maps API 에 초점을 두고 Google Maps 의 고유 기능만 추가할 생각입니다.

[@amay077](https://twitter.com/amay077) 이나 submit ISSUE, Pull-request 등을 통해서 기능을 제안할 수 있습니다!

추가 기능 계획:

* ~~Pin.ShowInfoWindow/HideInfoWindow 함수(혹은 IsVisibleInfoWindow 속성)~~ 버전 v1.0.0 에 추가됨.
* ~~탭이나 홀드로 pin 옮기기~~ 버전 v1.5.0 에 추가됨.
* ~~Polygon, Polyline, Circle~~ 버전 v1.1.0 에 추가됨.
* and more [enhancements](https://github.com/amay077/Xamarin.Forms.GoogleMaps/labels/enhancement)!

이 라이브러리는 Google Maps에 최적화되어 있고, 새로운 기능은 UWP 에 추가하지 않을 것이기 때문에
Windows 10 UWP 환경을 지원하고는 있지만 사용하기에 적합하지는 않습니다.

## 컨트리뷰션

당신의 컨트리뷰션을 언제나 환영하며, 감사드립니다.

다만, 프로젝트에 기여하기 전에 오른쪽 문서를 먼저 읽어주세요. [컨트리뷰션 가이드라인](CONTRIBUTING.md).

## 개발자 채팅방

개발자 채팅방은 항상 오픈되어있습니다. [gitter room](https://gitter.im/Xamarin-Forms-GoogleMaps/public)!

## 라이센스

[라이센스](LICENSE) 를 확인해주세요.

* logo.png by [alecive](http://www.iconarchive.com/show/flatwoken-icons-by-alecive.html) - [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed)
* Android Icon made by [Hanan](http://www.flaticon.com/free-icon/android_109464) from www.flaticon.com
* Apple Icon made by [Dave Gandy](http://www.flaticon.com/free-icon/apple-logo_25345) from www.flaticon.com

