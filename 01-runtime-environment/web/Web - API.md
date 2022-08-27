
```
[WebAPI]

	: https://developer.mozilla.org/en-US/docs/Web/API
  
  : https://developer.mozilla.org/en-US/docs/Web/API/History_API

```

    Web编程时，浏览器端提供的API接口。Web API 通常与 JS在一起使用，然而也并非总是如此。

### Window

```
[Window]

	: 表示一个包含DOM文档的窗口, document 属性指向窗口中载入的 DOM文档
  # window作为全局变量，代表了脚本正在运行的窗口，暴露给 Javascript 代码
  # window 对象实现了 Window 接口，此接口继承自 AbstractView 接口
  # 有标签页功能的浏览器中, 每个标签都拥有自己的 window 对象

	: https://developer.mozilla.org/zh-CN/docs/Web/API/Window

[属性]

	: 该接口从 EventTarget、WindowOrWorkerGlobalScope 和 WindowEventHandlers 继承属性

	# 这个属性指示当前窗口是否关闭
	: Window.closed  只读

	# 返回 console 对象的引用，该对象提供了对浏览器调试控制台的访问。
	: Window.console 只读

	# 返回对当前窗口所包含文档的引用
	: Window.document 只读

	# Returns the current event, which is the event currently being handled by the JavaScript code's context, or undefined if no event is currently being handled. The Event object passed directly to event handlers should be used instead whenever possible.
	: Window.event 只读

	# 返回一个对 history 对象的引用
	: Window.history 只读

	# 获得浏览器窗口的内容区域的高度，包含水平滚动条(如果有的话)
	: Window.innerHeight 只读

	# 获得浏览器窗口的内容区域的宽度，包含垂直滚动条(如果有的话)
	: Window.innerWidth 只读
 
 	# 返回窗口中的 frames 数量。参见 window.frames。
	: Window.length 只读

	# 获取、设置 window 对象的 location, 或者当前的 URL.
	: Window.location

	# 获取/设置窗口的名称
	: Window.name
  
  # 返回对 navigator 对象的引用
	: Window.navigator 只读
  
	# 返回浏览器窗口的外部高度
	: Window.outerHeight 只读

	# 返回浏览器窗口的外部宽度
	: Window.outerWidth 只读

	# Returns a reference to the screen object associated with the window.
	: Window.screen 只读

	# Both properties return the horizontal distance from the left border of the user's browser viewport to the left side of the screen.
	: Window.screenX and Window.screenLeft 只读

	# Both properties return the vertical distance from the top border of the user's browser viewport to the top side of the screen.
	: Window.screenY and Window.screenTop 只读

	# window.scrollX的别名
	: Window.pageXOffset 只读

	# window.scrollY的别名
	: Window.pageYOffset 只读
  
  	# Returns the scrollbars object, whose visibility can be toggled in the window.
	: Window.scrollbars 只读

	# The maximum offset that the window can be scrolled to horizontally, that is the document width minus the viewport width.
	: Window.scrollMaxX  只读

	# The maximum offset that the window can be scrolled to vertically (i.e., the document height minus the viewport height).
	: Window.scrollMaxY  只读

	# Returns the number of pixels that the document has already been scrolled horizontally.
	: Window.scrollX 只读

	# Returns the number of pixels that the document has already been scrolled vertically.
	: Window.scrollY 只读

	# 返回当前窗口或子窗口的父窗口的引用
	: Window.parent 只读

------------------------------------------------------------------------------------------

	# 返回当前 window 的 content 元素的引用。通过带下划线的过时变种方法不再可以获得 Web content
	: Window.content 和 Window._content   只读

	# 返回当前 chrome window 的 XUL 控制器对象
	: Window.controllers  只读

	# returns a reference to the CustomElementRegistry object, which can be used to register new custom elements and get information about previously registered custom elements.
	: Window.customElements 只读

	# 返回浏览器 crypto 对象
	: Window.crypto 只读

	# 获取或设置指定窗口的状态栏文本
	: Window.defaultStatus 已废弃 Gecko 23

	# 返回当前显示器的物理像素和设备独立像素的比例
	: Window.devicePixelRatio  只读

	# 获取在调用 window.showModalDialog() 时传递给窗口的参数（如果它是一个对话框）。这是一个 nsIArray
	: Window.dialogArguments 只读

	# window.personalbar 的另一种形式
	: Window.directories 

	# Returns a reference to a DOMMatrix object, which represents 4x4 matrices, suitable for 2D and 3D operations.
	: Window.DOMMatrix 只读 

	# Returns a reference to a DOMMatrixReadOnly object, which represents 4x4 matrices, suitable for 2D and 3D operations.
	: Window.DOMMatrixReadOnly 只读 

	# Returns a reference to a DOMPoint object, which represents a 2D or 3D point in a coordinate system.
	: Window.DOMPoint 只读 

	# Returns a reference to a DOMPointReadOnly object, which represents a 2D or 3D point in a coordinate system.
	: Window.DOMPointReadOnly 只读 

	# Returns a reference to a DOMQuad object, which provides represents a quadrilaterial object, that is one having four corners and four sides.
	: Window.DOMQuad 只读 

	# Returns a reference to a DOMRect object, which represents a rectangle.
	: Window.DOMRect 只读 

	# Returns a reference to a DOMRectReadOnly object, which represents a rectangle.
	: Window.DOMRectReadOnly 只读 

	# 返回嵌入窗口的元素，如果未嵌入窗口，则返回null
	: Window.frameElement 只读

	# 返回当前窗口中所有子窗体的数组
	: Window.frames 只读

	# 此属性表示窗口是否以全屏显示
	: Window.fullScreen

	# Gecko 13 (Firefox 13) 开始废弃。使用 Window.localStorage 替代它
  # 原本是：用于存储跨页面数据的多重存储对象
	: Window.globalStorage  已废弃 Gecko 13

	# 指出上下文环境是否能够使用安全上下文环境的特征
	: Window.isSecureContext  只读

	# 返回 locationbar 对象，其可视性可以在窗口中切换
	: Window.locationbar 只读

	# 返回用来存储只能在创建它的源下访问的数据的本地存储对象的引用
	: Window.localStorage 只读

	# 返回菜单条对象，它的可视性可以在窗口中切换
	: Window.menubar 只读

	# 返回窗口的 message manager 对象
	: Window.messageManager

	# 返回当前动画循环开始经过的毫秒数
	: Window.mozAnimationStartTime 只读 

	# Returns the horizontal (X) coordinate of the top-left corner of the window's viewport, in screen coordinates. This value is reported in CSS pixels. See mozScreenPixelsPerCSSPixel in nsIDOMWindowUtils for a conversion factor to adapt to screen pixels if needed.
	: Window.mozInnerScreenX 只读 

	# Returns the vertical (Y) coordinate of the top-left corner of the window's viewport, in screen coordinates. This value is reported in CSS pixels. See mozScreenPixelsPerCSSPixel for a conversion factor to adapt to screen pixels if needed.
	: Window.mozInnerScreenY 只读 

	# Returns the number of times the current document has been rendered to the screen in this window. This can be used to compute rendering performance.
	: Window.mozPaintCount  只读

	# 返回对打开当前窗口的那个窗口的引用
	: Window.opener

	# Returns the orientation in degrees (in 90 degree increments) of the viewport relative to the device's natural orientation.
	: Window.orientation   只读

	# Returns a Performance object, which includes the timing and navigation attributes, each of which is an object providing performance-related data. See also Using Navigation Timing for additional information and examples.
	: Window.performance 只读

	# 返回 personalbar 对象，它的可视性可以在窗口中切换
	: Window.personalbar 只读

	# Formerly provided access to install and remove PKCS11 modules.
	: Window.pkcs11 已废弃 Gecko 29

	# The return value to be returned to the function that called window.showModalDialog() to display the window as a modal dialog.
	: Window.returnValue

	# Returns an object reference to the window object itself.
	: Window.self 只读

	# Returns a reference to the session storage object used to store data that may only be accessed by the origin that created it.
	: Window.sessionStorage

	# Returns a reference to the window object of the sidebar.
	: Window.sidebar  只读

	# Returns a SpeechSynthesis object, which is the entry point into using Web Speech API speech synthesis functionality.
	: Window.speechSynthesis 只读

	# Gets/sets the text in the statusbar at the bottom of the browser.
	: Window.status

	# Returns the statusbar object, whose visibility can be toggled in the window.
	: Window.statusbar 只读

	# Returns the toolbar object, whose visibility can be toggled in the window.
	: Window.toolbar 只读

	# Returns a reference to the topmost window in the window hierarchy. This property is read only.
	: Window.top 只读

	# Returns a VisualViewport object which represents the visual viewport for a given window.
	: Window.visualViewport 只读

	# Returns a reference to the current window.
	: Window.window 只读

	# Returns a reference to the window object in the frames. See Window.frames for more details.
	: window[0], window[1], etc.

[方法]

	: 该接口从 EventTarget、WindowOrWorkerGlobalScope  继承方法

	# Displays an alert dialog.
	: Window.alert()

	# Moves back one in the window history. This method is obsolete; you should instead use window.history.back().
	: Window.back()  

	# Closes the current window.
	: Window.close()

	# Displays a dialog with a message that the user needs to respond to.
	: Window.confirm()

	# Opens a new window.
	: Window.open()

	# Opens a new dialog window.
	: Window.openDialog()

	# This method stops window loading.
	: Window.stop()
 
------------------------------------------------------------------------------------------

	# Sets focus away from the window.
	: Window.blur()

	# Enables you to cancel a callback previously scheduled with Window.requestAnimationFrame.
	: Window.cancelAnimationFrame() 

	# Enables you to cancel a callback previously scheduled with Window.requestIdleCallback.
	: Window.cancelIdleCallback() 

	# Registers the window to capture all events of the specified type.
	: Window.captureEvents() 

	# Cancels the repeated execution set using setImmediate.
	: Window.clearImmediate()

	# FIXME: NeedsContents
	: Window.disableExternalCapture() 已废弃 Gecko 24

	# Used to trigger an event.
	: Window.dispatchEvent()

	# Writes a message to the console.
	: Window.dump() 

	# FIXME: NeedsContents
	: Window.enableExternalCapture() 已废弃 Gecko 24

	# Searches for a given string in a window.
	: Window.find()

	# Sets focus on the current window.
	: Window.focus()

	# Moves the window one document forward in the history. This method is obsolete; you should instead use window.history.forward().
	: Window.forward()  

	# Flashes the application icon.
	: Window.getAttention()  

	# FIXME: NeedsContents
	: Window.getAttentionWithCycleCount()

	# Gets computed style for the specified element. Computed style indicates the computed values of all CSS properties of the element.
	: Window.getComputedStyle()

	# Gets default computed style for the specified element, ignoring author stylesheets.
	: Window.getDefaultComputedStyle() 

	# Returns the selection object representing the selected item(s).
	: Window.getSelection()

	# Returns the browser to the home page.
	: Window.home()  

	# Returns a MediaQueryList object representing the specified media query string.
	: Window.matchMedia()

	# FIXME: NeedsContents
	: Window.maximize()

	# Minimizes the window.
	: Window.minimize() (top-level XUL windows only)

	# Moves the current window by a specified amount.
	: Window.moveBy()

	# Moves the window to the specified coordinates.
	: Window.moveTo()

	# Provides a secure means for one window to send a string of data to another window, which need not be within the same domain as the first.
	: Window.postMessage()

	# Opens the Print Dialog to print the current document.
	: Window.print()

	# Returns the text entered by the user in a prompt dialog.
	: Window.prompt()

	# Releases the window from trapping events of a specific type.
	: Window.releaseEvents()  

	# Tells the browser that an animation is in progress, requesting that the browser schedule a repaint of the window for the next animation frame.
	: Window.requestAnimationFrame()

	# Enables the scheduling of tasks during a browser's idle periods.
	: Window.requestIdleCallback() 

	# Resizes the current window by a certain amount.
	: Window.resizeBy()

	# Dynamically resizes window.
	: Window.resizeTo()

	# FIXME: NeedsContents
	: Window.restore()  

	# FIXME: NeedsContents
	: Window.routeEvent() 已废弃 Gecko 24

	# Scrolls the window to a particular place in the document.
	: Window.scroll()

	# Scrolls the document in the window by the given amount.
	: Window.scrollBy()

	# Scrolls the document by the given number of lines.
	: Window.scrollByLines() 

	# Scrolls the current document by the specified number of pages.
	: Window.scrollByPages() 

	# Scrolls to a particular set of coordinates in the document.
	: Window.scrollTo()

	# Changes the cursor for the current window
	: Window.setCursor()  (top-level XUL windows only)

	# Executes a function after the browser has finished other heavy tasks
	：Window.setImmediate()

	# Toggles a user's ability to resize a window.
	: Window.setResizable() 

	# Sizes the window according to its content.
	: Window.sizeToContent() 

	# Updates the state of commands of the current chrome window (UI).
	: Window.updateCommands() 

```

