Kule urBrowser
=============
version: 3.160914

這是用來偵測使用者的作業系統、裝置以及瀏覽器資訊，並記錄於html標籤上。例如：
```html
<html lang="en-US" id="mac" class="chrome chrome53 webkit" data-device="desktop" data-device-type="desktop" data-device-sim="desktop" data-browser-name="chrome" data-browser-version="46" data-os-name="mac" data-doc-size="screen-md" data-screen-size="screen-md" data-orientation="portrait" data-doc-width="1080" data-screen-width="1080" data-layout-mode="desktop" data-inapp="false" data-urbrowser="true" >
```

##使用方式
你可以[下載檔案 (ver. 3.160914)](http://urbrowser.kule.tw/js/kule.urbrowser.min.js)
```html
<script type="text/javascript" src="path/to/kule.urbrowser.min.js"></script>
```
或是使用 CDN (ver. 3.160913):
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/kule.lazy/3.1.160913/js/kule.urbrowser.min.js"></script>
```

當網頁讀取時就會自動開始執行，並且將使用者的瀏覽器、作業系統、平台等等資訊記錄下來並置放於上`<html>`上。例如：
```html
<html lang="en-US" id="mac" class="chrome chrome46 webkit" data-device="desktop" data-device-type="desktop" data-device-sim="desktop" data-browser-name="chrome" data-browser-version="46" data-os-name="mac" data-doc-size="screen-md" data-screen-size="screen-md" data-orientation="portrait" data-doc-width="1080" data-screen-width="1080" data-layout-mode="desktop" data-inapp="false" data-urbrowser="true" >
```

###使用者的作業系統或平台
id 會記錄使用者的作業系統或平台，偶爾會發生在不同平台但相同瀏覽器的情況下發生部分的差異，所以透過id紀錄作業系統或是平台資訊，來處理CSS Hack，資訊包含 windows, mac, linux, android, iphone, ipad, ipod, wp(windows phone)，例如：
```html
<html id="mac">
```

在CSS Hack上就可以寫：
```css
#mac .selector {
    margin-top: -1px;
}
```

如果你有使用Sass, Compass或是Less，那麼可以這樣寫：
```css
#mac {
    .selector {
        margin-top: -1px;
    }
}
```

###使用者的瀏覽器與核心
class 會記錄使用者的瀏覽器與核心甚至包含版本，記錄瀏覽器核心是為了在相同核心的瀏覽器發生問題時，可以一次處理，例如Chrome, Safari, 新版的Opera 都是使用 Webkit。記錄版本是為了 萬惡的IE瀏覽器，例如：
```html
<html class="ie6 ie">
```

在CSS Hack上就可以寫：
```css
.ie6 .selector {
    margin-top: -1px;
}
```

如果是所有的IE：
```css
.ie .selector {
    margin-top: -1px;
}
```

針對某個IE版本（目前最低版本只到IE 6）：
```css
.ie6 .selector {}
```
```css
.ie7 .selector {}
```
```css
.ie8 .selector {}
```
```css
.ie9 .selector {}
```
```css
.ie10 .selector {}
```
```css
.ie11 .selector {}
```

針對某版本IE版本以下，例如：只要IE 11以下，可以這樣寫：
```css
.ie11lt .selector {} /*IE10, 9, 8, 7, 6*/
```

以此類推：
```css
.ie10lt .selector {} /*IE9, 8, 7, 6*/
```
```css
.ie9lt .selector {} /*IE8, 7, 6*/
```
```css
.ie8lt .selector {} /*IE7, 6*/
```
如果要包含IE11到IE6，請使用 .ie。

####針對所有使用Webkit核心的瀏覽器：
```css
.webkit .selector {}
```

針對Chrome, Firefox, Safari, Opera, Edge：
```css
.chrome .selector {}
```
```css
.firefox .selector {}
```
```css
.safari .selector {}
```
```css
.opera .selector {}
```
```css
.edge .selector {}
```

針對Android原生瀏覽器：
```css
.adrBuiltin .selector {}
```

###混合使用
有時候會發生不同作業系統某個相同瀏覽器的情況下有些微不同時，必須要做些Hack，例如：
```css
#windows.chrome .selector {
    margin-top: -1px;
}

