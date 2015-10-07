<div class="wrap">
    <h1>Kule urBrowser</h1>
    <p>這是用來偵測使用者的作業系統、裝置以及瀏覽器資訊，並記錄於html標籤上。例如：
        <br />
        <pre><code class="language-markup htmlTag"></code></pre>
    </p>

    <div id="doc">
        <h2>使用方式：</h2>
        <p><pre><code class="language-markup">&lt;script type="text/javascript" src="path/to/kule.urbrowser.min.js"&gt;&lt;/script&gt;</code></pre>
        </p>
        <p>當網頁讀取時就會自動開始執行，並且將使用者的瀏覽器、作業系統、平台等等資訊記錄下來並置放於上<code>&lt;html&gt;</code>上。例如：</p>
        <pre><code class="language-markup htmlTag"></code></pre>
        <h3>使用者的作業系統或平台</h3>
        <p>id 會記錄使用者的作業系統或平台，偶爾會發生在不同平台但相同瀏覽器的情況下發生部分的差異，所以透過id紀錄作業系統或是平台資訊，來處理CSS Hack，資訊包含 windows, mac, linux, android, iphone, ipad, ipod, wp(windows phone)，例如：</p>
        <pre><code class="language-markup htmlId">&lt;html id="<span class="whatsystem"></span>"&gt;</code></pre>
        <p>在CSS Hack上就可以寫：</p>
        <pre><code class="language-css">#<span class="whatsystem"></span> .selector {
margin-top: -1px;
}</code></pre>
        <p>如果你有使用Sass, Compass或是Less，那麼可以這樣寫：</p>
        <pre><code class="language-css">#<span class="whatsystem"></span> {
.selector {
margin-top: -1px;
}
}</code></pre>
        <h3>使用者的瀏覽器與核心</h3>
        <p>class 會記錄使用者的瀏覽器與核心甚至包含版本，記錄瀏覽器核心是為了在相同核心的瀏覽器發生問題時，可以一次處理，例如Chrome, Safari, 新版的Opera 都是使用 Webkit。記錄版本是為了
            <del>萬惡的</del>IE瀏覽器，例如：</p>
        <pre><code class="language-markup">&lt;html class="ie ie6"&gt;</code></pre>
        <p>在CSS Hack上就可以寫：</p>
        <pre><code class="language-css">.ie6 .selector {
margin-top: -1px;
}</code></pre>
        <p>如果是所有的IE：</p>
        <pre><code class="language-css">.ie .selector {
margin-top: -1px;
}</code></pre>
        <p>針對某個IE版本（目前最低版本只到IE 6）：</p>
        <pre><code class="language-css">.ie6 .selector {}</code></pre>
        <pre><code class="language-css">.ie7 .selector {}</code></pre>
        <pre><code class="language-css">.ie8 .selector {}</code></pre>
        <pre><code class="language-css">.ie9 .selector {}</code></pre>
        <pre><code class="language-css">.ie10 .selector {}</code></pre>
        <pre><code class="language-css">.ie11 .selector {}</code></pre>
        <p>針對某版本IE版本以下，例如：只要IE 11以下，可以這樣寫：</p>
        <pre><code class="language-css">.ie11lt .selector {} /*IE10, 9, 8, 7, 6*/</code></pre>
        <p>以此類推：</p>
        <pre><code class="language-css">.ie10lt .selector {} /*IE9, 8, 7, 6*/</code></pre>
        <pre><code class="language-css">.ie9lt .selector {} /*IE8, 7, 6*/</code></pre>
        <pre><code class="language-css">.ie8lt .selector {} /*IE7, 6*/</code></pre>
        <p>如果要包含IE11到IE6，請使用 .ie。</p>
        <br /><br />
        <p>針對所有使用Webkit核心的瀏覽器：</p>
        <pre><code class="language-css">.webkit .selector {}</code></pre>
        <p>針對Chrome, Firefox, Safari, Opera, Edge：</p>
        <pre><code class="language-css">.chrome .selector {}</code></pre>
        <pre><code class="language-css">.firefox .selector {}</code></pre>
        <pre><code class="language-css">.safari .selector {}</code></pre>
        <pre><code class="language-css">.opera .selector {}</code></pre>
        <pre><code class="language-css">.edge .selector {}</code></pre>
        <p>針對Android原生瀏覽器：</p>
        <pre><code class="language-css">.adrBuiltin .selector {}</code></pre>
        <h3>混合使用</h3>
        <p>有時候會發生不同作業系統某個相同瀏覽器的情況下有些微不同時，必須要做些Hack，例如：</p>
        <pre><code class="language-css">#<span class="whatsystem"></span>.<span class="whatbrowsername"></span> .selector {