### Location

```
[Location]

	: 表示其链接到的对象的位置(URL, 所做的修改反映在与之相关的对象上
  # Document (Document.location) 和 Window (Window.location) 

	: https://developer.mozilla.org/zh-CN/docs/Web/API/Location

[属性]

	: Location 接口不继承任何属性，但是实现了那些来自 URLUtils 的属性

	# 包含整个URL的一个DOMString
	: Location.href

	# 包含URL对应协议的一个DOMString, 最后有一个":"
	: Location.protocol

	# 包含了域名的一个DOMString，可能在该串最后带有一个":"并跟上URL的端口号
	: Location.host

	# 包含URL域名的一个DOMString
	: Location.hostname

	# 包含端口号的一个DOMString
	: Location.port

	# 包含URL中路径部分的一个DOMString，开头有一个“/"
	: Location.pathname

	# 包含URL参数的一个DOMString，开头有一个“?”
	: Location.search

	# 包含块标识符的DOMString，开头有一个“#”
	: Location.hash

	# 包含URL中域名前的用户名的一个DOMString
	: Location.username

	# 包含URL域名前的密码的一个 DOMString
	: Location.password

	# 包含页面来源的域名的标准形式DOMString (只读)
	: Location.origin 

[方法]

	: Location没有继承任何方法，但实现了来自URLUtils的方法

	# 加载给定URL的内容资源到这个Location对象所关联的对象上
	: Location.assign()

	# 重新加载来自当前 URL的资源
  # 有一个特殊的可选参数, 类型 Boolean 为true时会导致该方法引发的刷新一定会从服务器上加载数据
  # 如果是 false或没有制定这个参数, 浏览器可能从缓存当中加载页面
	: Location.reload()

	# 用给定的URL替换掉当前的资源
  # 与 assign() 方法不同的是用 replace()替换的新页面不会被保存在会话的历史 History中
  # 这意味着用户将不能用后退按钮转到该页面
	: Location.replace()

	# 返回一个DOMString, 包含整个URL
  # 它和读取URLUtils.href的效果相同。但是用它是不能够修改Location的值的
	: Location.toString()

[常用方法]
 
	# 实现页面加载方法, assign 方法有历史记录, replace 方法没有历史记录, 不能实现后退操作
	: Location.assign() 、Location.replace()

```