#mac.opera .selector {
    margin-top: 1px;
}
```

如果你有使用Sass, Compass或是Less，那麼可以這樣寫：
```css
#mac {
    &.chrome {
        .selector {
                margin-top: -1px;
        }
    }

    &.opera {
        .selector {
                margin-top: 1px;
        }
    }
}
```

###Webview
當使用 Webview 時，在某些情況下可能只需要針對 Webview 處理某些操作或是修正，因此如果你有使用 Webview 時，可在 User Agent 加上以下字串：cordova 或 phonegap 或 react 或 nodejs 或 webview 等字樣，如需分辨 iOS 與 Andoird 可如下表示：

1. iOS: webview-ios
2. Android: webview-android

在 html 標籤上就會顯示以下資訊：
```html
<html class="webview-ios webview webkit" data-webview="ios">
```
```html
<html class="webview-adr webview webkit" data-webview="android">
```

如果不是上述情況時，`data-webview` 則顯示為 `false`。


###第三方 APP 內建的瀏覽器
有時使用者會從某些 APP 開啟連結，由 APP 內建的瀏覽器開啟，此時開發者難以知道使用者瀏覽器的版本，因此針對了 Facebook apps, Twitter, Line, Kakaotalk, MicroMessenger(微信) 等 APP 做識別，並且會將該 APP 名稱置入於 class 名稱內，例如：
```html
<html class="facebook webkit">
```

###使用者的裝置
使用者的裝置類型分為Desktop以及Mobile兩種，以便針對不同裝置去處理Hack或是不同的設計，例如：
```html
<html data-device-type="desktop">
```

在CSS Hack上就可以寫：
```css
[data-device-type="desktop"] .selector {
    margin-top: -1px;
}
```

搭配尺寸範圍可分類為 Phone, Tablet, Desktop 三種。
```html
<html data-device="desktop">
```

開發時為了方便檢視，data-device-sim 模擬現在文件尺寸是接近哪種裝置
data-screen-width 的值是直接取得 document 的寬度值，根據這個寬度來模擬現在的尺寸是接近哪一種裝置，包含 Phone, Tablet, Desktop，參考來源：[http://www.cutegrids.com/](http://www.cutegrids.com/)，
phone => xs, tablet=> sm, desktop => md, Large Desktops => lg

```html
<html data-screen-range="lg">
```
```html
<html data-screen-range="md">
```
```html
<html data-screen-range="sm">
```
```html
<html data-screen-range="xs">
```

###裝置的寬度以及橫式或直式的處理
如果在行動裝置上會直接依據 window.orientation 回傳結果來判斷是portrait或是landscape，如果是電腦裝置則是計算寬與高的關係來模擬是portrait或是landscape，當直式畫面時顯示以下內容：
```html
<html data-orientation="portrait">
```

如果是橫式時則會顯示：
```html
<html data-orientation="landscape">
```

###瀏覽器名稱與版本號碼
```html
<html data-browser-name="chrome" data-browser-version="53.0.2785.101">
```

###OS 名稱與版本
記錄使用者裝置的系統名稱與版本號碼。
```html
<html data-os-name="mac" data-os-version="10.11.6">
```

###Layout Mode
無論使用 RWD 或是 AWD 時，可以要分辨現在是使用哪一種設計版型。判斷規則為：如果是行動裝置並且視窗寬度小於 992px，會歸類在 Mobile Layout，反之則歸類於 Desktop Layout。
```html
<html data-layout-mode="desktop">
```

###Cookie
urBrowser 會將以上部分資訊記錄到 Cookie 上，以便後端或是其他用途使用。
```javascript
urbrowser={"project":"urBrowser","version":"3.160914","author":"Kei Cheng","srcWidth":1080,"srcHeight":1920,"docWidth":1080,"docHeight":1015,"getNameByAgent":"chrome","getPlatform":"mac","getBrowserWithCoreNames":"chrome chrome53 webkit","getBrowserVersionsByName":{"int":53,"full":"53.0.2785.101"},"getOSName":"mac","getOSVersion":"10.11.6","getBrowserNames":{"name":"chrome","class":"chrome chrome53 webkit"},"getBrowserFullVersion":"53.0.2785.101","getDevices":{"device":"desktop","type":"desktop","sim":"desktop"},"getOrientation":"landscape","getSizeRanges":{"screen":"md","document":"md"},"getLanguage":"en-US","isInApp":false,"isWebView":false,"getLayoutMode":"desktop"}
```

當後端要使用時，以PHP為例：
```php
<?php
    $urbrowser = json_decode($_COOKIE['urbrowser']);
    $layout = $urbrowser->getLayoutMode;

    if ($layout == 'desktop') {
        //dosomething...
    }

    if ($layout == 'mobile') {
        //dosomething...
    }
?>
```

以下為 PHP var_dump 之後出來的結果：
```
object(stdClass)#1 (22) {
  ["project"]=>
  string(9) "urBrowser"
  ["version"]=>
  string(8) "3.160914"
  ["author"]=>
  string(9) "Kei Cheng"
  ["srcWidth"]=>
  int(1080)
  ["srcHeight"]=>
  int(1920)
  ["docWidth"]=>
  int(1080)
  ["docHeight"]=>
  int(1015)
  ["getNameByAgent"]=>
  string(6) "chrome"
  ["getPlatform"]=>
  string(3) "mac"
  ["getBrowserWithCoreNames"]=>
  string(22) "chrome chrome53 webkit"
  ["getBrowserVersionsByName"]=>
  object(stdClass)#2 (2) {
    ["int"]=>
    int(53)
    ["full"]=>
    string(13) "53.0.2785.101"
  }
  ["getOSName"]=>
  string(3) "mac"
  ["getOSVersion"]=>
  string(7) "10.11.6"
  ["getBrowserNames"]=>
  object(stdClass)#3 (2) {
    ["name"]=>
    string(6) "chrome"
    ["class"]=>
    string(22) "chrome chrome53 webkit"
  }
  ["getBrowserFullVersion"]=>
  string(13) "53.0.2785.101"
  ["getDevices"]=>
  object(stdClass)#4 (3) {
    ["device"]=>
    string(7) "desktop"
    ["type"]=>
    string(7) "desktop"
    ["sim"]=>
    string(7) "desktop"
  }
  ["getOrientation"]=>
  string(9) "landscape"
  ["getSizeRanges"]=>
  object(stdClass)#5 (2) {
    ["screen"]=>
    string(2) "md"
    ["document"]=>
    string(2) "md"
  }
  ["getLanguage"]=>
  string(5) "en-US"
  ["isInApp"]=>
  bool(false)
  ["isWebView"]=>
  bool(false)
  ["getLayoutMode"]=>
  string(7) "desktop"
}
```
