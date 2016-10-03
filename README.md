### 使用方式：

你可以[下載檔案](http://urbrowser.kule.tw/js/kule.urbrowser.min.js) (ver. 3.161003)

```html
<script src="path/to/kule.urbrowser.min.js?domain=.你的網域"></script>
```

或是使用 CDN (ver. 3.161002):
```html
<script id="urbrowser" data-domain=".kule.tw" src="//cdnjs.cloudflare.com/ajax/libs/kule.lazy/3.1.161002/js/kule.urbrowser.min.js"></script>
```

無論使用以上哪一種方式，你可以將你的網域加入至 data-domain 或是在網址上加上參數（例如：kule.urbrowser.min.js?domain=.你的網域），如果是使用 3.161002 或是更之前的版本請額外加上 `id="urbrowser"`。當網頁讀取時就會自動開始執行，並且將使用者的瀏覽器、作業系統、平台等等資訊記錄下來並置放於上`<html>`上，例如：
```html
<html lang="en-US" id="mac" class="chrome chrome53 webkit" data-browser-name="chrome" data-browser-version="53.0.2785.116" data-os-name="mac" data-os-version="10.11.6" data-device="desktop" data-device-type="desktop" data-device-sim="desktop" data-orientation="landscape" data-screen-range="md" data-doc-range="md" data-layout-mode="desktop" data-inapp="false" data-webview="false" data-ub-version="3.161002">
```

IE 9+, Edge 12+, Chrome 4+, Firefox 3.5+, Safari 4+, Opera 11.5+ 等瀏覽器會另外儲存至 Cookie 與 [Local Storage](http://caniuse.com/#feat=namevalue-storage)，可隨時供 javascript 或後端語言使用，例如：
```javascript
{"project":"urBrowser","version":"3.161003","author":"Kei Cheng","srcWidth":1080,"srcHeight":1920,"docWidth":1080,"docHeight":964,"getNameByAgent":"chrome","getPlatform":"mac","getBrowserWithCoreNames":"chrome chrome53 webkit","getBrowserVersionsByName":{"int":53,"full":"53.0.2785.116"},"getOSName":"mac","getOSVersion":"10.11.6","getBrowserNames":{"name":"chrome","classes":"chrome chrome53 webkit"},"getBrowserFullVersion":"53.0.2785.116","getDevices":{"device":"desktop","type":"desktop","sim":"desktop"},"getOrientation":"landscape","getSizeRanges":{"screen":"md","document":"md"},"getLanguage":"en-US","isInApp":false,"isWebView":false,"getLayoutMode":"desktop"}
```

### 使用者的作業系統或平台

id 會記錄使用者的作業系統或平台，偶爾會發生在不同平台但相同瀏覽器的情況下發生部分的差異，所以透過 id 紀錄作業系統或是平台資訊，來處理CSS Hack，資訊包含 windows, wp(windows phone), mac, iphone, ipad, ipod, linux, android, chromeos, unix, solaris, playstation, nintendo, blackberry, freebsd, openbsd, palm, symbian，例如：
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

### 使用者的瀏覽器與核心

class 會記錄使用者的瀏覽器與核心甚至包含版本，記錄瀏覽器核心是為了在相同核心的瀏覽器發生問題時，可以一次處理，例如Chrome, Safari, 新版的Opera 都是使用 Webkit。記錄版本是可以針對某一個版本發生異狀時做個別處置。另外<del>萬惡的</del>IE 瀏覽器較為複雜，因此另外有做某版本向下相容的 class (IE 10以下為：ie10lt)，例如：
```html
<html class="ie6 ie7lt ie8lt ie9lt ie10lt ie11lt ie">
<html class="ie7 ie8lt ie9lt ie10lt ie11lt ie">
<html class="ie8 ie9lt ie10lt ie11lt ie">
<html class="ie9 ie10lt ie11lt ie">
<html class="ie10 ie11lt ie">
<html class="ie11 ie">
```

其他瀏覽器只會顯示「瀏覽器名稱」、「瀏覽器名稱+版本」以及「瀏覽器核心名稱」，例如：
```html
<html class="edge edge14 webkit">
<html class="chrome chrome53 webkit">
<html class="safari safari10 webkit">
<html class="firefox firefox47 gecko">
<html class="opera opera40 webkit">
```

當新的瀏覽器剛釋出時，當版本號低於2時或是沒有版本號時，則只會顯示「瀏覽器名稱」、以及「瀏覽器核心名稱」，例如：
```html
<html class="yolo webkit">
```

除了以上這些較為知名的瀏覽器之外，有一些瀏覽器是基於某個瀏覽器再添加各自的功能或特色，這種情況下尤其在 Chrome/Chromium 上較為明顯，此時該瀏覽器的 class 名稱則會另外新增 chrome 這個名稱，例如：
```html
<html class="yandex chrome webkit">
```

針對以上範例，在CSS Hack上就可以這麼寫：
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

.ie7 .selector {}

.ie8 .selector {}

.ie9 .selector {}

.ie10 .selector {}

.ie11 .selector {}
```

針對某版本 IE 版本以下，例如：只要 IE 11 以下，可以這樣寫：
```css
.ie11lt .selector {} /*IE10, 9, 8, 7, 6*/
```

以此類推：
```css
.ie10lt .selector {} /*IE9, 8, 7, 6*/

.ie9lt .selector {} /*IE8, 7, 6*/

.ie8lt .selector {} /*IE7, 6*/
```

如果要包含IE11到IE6，請使用：
```css
.ie .selector {}
```

針對所有使用Webkit核心的瀏覽器：
```css
.webkit .selector {}
```

針對Chrome, Firefox, Safari, Opera, Edge, Vivaldi：
```css
.chrome .selector {}

.firefox .selector {}

.safari .selector {}

.opera .selector {}

.edge .selector {}

.vivaldi .selector {}
```

針對Android原生瀏覽器：
```css
.adrBuiltin .selector {}
```

### 混合使用

有時候會發生不同作業系統某個相同瀏覽器的情況下有些微不同時，必須要做些Hack，例如：
```css
#mac.chrome .selector {
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
                padding-left: 2px;
        }
    }
}
```

### Webview

當使用 Webview 時，在某些情況下可能只需要針對 Webview 處理某些操作或是修正，因此如果你有使用 Webview 時，可在 User Agent 加上以下字串：cordova 或 phonegap 或 react 或 nodejs 或 webview 等字樣，如需分辨 iOS 與 Andoird 可如下表示：

*   iOS: webview-ios
*   Android: webview-android

在 `html` 標籤上就會顯示以下資訊 ：
```html
<html class="webview-ios webview webkit" data-webview="ios">
```
```html
<html class="webview-adr webview webkit" data-webview="android">
```

如果不是上述情況時，`data-webview` 則顯示為 `false`。

### 第三方 APP 內建的瀏覽器

有時使用者會從某些 APP 開啟連結，由 APP 內建的瀏覽器開啟，此時開發者難以知道使用者瀏覽器的版本，因此針對了 Facebook apps, Twitter, Line, Kakaotalk, MicroMessenger(微信) 等 APP 做識別，並且會將該 APP 名稱置入於 class 名稱內，例如：
```html
<html class="facebook webkit">
```

### 使用者的裝置

偵測使用者裝置以及寬度來區分Desktop, Tablet, Mobile三種，例如：
```html
<html data-device="desktop">
```

單純區分使用者裝置類型為 Desktop 與 Mobile 兩種
```html
<html data-device-type="desktop">
```

開發時為了方便檢視，data-device-sim 模擬現在文件尺寸是接近哪種裝置

data-screen-range 與 data-doc-range 的值是直接取得 screen 與 document 的寬度值，根據這個寬度來模擬現在的尺寸是接近哪一種裝置，包含 Phone, Tablet, Desktop，參考來源：http://www.cutegrids.com/，Phone => xs, Tablet=> sm, Desktop => md, Large Desktops => lg
```html
<html device-sim="desktop" data-screen-range="md" data-doc-range="lg">