### History

```
[History]

	: 允许操作浏览器的曾经在标签页或者框架里访问的会话历史记录

	: https://developer.mozilla.org/zh-CN/docs/Web/API/History

[属性]

	: History 接口不继承于任何属性

	# 返回一个整数, 该整数表示会话历史中元素的数目, 包括当前加载的页 (只读)
	: History.length 只读

//	# 返回一个代表session历史记录中活动的项目URL的DOMString
//  # 这个属性永远对web内容不可用并且已经不再被任何浏览器支持。可以使用Location.href来代替它
//	: History.current (只读, 已废弃 Gecko 26)

//	# 返回一个代表session历史记录中后一个项目URL的DOMString
//  # 这个属性永远对web内容不可用并且不被其他浏览器支持
//	: History.next (只读, 已废弃 Gecko 26)

//	# 返回一个代表session历史记录中前一个项目URL的DOMString
//  # 这个属性永远对web内容不可用并且不被其他浏览器支持
//	: History.previous (只读, 已废弃 Gecko 26)

	# 允许Web应用程序在历史导航上显式地设置默认滚动恢复行为
  # 此属性可以是自动的（auto）或者手动的（manual）
	: History.scrollRestoration 

	# 返回一个表示历史堆栈顶部的状态的值, 这是一种可以不必等待popstate事件而查看状态而的方式
	: History.state (只读)

[方法]

	: History接口不继承任何方法

	# 前往上一页, 用户可点击浏览器左上角的返回按钮模拟此方法. 等价于 history.go(-1)
  # Note: 当浏览器会话历史记录处于第一页时调用此方法没有效果，而且也不会报错
	: History.back()

	# 浏览器历史记录里前往下一页, 可点击浏览器左上角的前进按钮模拟此方法, 等价于 history.go(1)
  # Note: 当浏览器历史栈处于最顶端时( 当前页面处于最后一页时 )调用此方法没有效果也不报错
	: History.forward()

	# 通过当前页面的相对位置从浏览器历史记录( 会话记录 )加载页面
  # 参数为-1的时候为上一页，参数为1的时候为下一页. 当整数参数超出界限时没有任何效果也不会报错。
  # 调用没有参数的 go() 方法或者不是整数的参数时也没有效果
	: History.go()


	# 按指定的名称和URL（如果提供该参数）将数据push进会话历史栈, 数据被DOM进行不透明处理
  # 可以指定任何可以被序列化的javascript对象
	: History.pushState()

	# 按指定的数据，名称和URL(如果提供该参数)，更新历史栈上最新的入口
  # 这个数据被DOM 进行了不透明处理。你可以指定任何可以被序列化的javascript对象
	: History.replaceState()

[常用方法]

	# H5新接口, 可以做到改变网址却不需要刷新页面, 这个特性后来用到了单页面应用中
	: History.pushState() 、 History.replaceState()

```

