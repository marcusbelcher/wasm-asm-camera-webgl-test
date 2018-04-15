
# README
This repo is a simple test case for anyone to use - as is - to check similar browser compatibility issues. Primarily tests cases for Webcam/Camera access via getUserMedia, HTTPS (as some browsers block camera access from unsecured sites), WebAssembly, ASM, and WebGL. 

Live example here: https://marcusbelcher.github.io/wasm-asm-camera-webgl-test/index.html

This repo is also used within an Android test application here: https://github.com/marcusbelcher/android-getUserMedia-test

## Build / Deploy
- Checkout this repo to the required host in a servable directory (e.g. `/var/www/html`)
- Start your server  (e.g. `http-server`, `httpd start`, etc)
- Go to the required URL in the browser you would like to test (e.g. `https://127.0.0.1:8080`)

## 3rd Parties
- https://github.com/webrtc/adapter (https://webrtc.github.io/adapter/adapter-latest.js) is packaged within the repo. 

# ISSUES
## iOS 
- <= 10
	- getUserMedia is not availible on iOS, thus all camera management must be done by the native iOS app.
- 11
	- Safari passes all tests and shows a live camera feed.
	- In-app webviews utilising SFSafariViewController, UIWebView, WKWebView do not currently support getUserMedia access
		- Thus any in-app browser - currently at the time of writing - does not support camera access. 
		- To get around this you can:
			- (Easy, poor UX) prompt the user to open the experience in Safari
			- (Hard, good UX) Implement bespoke camera access in the native iOS app and send/inject the stream into the webpage via the necessary bridging code.
- 12 (~ Sept 2018)
	- An educated 'gestimate' SFSafariViewController and WKWebView will get getUserMedia access in this update. UIWebView will not get getUserMedia. 

## Android
- 7.0
	- Chrome passes all tests and shows a live camera feed.
	- Firefox passes all tests and shows a live camera feed.
	- Edge passes all tests, receives a success message from getUserMedia however sometimes it does not show a live feed.
	- Facebook in-app WebView shows a `NotAllowedError - Permission denied`. 
	- Slacks in-app webview correctly runs the tests and shows a live camera feed (default app being Chrome, Samsung Internet). If Firefox/Edge are classed as the default app Slack opens the experience in the selected app vs running within its own web browser view.
	- Custom app (https://github.com/marcusbelcher/android-getUserMedia-test)
		- If permissions have been granted (Application settings) - all tests passed and live video should be seen
		- If permissions have not been granted I encounter a `NotReadableError - Could not start source` inside JavaScript. 
		The difference in errors between this app and Facebook will be down to WebView impementation and Application permissions. 

# Useful links
- https://github.com/webrtc/adapter (https://webrtc.github.io/adapter/adapter-latest.js) 
- https://www.webrtc-experiment.com/DetectRTC/
- https://stackoverflow.com/questions/48775154/notreadableerror-could-not-start-source
- https://github.com/googlesamples/android-PermissionRequest
- https://github.com/googlearchive/chromium-webview-samples/tree/master/webrtc-example
- https://bintray.com/package/readme/google/webrtc/google-webrtc
