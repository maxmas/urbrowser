Kule urBrowser
=============
version: 2.151107

這是用來偵測使用者的作業系統、裝置以及瀏覽器資訊，並記錄於html標籤上。例如：
```html
<html lang="en-US" id="mac" class="chrome chrome46 webkit" data-device="desktop" data-device-type="desktop" data-device-sim="desktop" data-browser-name="chrome" data-browser-version="46" data-os-name="mac" data-doc-size="screen-md" data-screen-size="screen-md" data-orientation="portrait" data-doc-width="1080" data-screen-width="1080" data-layout-mode="desktop" data-urbrowser="true">
```

##使用方式
你可以[下載檔案](http://urbrowser.kule.tw/js/kule.urbrowser.min.js)
```html
<script type="text/javascript" src="path/to/kule.urbrowser.min.js"></script>
```
或是使用 CDN:
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/kule.lazy/3.0.1106beta/js/kule.urbrowser.min.js"></script>
```

當網頁讀取時就會自動開始執行，並且將使用者的瀏覽器、作業系統、平台等等資訊記錄下來並置放於上`<html>`上。例如：
```html
<html lang="en-US" id="mac" class="chrome chrome46 webkit" data-device="desktop" data-device-type="desktop" data-device-sim="desktop" data-browser-name="chrome" data-browser-version="46" data-os-name="mac" data-doc-size="screen-md" data-screen-size="screen-md" data-orientation="portrait" data-doc-width="1080" data-screen-width="1080" data-layout-mode="desktop" data-urbrowser="true">
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
<html class="ie ie6">
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

###Cordova
當使用 Cordova 時，在某些情況下可能只需要針對 Cordova 處理某些操作或是修正，因此如果你有使用 Cordova 時，可在 User Agent 加上以下字串：

1. iOS: Cordova-iOS
2. Android: Cordova-Android

在 html 標籤上就會顯示以下資訊 (inapp 這個class是為了將來能夠共同處理 webapp 而新增。)：
```html
<html class="cordova-ios cordova webkit inapp">
```
```html
<html class="cordova-adr cordova webkit inapp">
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
phone => screen-xs, tablet=> screen-sm, desktop => screen-md, Large Desktops => screen-lg

```html
<html data-screen-width="1920" data-device-sim="desktop" data-screen-size="screen-lg">
```
```html
<html data-screen-width="1080" data-device-sim="desktop" data-screen-size="screen-md">
```
```html
<html data-screen-width="768" data-device-sim="tablet" data-screen-size="screen-sm">
```
```html
<html data-screen-width="480" data-device-sim="phone" data-screen-size="screen-xs">
```

###裝置的寬度以及橫式或直式的處理
如果在行動裝置上會直接依據 window.orientation 回傳結果來判斷是portrait或是landscape，如果是電腦裝置則是計算寬與高的關係來模擬是portrait或是landscape，當直式畫面時顯示以下內容：
```html
<html data-orientation="portrait" data-doc-width="320">
```

如果是橫式時則會顯示：
```html
<html data-orientation="landscape" data-doc-width="768">
```

###瀏覽器名稱與版本號碼
```html
<html data-browser-name="chrome" data-browser-version="46">
```

###Desktop 與 Windows 版本
當使用桌上型或筆記型電腦時，會記錄使用者的系統名稱，當使用者使用的是Windows系統時，會記錄該系統的版本號碼。
```html
<html data-os-name="windows" data-os-version="95">
```
```html
<html data-os-name="windows nt" data-os-version="6.2">
```

###Layout Mode
無論使用 RWD 或是 AWD 時，可以要分辨現在是使用哪一種設計版型。判斷規則為：如果是行動裝置並且視窗寬度小於 992px，會歸類在 Mobile Layout，反之則歸類於 Desktop Layout。在 Cookie 上則會提供 layout: isDesktopLayout 或是 isMobileLayout。
```html
<html data-layout-mode="desktop">
```

###Cookie
urBrowser 會將以上部分資訊記錄到 Cookie 上，以便後端或是其他用途使用。
```javascript
urbrowser={"device":"desktop","deviceType":"desktop","screenWidth":1080,"breakpoint":"screen-md","orientation":"portrait", "layout": "isDesktopLayout"}
```

當後端要使用時，以PHP為例：
```php
<?php
    $urbrowser = json_decode($_COOKIE['urbrowser']);
    $layout = $urbrowser->layout;

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
object(stdClass)#1 (6) {
  ["device"]=>
  string(7) "desktop"
  ["deviceType"]=>
  string(7) "desktop"
  ["screenWidth"]=>
  int(1080)
  ["breakpoint"]=>
  string(9) "screen-md"
  ["orientation"]=>
  string(8) "portrait"
  ["layout"]=>
  string(7) "desktop"
}
```