### Navigator

```
[Navigator]

	: 表示用户代理的状态和标识, 它允许脚本查询它和注册自己进行一些活动。

	: https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator

[属性]

	: NavigatorID, NavigatorLanguage, NavigatorOnLine, NavigatorGeolocation,
  NavigatorPlugins, NavigatorUserMedia, NetworkInformation
  未从其中继承任何属性, 但实现了部分属性

	# 筛选所有的 VRDisplay 对象, 数组的形式返回, 所有VRDisplay.ispresenting 属性的值为true的对象
	: Navigator.activeVRDisplays 只读

	# 返回当前浏览器的内部“开发代号”名称。 不能保证此属性返回的值是正确的
	: NavigatorID.appCodeName 只读

	# 以 DOMString 的形式返回浏览器官方名称。 不能保证此属性返回的值是正确的
	: NavigatorID.appName 只读

	# 以 DOMString 的形式返回浏览器版本。不能保证此属性返回的值是正确的
	: NavigatorID.appVersion 只读

	# 返回一个 BatteryManager 对象，你可以用它来获取一些电池充电状态的信息
	: Navigator.battery 只读

	# 提供一个NetworkInformation对象来获取设备的网络连接信息
	: Navigator.connection 只读

	# 当忽略 cookie 时返回 false，否则返回 true
	: Navigator.cookieEnabled 只读

	# 返回一个 Geolocation 对象，据之可访问设备的地理位位置信息。
	: Navigator.geolocation 只读

	# Returns the number of logical processor cores available.
	: NavigatorConcurrentHardware.hardwareConcurrency 只读

	# 返回Boolean表明浏览器是否支持Java
	: NavigatorPlugins.javaEnabled 只读

	# Returns a Keyboard object which provides access to functions that retrieve keyboard layout maps and toggle capturing of key presses from the physical keyboard.
	: Navigator.keyboard 只读

	# 返回DOMString表示用户的首先语言，通常是浏览器用户界面的语言。当未知的时，返回null
	: NavigatorLanguage.language 只读

	# 返回一个表示用户已知语言的DOMString数组，并按优先顺序排列
	: NavigatorLanguage.languages 只读

	: NavigatorPlugins.mimeTypes 只读

	# Returns a LockManager object which provides methods for requesting a new Lock object and querying for an existing Lock object
	: Navigator.locks 只读

	# Returns a MediaCapabilities object that can expose information about the decoding and encoding capabilities for a given format and output capabilities.
	: Navigator.mediaCapabilities 只读

	# Returns the maximum number of simultaneous touch contact points are supported by the current device.
	# 回MimeTypeArray数组用于列举浏览器所支持的MIME类型
  : Navigator.maxTouchPoints 只读

	# 返回Boolean来表明浏览器是否联网
	: NavigatorOnLine.onLine 只读

	# 返回当前操作系统名
	: Navigator.oscpu

	# Returns a Permissions object that can be used to query and update permission status of APIs covered by the Permissions API.
	: Navigator.permissions 只读

	# 返回浏览器平台名，不确定此值是否有效
	: NavigatorID.platform 只读

	# 返回PluginArray数组用于列举出浏览器安装的插件
	: NavigatorPlugins.plugins 只读

	# 在任意浏览器下都只返回'Gecko'，此属性只用于兼容的目的
	: NavigatorID.product 只读 

	# 返回ServiceWorkerContainer 对象用于提供注册、删除、更新以及为了associated document的ServiceWorker对象之间的通信。
	: Navigator.serviceWorker 只读

	# Returns the singleton StorageManager object used for managing persistence permissions and estimating available storage on a site-by-site/app-by-app basis.
	: NavigatorStorage.storage 只读

	# 返回当前浏览器的用户代理
	: NavigatorID.userAgent 只读

	: Navigator.webdriver 只读 

[非标准方法]

	# 返回浏览器识别码 (e.g., "2006090803").
	: navigator.buildID 

	# 返回布尔值以表明cookies是否能再浏览器中启用
	: Navigator.cookieEnabled 

	# 报告用户的不追踪参数值，当值为yes，你的网址或应用将不追踪用户
	: navigator.doNotTrack 

	# 返回 id 对象， 你能用 BrowserID 添加支持 到你的网址
	: navigator.id

	# Returns an Apps object you can use to install, manage, and control Open Web apps.
	: navigator.mozApps 

	# The navigator.mozAudioChannelManager object provides access to the mozAudioChannelManager interface, which is used to manage your Firefox OS device's audio channels, including setting what channel's volume to affect when the volume buttons are pressed inside a particular app.
	: navigator.mozAudioChannelManager 

	: navigator.mozNotification 已废弃 Gecko 22

	# Returns a notification object you can use to deliver notifications to the user from your web application.
	: navigator.webkitNotification

	# The Object, returned by the navigator.mozSocial property, is available within the social media provider's panel to provide functionality it may need.
	: navigator.mozSocial 

	# Returns the build number of the current browser (e.g., "20060909").
	: navigator.productSub 

	# Returns an empty string. In Netscape 4.7x, returns "US & CA domestic policy" or "Export policy".
	: navigator.securitypolicy 

	# Returns a boolean indicating whether the browser is running in standalone mode. Available on Apple's iOS Safari only.
	: navigator.standalone 

	# Returns the vendor name of the current browser (e.g., "Netscape6").
	: navigator.vendor 

	# Returns the vendor version number (e.g. "6.1").
	: navigator.vendorSub 

	# Returns a PointerLock object for the Mouse Lock API.
	: navigator.webkitPointer 

[标准方法]

	# Returns a promise that resolves to an array of VRDisplay objects representing any available VR devices connected to the computer.
	: Navigator.getVRDisplays() 

	# After having prompted the user for permission, returns the audio or video stream associated to a camera or microphone on the local computer.
	: NavigatorUserMedia.getUserMedia()

	# Allows web sites to register themselves as a possible handler for a given MIME type.
	: navigator.registerContentHandler

	# Allows web sites to register themselves as a possible handler for a given protocol.
	: navigator.registerProtocolHandler

	# Returns a Promise for a MediaKeySystemAccess object.
	: Navigator.requestMediaKeySystemAccess() 

	# Used to asynchronously transfer a small amount of data using HTTP from the User Agent to a web server.
	: Navigator.sendBeacon()

	# Invokes the native sharing mechanism of the current platform.
	: Navigator.share()

	# Returns false. JavaScript taint/untaint functions removed in JavaScript 1.2.
	: NavigatorID.taintEnabled() 已废弃 Gecko 1.7.8 已废弃 Gecko 9.0 

	# Causes vibration on devices with support for it. Does nothing if vibration support isn't available.
	: Navigator.vibrate()

```

