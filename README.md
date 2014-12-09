<div class="wrap">
        <h1>Kule urBrowser</h1>
        <p>這是用來偵測使用者的作業系統、裝置以及瀏覽器資訊，並記錄於html標籤上。例如：
            <br /><code>&lt;html id="mac" class"chrome webkit" data-device="desktop"&gt;</code>
        </p>

        <div class="tabs">
            <div id="doc">
                <h2>使用方式：</h2>
                <p><code>&lt;script type="text/javascript" src="path/to/urbrowser.min.js"&gt;&lt;/script&gt;</code>
                </p>
                <p>當網頁讀取時就會自動開始執行，並且將使用者的瀏覽器、作業系統、平台等等資訊記錄下來並置放於上<code>&lt;html&gt;</code>上。例如：</p>
                <pre class="paperShadow shadow-right"><code class="language-markup">&lt;html id="iphone" class="chrome webkit" data-version="38" data-device="mobile" data-screen-mode="portrait" data-screen-width="320"&gt;</code></pre>
                <h3>使用者的作業系統或平台</h3>
                <p>id 會記錄使用者的作業系統或平台，偶爾會發生在不同平台但相同瀏覽器的情況下發生部分的差異，所以透過id紀錄作業系統或是平台資訊，來處理CSS Hack，資訊包含 windows, mac, linux, android, iphone, ipad, ipod, wp(windows phone)，例如：</p>
                <pre class="paperShadow shadow-right"><code class="language-markup">&lt;html id="mac"&gt;</code></pre>
                <p>在CSS Hack上就可以寫：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">#mac .selector {
    margin-top: -1px;
}</code></pre>
                <p>如果你有使用Sass, Compass或是Less，那麼可以這樣寫：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">#mac {
    .selector {
        margin-top: -1px;
    }
}</code></pre>
                <h3>使用者的瀏覽器與核心</h3>
                <p>class 會記錄使用者的瀏覽器與核心甚至包含版本，記錄瀏覽器核心是為了在相同核心的瀏覽器發生問題時，可以一次處理，例如Chrome, Safari, 新版的Opera 都是使用 Webkit。記錄版本是為了
                    <del>萬惡的</del>IE瀏覽器，例如：</p>
                <pre class="paperShadow shadow-right"><code class="language-markup">&lt;html class="ie ie6"&gt;</code></pre>
                <p>在CSS Hack上就可以寫：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">.ie6 .selector {
    margin-top: -1px;
}</code></pre>
                <p>如果是所有的IE：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">.ie .selector {
    margin-top: -1px;
}</code></pre>
                <p>針對某個IE版本（目前最低版本只到IE 6）：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">.ie6 .selector {}</code></pre>
                <pre class="paperShadow shadow-right"><code class="language-css">.ie7 .selector {}</code></pre>
                <pre class="paperShadow shadow-right"><code class="language-css">.ie8 .selector {}</code></pre>
                <pre class="paperShadow shadow-right"><code class="language-css">.ie9 .selector {}</code></pre>
                <pre class="paperShadow shadow-right"><code class="language-css">.ie10 .selector {}</code></pre>
                <pre class="paperShadow shadow-right"><code class="language-css">.ie11 .selector {}</code></pre>
                <p>針對Webkit核心：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">.webkit .selector {}</code></pre>
                <p>針對Chrome, Firefox, Safari, Opera：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">.chrome .selector {}</code></pre>
                <pre class="paperShadow shadow-right"><code class="language-css">.firefox .selector {}</code></pre>
                <pre class="paperShadow shadow-right"><code class="language-css">.safari .selector {}</code></pre>
                <pre class="paperShadow shadow-right"><code class="language-css">.opera .selector {}</code></pre>
                <p>針對Android原生瀏覽器：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">.androidBuiltin .selector {}</code></pre>
                <h3>混合使用</h3>
                <p>有時候會發生不同作業系統某個相同瀏覽器的情況下有些微不同時，必須要做些Hack，例如：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">#windows.chrome .selector {
    margin-top: -1px;
}

#mac.chrome .selector {
    margin-top: 1px;
}
</code></pre>
                <p>如果你有使用Sass, Compass或是Less，那麼可以這樣寫：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">#mac {
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
                <p>目前只有初步分類為Desktop以及Mobile兩種，以便針對不同裝置去處理Hack或是不同的設計，例如：</p>
                <pre class="paperShadow shadow-right"><code class="language-markup">&lt;html data-device="mobile"&gt;</code></pre>
                <p>在CSS Hack上就可以寫：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">[data-device="mobile"] .selector {
    margin-top: -1px;
}</code></pre>
                <h3>行動裝置的寬度以及橫式或直式的處理</h3>
                <p>這個部分只有使用者的裝置為 Mobile 時才會啟用，並且偵測該裝置的寬度以及裝置的擺放比例，例如當行動裝置畫面為直式時會顯示：</p>
                <pre class="paperShadow shadow-right"><code class="language-markup">&lt;html data-screen-mode="portrait" data-screen-width="320"&gt;</code></pre> 如果是橫式時則會顯示：
                <pre class="paperShadow shadow-right"><code class="language-markup">&lt;html data-screen-mode="landscape" data-screen-width="320"&gt;</code></pre>
                <p>在CSS Hack上就可以寫：</p>
                <pre class="paperShadow shadow-right"><code class="language-css">[data-screen-mode="portrait"] .selector {
    margin-top: -1px;
}

[data-screen-mode="landscape"] .selector {
    margin-top: 1px;
}
</code></pre><br/>
                <h2>Javascript 也能用</h2>
                <p>在js上可以取得你可能需要判別的資訊來做不同的功能撰寫或是效果，例如：</p>
                <pre class="paperShadow shadow-right"><code class="language-javascript">if( $('html').hasClass('ie') ){
    console.log('Suck!');
}
</code></pre>
                <p>以上，這是目前處理好的部分，未來或許有專案上遇到的新問題或是有人願意提供更好的方法時會繼續持續更新。</p>
            </div>