margin-top: -1px;
}

#<span class="whatsystem"></span>.<span class="whatbrowsername"></span> .selector {
margin-top: 1px;
}
</code></pre>
        <p>如果你有使用Sass, Compass或是Less，那麼可以這樣寫：</p>
        <pre><code class="language-css">#<span class="whatsystem"></span> {
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
}</code></pre>
        <h3>使用者的裝置</h3>
        <p>使用者的裝置類型分為Desktop以及Mobile兩種，以便針對不同裝置去處理Hack或是不同的設計，例如：</p>
        <pre><code class="language-markup">&lt;html data-device-type="mobile"&gt;</code></pre>
        <p>在CSS Hack上就可以寫：</p>
        <pre><code class="language-css">[data-device-type="mobile"] .selector {
margin-top: -1px;
}</code></pre><br />
        <p>搭配尺寸範圍可分類為 Phone, Tablet, Desktop 三種。</p>
        <pre><code class="language-markup">&lt;html data-device="phone"&gt;</code></pre>
        <p>開發時為了方便檢視，data-device-sim 模擬現在文件尺寸是接近哪種裝置</p>
        <p>data-screen-width 的值是直接取得 document 的寬度值，根據這個寬度來模擬現在的尺寸是接近哪一種裝置，包含 Phone, Tablet, Desktop，參考來源：http://www.cutegrids.com/，phone => screen-xs, tablet=> screen-sm, desktop => screen-md, Large Desktops => screen-lg</p>
        <pre><code class="language-markup">&lt;html data-screen-width="1920" data-device-sim="desktop" data-screen-size="screen-lg"&gt;</code></pre>
        <pre><code class="language-markup">&lt;html data-screen-width="1080" data-device-sim="desktop" data-screen-size="screen-md"&gt;</code></pre>
        <pre><code class="language-markup">&lt;html data-screen-width="768" data-device-sim="tablet" data-screen-size="screen-sm"&gt;</code></pre>
        <pre><code class="language-markup">&lt;html data-screen-width="480" data-device-sim="phone" data-screen-size="screen-xs"&gt;</code></pre>

        <h3>裝置的寬度以及橫式或直式的處理</h3>
        <p>如果在行動裝置上會直接依據 window.orientation 回傳結果來判斷是portrait或是landscape，如果是電腦裝置則是計算寬與高的關係來模擬是portrait或是landscape，當直式畫面時顯示以下內容：</p>
        <pre><code class="language-markup">&lt;html data-orientation="portrait" data-doc-width="320"&gt;</code></pre>如果是橫式時則會顯示：
        <pre><code class="language-markup">&lt;html data-orientation="landscape" data-doc-width="768"&gt;</code></pre>

        <h3>瀏覽器名稱與版本號碼</h3>
        <pre><code class="language-markup">&lt;html data-browser-name="chrome" data-browser-version="41"&gt;</code></pre>
        <h3>Desktop 與 Windows 版本</h3>
        <p>當使用桌上型或筆記型電腦時，會記錄使用者的系統名稱，當使用者使用的是Windows系統時，會記錄該系統的版本號碼。</p>
        <pre><code class="language-markup">&lt;html data-os-name="windows" data-os-version="95"&gt;</code></pre>
        <pre><code class="language-markup">&lt;html data-os-name="windows nt" data-os-version="6.2"&gt;</code></pre>
        <h3>Cookie</h3>
        <p>urBrowser 會將 data-device 的資訊記錄到 Cookie 上，以便後端可以使用。</p>
        <pre><code class="language-js">urbrowser={"device":"desktop","deviceType":"desktop","screenWidth":1080,"breakpoint":"screen-md","orientation":"portrait"}</code></pre>
        <br />
        <p>當後端要使用時，以PHP為例：</p>
        <pre class="language-php"><code class="language-php">&lt;?php
$urbrowser = json_decode($_COOKIE['urbrowser']);
$device = $urbrowser->device;

if ($device == 'desktop') {
//dosomething...
}

if ($device == 'tablet') {
//dosomething...
}

if ($device == 'phone') {
//dosomething...
}
?&gt;</code></pre>
</div>
</div>