<html device-sim="desktop" data-screen-range="md" data-doc-range="md">

<html device-sim="tablet" data-screen-range="md" data-doc-range="sm">

<html device-sim="phone" data-screen-range="md" data-doc-range="xs">
```

### Orientation

如果在行動裝置上會直接依據 window.orientation 回傳結果來判斷是portrait或是landscape，如果是電腦裝置則是計算寬與高的關係來模擬是portrait或是landscape，當直式畫面時顯示以下內容：
```html
<html data-orientation="portrait">
```

如果是橫式時則會顯示：
```html
    <html data-orientation="landscape">
```

### 瀏覽器名稱與版本號碼
```html
<html data-browser-name="chrome" data-browser-version="53.0.2785.116">
```

### OS 名稱與版本

記錄使用者裝置的系統名稱與版本號碼。
```html
<html data-os-name="mac" data-os-version="10.11.6">
```

### Layout Mode

無論使用 RWD 或是 AWD 時，可以分辨現在是使用哪一種設計版型。判斷規則為：如果是行動裝置並且視窗寬度小於 992px，會歸類在 Mobile Layout，反之則歸類於 Desktop Layout。
```html
<html data-layout-mode="desktop">
```

### LocalStorage 與 Cookie

urBrowser 會將所有資訊記錄於 LocalStorage 與 Cookie(預設時效為365天)，後端可透過 Cookie 取得資料，javascript 取得使用者瀏覽器資訊時，可直接透過 LocalStorage 取得，例如：
```javascript
    var urb = localStorage.getItem('urbrowser');

    urb = JSON.parse(urb);
    console.log(urb.getBrowserWithCoreNames); //
    console.log(urb.getOrientation); //
