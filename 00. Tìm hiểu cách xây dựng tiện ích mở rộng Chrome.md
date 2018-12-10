# Tìm hiểu cách xây dựng tiện ích mở rộng Chrome

## 1. Tại sao?

Tiện ích mở rộng Chrome là _cả một_ **_thế giới cơ hội khác_** để xây dựng các công cụ hỗ trợ web!

### Thông tin nhanh

* Gần **_53% mọi người sử dụng Chrome_** để truy cập Internet trên các thiết bị máy tính để bàn. xem: [http://gs.statcorer.com/#desktop-browser-ww-monthly-201506-201506-bar](http://gs.statcounter.com/#desktop-browser-ww-monthly-201506-201506-bar)
* **Chromebook** là phân khúc **_phát triển nhanh nhất_** của thị trường PC. Trong năm 2014, Chromebook chiếm 14% tổng doanh số của máy tính xách tay cho cả kênh thương mại và bán lẻ; tăng 85 phần trăm từ năm 2013. [http://betanews.com/2015/02/24/2015-is-year-of-the-chromebook/](http://betanews.com/2015/02/24/2015-is-year-of-the-chromebook/)
* Các tiện ích mở rộng của Chrome có thể được xây dựng để trở thành các ứng dụng toàn diện chạy trong _mọi_ môi trường chrome.
* Vì Tiện ích mở rộng Chrome của bạn được **_viết bằng Công nghệ web tiêu chuẩn: HTML + CSS + JavaScript_**, bạn có thể sử dụng lại mã giao diện người dùng web của mình với sửa đổi tối thiểu (với điều kiện đã được mô đun hóa).

## 2. Là gì?

Tiện ích mở rộng là các chương trình nhỏ có thể sửa đổi và nâng cao chức năng của trình duyệt Chrome. Bạn viết chúng bằng các công nghệ web tiêu chuẩn web (HTML, JavaScript và CSS).

Tiện ích mở rộng của Chrome ( hoặc"Apps") cho phép bạn tạo các công cụ trong trình duyệt để thêm chức năng cho trải nghiệm duyệt web. Trong trường hợp của chúng ta, chúng ta muốn dành cho mọi người.

## 3. Thế nào ?

### Quyền

* Các quyền là gì? [https://developer.chrome.com/extensions/permissions](https://developer.chrome.com/extensions/permissions)

### _Ví dụ:_

#### Hành động của trình duyệt (Khi người đó nhấp vào Biểu tượng tiện ích mở rộng)

Tác vụ của trình duyệt cho phép bạn thêm một biểu tượng vào trình duyệt, ví dụ:

![hành động trình duyệt](https://developer.chrome.com/static/images/browser-action.png)

Xem: [https://developer.chrome.com/extensions/browserAction](https://developer.chrome.com/extensions/browserAction)

Ví dụ về một Hành động Trình duyệt đơn giản là một biểu tượng mà khi nhấp vào sẽ thay đổi nền trang.

Xem: [https://github.com/dwyl/learn-chrome-extensions/tree/master/examples/make_page_red](https://github.com/dwyl/learn-chrome-extensions/tree/master/examples/make_page_red)

#### Hiển thị danh sách Dấu trang

Sử dụng API dấu trang để hiển thị danh sách các dấu trang của người đó khi họ nhấp vào biểu tượng ( `browser_action` )

![chrome-mở rộng-đánh dấu-người xem](https://cloud.githubusercontent.com/assets/194400/11568030/e4a1eba8-99e1-11e5-83a3-cf7709a10ed0.png)

Xem: [https://github.com/dwyl/learn-chrome-extensions/tree/master/examples/my_bookmarks](https://github.com/dwyl/learn-chrome-extensions/tree/master/examples/my_bookmarks)

#### Thay đổi `src` của Biểu tượng khi nhấp vào

Hãy tưởng tượng ứng dụng của bạn muốn thay đổi biểu tượng để phản hồi lại một sự kiện hoặc thông báo:

Điều đó khá dễ dàng với dòng sau:

```js
chrome.browserAction.setIcon({path:"icon-notification.png"});
```

xem: [https://github.com/dwyl/learn-chrome-extensions/tree/master/examples/set_icon_path](https://github.com/dwyl/learn-chrome-extensions/tree/master/examples/set_icon_path)

#### Truy cập dữ liệu trình duyệt ( _Xóa lịch sử_ )

Sử dụng API `chrome.browsingData` để xóa dữ liệu duyệt web khỏi hồ sơ cục bộ của người dùng.

![duyệtdata_api](https://cloud.githubusercontent.com/assets/194400/11569180/62dc7956-99e8-11e5-8c1c-15be80af7590.png)

API chỉ cho phép bạn xóa lịch sử, do đó, nó chỉ hữu ích cho giới hạn một số ứng dụng.

xem: [https://developer.chrome.com/extensions/browsingData](https://developer.chrome.com/extensions/browsingData)

#### Sử dụng Phím tắt Keyboad trong Tiện ích mở rộng của bạn

Sử dụng `commands.onCommand` chúng ta có thể ra lệnh bàn phím để kích hoạt các sự kiện trong tiện ích mở rộng của mình.

Các lệnh được định nghĩa trong `manifest.json` là:

```js
"commands": {
  "toggle-feature": {
    "suggested_key": { "default": "Ctrl+Shift+Y" },
    "description": "Send a 'toggle-feature' event to the extension"
  },
  "_execute_browser_action": {
    "suggested_key": {
      "default": "Ctrl+Shift+F",
      "mac": "MacCtrl+Shift+F"
    }
  }
}
```

Điều này có thể hữu ích để mở một trang nền (cửa sổ bật lên) để đọc nội dung, ví dụ: hãy tưởng tượng nếu tiện ích mở rộng của bạn cung cấp tiện ích nhắn tin tức thời và bạn có thể thấy các tin nhắn mới nhất từ ​​bất kỳ trang nào mà không cần mở trình nhắn tin.

xem: [https://developer.chrome.com/extensions/commands](https://developer.chrome.com/extensions/commands)

#### Sử dụng desktopCapture để chụp ảnh màn hình

`desktopCapture` cho phép bạn chụp màn hình của những client.<br>

![chrome-mở rộng-chụp-máy tính để bàn](https://cloud.githubusercontent.com/assets/194400/11576119/7f2aa1ae-9a0c-11e5-8f61-f342b5f60448.png)<br>

xem: https://github.com/dwyl/learn-chrome-extensions/tree/master/examples/desktop_capture<br>
và: [https://developer.chrome.com/extensions/desktopCapture](https://developer.chrome.com/extensions/desktopCapture)

#### Lấy danh sách các thiết bị đã đăng nhập

API `signedInDevices` cung cấp cho bạn danh sách tất cả các thiết bị mà người đó đã đăng nhập bằng tài khoản Google của họ:

![thiết bị chrome](https://cloud.githubusercontent.com/assets/194400/11576561/6d0102e0-9a0f-11e5-94b7-e5d779b845f2.png)

xem: https://github.com/dwyl/learn-chrome-extensions/tree/master/examples/my_devices<br>
API: [https://developer.chrome.com/extensions/signInDevices](https://developer.chrome.com/extensions/signedInDevices)

#### Thông báo!

Vậy bạn có muốn hiển thị thông báo cho mọi người trong Chrome hay không?

![chrome-ext-thông báo](https://cloud.githubusercontent.com/assets/194400/11591150/8262ba6a-9a8d-11e5-8354-4fff6a3d54c0.png)

xem: https://github.com/dwyl/learn-chrome-extensions/tree/master/examples/notifications cho trình thông báo của Toast.<br>
API: [https://developer.chrome.com/apps/notifying](https://developer.chrome.com/apps/notifications)

#### Event Page > Alarms

> 'declarativeWebRequest' yêu cầu kênh Google Chrome beta hoặc mới hơn

Xem:

* [https://developer.chrome.com/extensions/event_pages](https://developer.chrome.com/extensions/event_pages)
* [https://developer.chrome.com/extensions/alarms#method-create](https://developer.chrome.com/extensions/alarms#method-create)

#### Lịch sử

Lấy lịch sử truy cập trang:

[https://developer.chrome.com/extensions/history#method-getVisits](https://developer.chrome.com/extensions/history#method-getVisits)

## 4. Câu hỏi?

**Hỏi**: Chúng ta có thể có **_cả_** `page_action` **_và_** `browser_action` không?

**Trả lời**: Không. Nhưng bạn có thể tạo nhiều tiện ích mở rộng và yêu cầu chúng giao tiếp với nhau

xem: [http://stackoverflow.com/questions/14519458/google-chrom-extension-browser-page-action](http://stackoverflow.com/questions/14519458/google-chrome-extension-browser-page-action)
và: [https://developer.chrome.com/extensions/extension#event-onMessageExternal](https://developer.chrome.com/extensions/extension#event-onMessageExternal)

**Hỏi**: Làm cách nào để kiểm tra khi Tab/Trang tải xong?
**Trả lời**: Thêm một event listener:

```js
chrome.tabs.onUpdated.addListener(function(tabId , info) {
    if (info.status == "complete") {
        // your code ...
    }});
```

[http://stackoverflow.com/questions/2149917/chrom-extensions-how-to-ledge-when-a-tab-as](http://stackoverflow.com/questions/2149917/chrome-extensions-how-to-know-when-a-tab-has-finished-loading-from-the-backgr)

## 5. Thông tin thêm

### Video

* Tiện ích mở rộng của Google Chrome: Cách xây dựng tiện ích mở rộng (chính thức của Nhà phát triển Google): [https://www.youtube.com/watch?v=e3McMaHvlBY](https://www.youtube.com/watch?v=e3McMaHvlBY) (từ năm 2009 nhưng tất cả thông tin vẫn hợp lệ)
* Xây dựng tiện ích mở rộng Chrome đầu tiên của bạn: [https://www.youtube.com/watch?v=pT-b2SpFIWo](https://www.youtube.com/watch?v=pT-b2SpFIWo)

### Hướng dẫn

* Bắt đầu: Xây dựng tiện ích mở rộng Chrome: [https://developer.chrome.com/extensions/getstarted](https://developer.chrome.com/extensions/getstarted)
* Cách tạo tiện ích mở rộng Chrome trong 10 phút: [http://www.sitepoint.com/create-chrom-extension-10-minutes-flat/](http://www.sitepoint.com/create-chrome-extension-10-minutes-flat/)
* Cách xây dựng tiện ích mở rộng Chrome: [http://lifehacker.com/5857721/how-to-build-a-chrom-extension](http://lifehacker.com/5857721/how-to-build-a-chrome-extension)
* Phát triển tiện ích mở rộng của Google Chrome: [http://code.tutsplus.com/tutorials/developing-google-chrom-extensions Nottnet-33076](http://code.tutsplus.com/tutorials/developing-google-chrome-extensions--net-33076)
* Xuất bản ứng dụng của bạn: [https://developer.chrome.com/webstore/publish](https://developer.chrome.com/webstore/publish)

### Bài viết

* Mọi thứ bạn cần biết về Tiện ích mở rộng trình duyệt: [http://www.howtogeek.com/169080/beginner-geek-everything-you-need-to-ledge-about-browser-extensions/](http://www.howtogeek.com/169080/beginner-geek-everything-you-need-to-know-about-browser-extensions/)
* Bao nhiêu phần trăm người dùng Internet sử dụng tiện ích mở rộng trình duyệt? [https://www.quora.com/What-percentage-of-INET-users-use-browser-extensions](https://www.quora.com/What-percentage-of-Internet-users-use-browser-extensions) trong năm 2010, 33% người dùng Chrome có tiện ích mở rộng. Tôi không thể tìm thấy dữ liệu gần đây hơn (vui lòng cập nhật nếu bạn tìm thấy số liệu thống kê gần đây)
* Xuất bản tiện ích mở rộng Chrome? 7 mẹo để tăng lượt tải về: [http://ecquire.com/blog/how-to-get-more-chrom-extension-doads/](http://ecquire.com/blog/how-to-get-more-chrome-extension-downloads/)
* Tiện ích mở rộng Chrome của bạn có thể đánh cắp thông tin cá nhân của bạn. Đây là cách ngăn chặn chúng: [http://digiwonk.wonderhowto.com/how-to/your-chrom-extensions-may-be-steals-your-personal-info-heres- stop-them-0150766 /](http://digiwonk.wonderhowto.com/how-to/your-chrome-extensions-may-be-stealing-your-personal-info-heres-stop-them-0150766/) (_Quyền riêng tư Lý do tôi không sử dụng bất kỳ tiện ích mở rộng nào_ )
* Cảnh báo: Tiện ích mở rộng trình duyệt của bạn đang theo dõi bạn: [http://www.howtogeek.com/180175/warning-your-browser-extensions-are-spying-on-you/](http://www.howtogeek.com/180175/warning-your-browser-extensions-are-spying-on-you/)
* Google Chrome Privacy Whitepaper: [https://www.google.co.uk/chrome/browser/privacy/whitepaper.html](https://www.google.co.uk/chrome/browser/privacy/whitepaper.html)
* Vậy, bạn muốn xây dựng tiện ích mở rộng chrome: [https://blog.hartleybrody.com/chrome-extension/](https://blog.hartleybrody.com/chrome-extension/) (_ví dụ_ BuzzKill của @hartleybrody)
* Ứng dụng Chrome là gì? [https://developer.chrome.com/apps/about_apps](https://developer.chrome.com/apps/about_apps) (_chúng thật tuyệt vời_ !)
* **_Gói ứng dụng Chrome cho iOS và Android bằng Cordova_**:[https://github.com/MobileChromeApps/mobile-chrome-apps](https://github.com/MobileChromeApps/mobile-chrome-apps) bạn có tò mò không? xem: [issues/598](https://github.com/MobileChromeApps/mobile-chrome-apps/issues/598)
* Đáng buồn thay, nhóm Chrome Android không thực hiện Tiện ích mở rộng Chrome cho thiết bị di động. xem: [https://www.reddit.com/r/Android/comments/35v8gi/we_are_the_chrome_for_android_team_ama/cr8alzk](https://www.reddit.com/r/Android/comments/35v8gi/we_are_the_chrome_for_android_team_ama/cr8alzk) _(có lẽ bởi vì nó sẽ cho phép chặn quảng cáo...)_