### Screen

```
[Screen]

	: 表示一个屏幕窗口，往往指的是当前正在被渲染的window对象
  由浏览器决定提供屏幕对象，此对象一般通过当前浏览器窗口活动状态动态检测来得到

	: https://developer.mozilla.org/zh-CN/docs/Web/API/Screen

[属性]

	# Specifies the y-coordinate of the first pixel that is not allocated to permanent or semipermanent user interface features.
	: Screen.availTop

	# 返回屏幕左边边界的第一个像素点
	: Screen.availLeft

	# Specifies the height of the screen, in pixels, minus permanent or semipermanent user interface features displayed by the operating system, such as the Taskbar on Windows.
	: Screen.availHeight

	# 返回窗口中水平方向可用空间的像素值
	: Screen.availWidth

	# 返回屏幕的色彩深度
	: Screen.colorDepth

	# 以像素为单位返回屏幕的高度
	: Screen.height

	# 返回从最左边界到当前屏幕的像素值
	: Screen.left

	# 返回当前屏幕的转向
	: Screen.orientation

	# 获取屏幕的像素点
	: Screen.pixelDepth

	# 返回最上边界到当前屏幕的像素值
	: Screen.top

	# 返回屏幕的宽度
	: Screen.width

  # 布尔值。如果设置为false讲关闭设备的屏幕
	: Screen.mozEnabled

	# 控制设备屏幕的亮度。期望参数是0-1.0之间的浮点数
	: Screen.mozBrightness

[方法]

	# 锁定屏幕转向(仅在全屏或者已安装的APP中生效)
	: Screen.lockOrientation

	# 解锁屏幕转向(仅在全屏或者已安装的APP中生效), 方法继承于 EventTarget
	: Screen.unlockOrientation

	# Registers an event handler of a specific event type on the EventTarget.
	: EventTarget.addEventListener()

	# Removes an event listener from the EventTarget.
	: EventTarget.removeEventListener()

	# Dispatches an event to this EventTarget.
	: EventTarget.dispatchEvent()

```

