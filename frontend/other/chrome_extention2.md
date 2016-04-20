### popup.js
```
// Copyright (c) 2014 The Chromium Authors. All rights reserved.
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.

/**
 * Get the current URL.
 *
 * @param {function(string)} callback - called when the URL of the current tab
 *   is found.
 */
function getCurrentTabUrl(callback) {
  // Query filter to be passed to chrome.tabs.query - see
  // https://developer.chrome.com/extensions/tabs#method-query
  var queryInfo = {
    active: true,
    currentWindow: true
  };

  chrome.tabs.query(queryInfo, function(tabs) {
    // chrome.tabs.query invokes the callback with a list of tabs that match the
    // query. When the popup is opened, there is certainly a window and at least
    // one tab, so we can safely assume that |tabs| is a non-empty array.
    // A window can only have one active tab at a time, so the array consists of
    // exactly one tab.
    var tab = tabs[0];

    // A tab is a plain object that provides information about the tab.
    // See https://developer.chrome.com/extensions/tabs#type-Tab
    var url = tab.url;
    var favIconUrl = tab.favIconUrl;

    // tab.url is only available if the "activeTab" permission is declared.
    // If you want to see the URL of other tabs (e.g. after removing active:true
    // from |queryInfo|), then the "tabs" permission is required to see their
    // "url" properties.
    console.assert(typeof url == 'string', 'tab.url should be a string');

    callback(url, favIconUrl);
  });

  // Most methods of the Chrome extension APIs are asynchronous. This means that
  // you CANNOT do something like this:
  //
  // var url;
  // chrome.tabs.query(queryInfo, function(tabs) {
  //   url = tabs[0].url;
  // });
  // alert(url); // Shows "undefined", because chrome.tabs.query is async.
}

function renderStatus(statusText) {
  document.getElementById('status').textContent = statusText;
}

document.addEventListener('DOMContentLoaded', function() {

    getCurrentTabUrl(function(url, favIconUrl){

      var qrcode = new QRCode("qrcode", {
          text: "http://jindo.dev.naver.com/collie",
          width: 200,
          height: 200,
          colorDark : "#000000",
          colorLight : "#ffffff",
          correctLevel : QRCode.CorrectLevel.H
      });
       qrcode.makeCode(url, favIconUrl)
      if (favIconUrl) {
        var fav = document.getElementById("fav")
        fav.src = favIconUrl
        document.getElementById("fav").style.display = 'block'
      }
      document.getElementById("qrcode").style.display = 'block';

  })
});

```
### popup.html
```
<!doctype html>
<!--
 This page is shown when the extension button is clicked, because the
 "browser_action" field in manifest.json contains the "default_popup" key with
 value "popup.html".
 -->
<html>
  <head>
    <title>Getting Started Extension's Popup</title>
    <style>
      body {
        font-family: "Segoe UI", "Lucida Grande", Tahoma, sans-serif;
        font-size: 100%;
        height: 220px;
        width: 220px;
      }
      #qrcode {
        position: absolute;
        top: 50%;
        left: 50%;
        margin: -100px 0 0 -100px;
        display: none;
      }
      #fav {
        display: none;
        opacity: .95;
        position: absolute;
        top: 50%;
        left: 50%;
        padding: 3px;
        width: 32px;
        height: 32px;
        margin-left: -16px;
        margin-top: -16px;
        border-radius: 5px;
        background: #fff;
        border: transparent;
        z-index: 100;
    }
    </style>

    <!--
      - JavaScript and HTML must be in separate files: see our Content Security
      - Policy documentation[1] for details and explanation.
      -
      - [1]: https://developer.chrome.com/extensions/contentSecurityPolicy
     -->
    <script src="./lib/qrcode.min.js"></script>
    <script src="popup.js"></script>
  </head>
  <body>
  <div id="qrcode"></div>
  <img id="fav" src="icon.png" alt="">
  </body>
</html>
```
### manifest.json
```

```