```
注意：不支援 IE 9 以下版本 (IE 9 以下應該也不需要處理 RWD 或 AWD 才是)

LocalStorage 資料
```javascript
{"project":"urBrowser","version":"3.161003","author":"Kei Cheng","srcWidth":1080,"srcHeight":1920,"docWidth":1080,"docHeight":964,"getNameByAgent":"chrome","getPlatform":"mac","getBrowserWithCoreNames":"chrome chrome53 webkit","getBrowserVersionsByName":{"int":53,"full":"53.0.2785.116"},"getOSName":"mac","getOSVersion":"10.11.6","getBrowserNames":{"name":"chrome","classes":"chrome chrome53 webkit"},"getBrowserFullVersion":"53.0.2785.116","getDevices":{"device":"desktop","type":"desktop","sim":"desktop"},"getOrientation":"landscape","getSizeRanges":{"screen":"md","document":"md"},"getLanguage":"en-US","isInApp":false,"isWebView":false,"getLayoutMode":"desktop"}
```

Cookie 資料
```javascript
urbrowser={"project":"urBrowser","version":"3.161003","author":"Kei Cheng","srcWidth":1080,"srcHeight":1920,"docWidth":1080,"docHeight":964,"getNameByAgent":"chrome","getPlatform":"mac","getBrowserWithCoreNames":"chrome chrome53 webkit","getBrowserVersionsByName":{"int":53,"full":"53.0.2785.116"},"getOSName":"mac","getOSVersion":"10.11.6","getBrowserNames":{"name":"chrome","classes":"chrome chrome53 webkit"},"getBrowserFullVersion":"53.0.2785.116","getDevices":{"device":"desktop","type":"desktop","sim":"desktop"},"getOrientation":"landscape","getSizeRanges":{"screen":"md","document":"md"},"getLanguage":"en-US","isInApp":false,"isWebView":false,"getLayoutMode":"desktop"}
```

可指定 Cookie 的 domain，只要在載入 js 檔案名稱後面加上參數：
```html
<script src="path/to/kule.urbrowser.min.js?domain=.你的網域"></script>
```
    
或是設定屬性 `data-domain=".你的網域"`：
```html
<script data-domain=".你的網域" src="path/to/kule.urbrowser.min.js"></script>
```

如果使用 3.161002 或更之前的版本請加上 id 與 data-domain。（你的網域前面建議增加 . 符號，如範例相同。）
```html
<script id="urbrowser" data-domain=".你的網域" src="path/to/kule.urbrowser.min.js"></script>
````

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
```php
object(stdClass)#1 (22) {
  ["project"]=>
  string(9) "urBrowser"
  ["version"]=>
  string(8) "3.161003"
  ["author"]=>
  string(9) "Kei Cheng"
  ["srcWidth"]=>
  int(1080)
  ["srcHeight"]=>
  int(1920)
  ["docWidth"]=>
  int(1080)
  ["docHeight"]=>
  int(964)
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
    string(13) "53.0.2785.116"
  }
  ["getOSName"]=>
  string(3) "mac"
  ["getOSVersion"]=>
  string(7) "10.11.6"
  ["getBrowserNames"]=>
  object(stdClass)#3 (2) {
    ["name"]=>
    string(6) "chrome"
    ["classes"]=>
    string(22) "chrome chrome53 webkit"
  }
  ["getBrowserFullVersion"]=>
  string(13) "53.0.2785.116"
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

### 瀏覽器支援

最後，urBrower 可支援的瀏覽器包含：IE 9+, Edge 12+, Chrome 4+, Firefox 3.5+, Safari 4+, Opera 11.5+。  
IE 6 至 IE 8 僅顯示瀏覽器資訊於 `<html>`上，但不會將資訊儲存於 Cookie 與 Web Storage。

IE 8 雖然支援 Web Storage，但是正常來說因為製作 RWD 或 AWD 時應該不太會需要支援到 IE 8，所以就放棄了。
