# AndroidHttpCapture

AndroidHttpCapture is an Android network diagnostic and packet capture tool designed for mobile traffic debugging. It can be considered a mobile version of **Fiddler** for Android.

It supports on-device HTTP/HTTPS capture, HAR export, DNS/Ping/TraceRoute diagnostics, response modification, host configuration, WebView debugging, and system proxy capture for other apps.

> **Note**
> Before using AndroidHttpCapture, please make sure the phone’s existing HTTP proxy settings are disabled.

---

## Features

### 1. HTTP/HTTPS Capture

When users open a webpage through AndroidHttpCapture, all HTTP requests will be recorded. Captured packets can be previewed, shared, and uploaded.

The upload endpoint should be configured manually in `MainActivity`.

On first launch, users need to install the CA certificate in order to capture HTTPS traffic. The principle is the same as Fiddler: HTTPS traffic is captured through a MITM proxy.

If the certificate is not installed, HTTPS requests cannot be captured.

For newer Android versions, the app may not be able to open the certificate installation page automatically. In that case, please install the certificate manually:

```text
Settings -> Security & Lock Screen -> Encryption & Credentials -> Install Certificate
```

Certificate path:

```text
/har/littleproxy-mitm.pem
```

The preview page shows all network requests captured since the app started. It supports pagination, URL search, filtering, and clearing captured packets.

The captured data includes:

- Request Headers
- Request Cookies
- Request Body
- Response Headers
- Response Cookies
- Response Body

If the content is JSON, it will be automatically formatted for easier reading.

The share feature packages all captured packets into a HAR file and compresses it as a ZIP file, which can then be shared through apps such as WeChat, QQ, or other supported Android sharing targets.

---

### 2. Response Injection

AndroidHttpCapture supports modifying response traffic.

> Current limitation: this version only supports HTTP response modification.

---

### 3. Environment Switching

The app supports switching between different simulated environments, including:

- Normal browser
- WeChat
- QQ

The default environment is a normal browser.

---

### 4. Multiple Input Methods

AndroidHttpCapture supports multiple ways to open a target page:

- Navigation menu
- Address bar
- QR code scanning
- Schema launch

Schema format:

```text
jdhttpmonitor://webview?param={'url'='http://www.darkal.cn'}
```

---

### 5. Host Configuration

The app supports custom host configuration for specific domains.

This is useful for testing different backend environments or redirecting domain traffic during development.

---

### 6. Console Log Viewer

AndroidHttpCapture can display `console.log` output from the WebView page, making it easier to debug hybrid apps and mobile web pages.

---

### 7. Network Tools

AndroidHttpCapture includes several common network diagnostic tools, such as:

- DNS lookup
- Ping
- Device information

These tools help developers quickly diagnose network issues directly on the Android device.

---

### 8. System Proxy Capture

When the phone’s proxy server is set to:

```text
127.0.0.1:8888
```

AndroidHttpCapture can capture HTTP traffic from other apps, such as WeChat.

In this mode, AndroidHttpCapture works like a mobile Fiddler running directly on the phone.

> **Security Notice**
> Please only use this feature for debugging your own apps, test environments, or traffic that you are authorized to inspect.

---

## Demo APK

Demo APK download:

```text
Please add your APK download link here.
```

---

## User Guide

Operation manual:

```text
Please add your user guide link here.
```

---

## Q & A

### How can I view and analyze shared HTTP packets?

The shared file is a compressed ZIP file. After extracting it, you will get a `.har` file.

You can analyze the HAR file using Fiddler or an online HAR viewer.

#### Fiddler

Import the HAR file into Fiddler:

```text
Import Sessions -> Select Import Format -> HTTPArchive -> Select HAR file
```

#### Online HAR Viewer

You can also use an online HAR viewer:

```text
http://static.hk.darkal.cn/har/
```

Drag the HAR file into the tool to analyze it.

---

## Known Issues

1. The app currently trusts all server certificates without validation.
2. When response injection is enabled, some HTTPS pages may encounter:

```text
ERR_CONTENT_LENGTH_MISMATCH
```

This issue appears to have been improved, but more user feedback is needed.

---

## Implementation

AndroidHttpCapture is built on top of **Netty** and **browsermob-proxy**.

### Netty

Netty is an asynchronous event-driven network application framework for rapid development of maintainable, high-performance protocol servers and clients.

Project link:

```text
https://github.com/netty/netty
```

Because Android 5.0+ does not support certificates with the `JKS` provider, part of Netty’s certificate implementation was reverse-modified to adapt it to Android.

The modified library is:

```text
netty_android.jar
```

### browsermob-proxy

browsermob-proxy is a free utility that helps web developers watch and manipulate network traffic from AJAX applications.

Project link:

```text
https://github.com/lightbody/browsermob-proxy
```

Several parts of browsermob-proxy were modified to make it compatible with Android.

---

## Contributing

Contributions are welcome.

If you find this project useful, please consider:

- Starring the repository
- Reporting bugs
- Submitting pull requests
- Improving documentation
- Sharing feedback

---

## Support

If you like this project and want to support its development, you can buy me a coffee.

```text
Please add your donation QR code or support link here.
```

---

## Disclaimer

AndroidHttpCapture is intended for legitimate development, debugging, testing, QA, and educational purposes.

Do not use this tool to capture, inspect, modify, or distribute network traffic without proper authorization. The author is not responsible for any misuse of this software.

---

## License

MIT License

Copyright (c) 2016 AndroidHttpCapture

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files, to deal in the Software
without restriction, including without limitation the rights to use, copy,
modify, merge, publish, distribute, sublicense, and/or sell copies of the
Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
