# Uploading Apps (Android vs iOS)

To run autonomous mobile tests with Rova, you first need to give the AI agent access to your mobile application.

To open the uploader, simply navigate to the Apps page in your dashboard and click the Upload App button.

### Upload Methods

Rova offers two simple ways to get your app binary into the cloud environment:

#### 1. File Upload (Direct Drag & Drop)

If you have the build file sitting on your computer, this is the quickest way to get started.

* Supported Formats: `.apk` (Android) or `.ipa` (iOS) files.
* Size Limit: You can upload builds up to 1000MB (1GB).
* How to use: Drag and drop your file directly into the modal or click to browse your local folders.

<figure><img src="../../.gitbook/assets/ROVA-AI-Autonomous-Mobile-Testing-07-17-2026_09_14_AM.png" alt="A dark-themed modal window titled &#x22;Upload App&#x22; with the &#x22;File Upload&#x22; tab selected. It features a dashed drag-and-drop area containing a cloud icon and the text &#x22;Drag &#x26; drop your APK or IPA file here or click to browse&#x22;. Below the drop area, it notes a &#x22;Maximum file size: 1000MB&#x22;. &#x22;Cancel&#x22; and &#x22;Upload&#x22; buttons are positioned in the bottom right corner." width="458"><figcaption></figcaption></figure>

#### 2. URL Upload (Direct Link)

If your app is built automatically through a CI/CD pipeline, you can bypass downloading it locally by pointing Rova to a hosted file.

* Platform Selection: Explicitly select whether the URL points to an Android or iOS binary.
* App URL: Provide a direct, publicly accessible download link to your app (e.g., from your GitHub releases, AWS S3 buckets, Bitrise artifacts, or other CI/CD storage).
* _Note: Ensure the link is a direct download link and does not require authentication or passcodes to access._

<figure><img src="../../.gitbook/assets/ROVA-AI-Autonomous-Mobile-Testing-07-17-2026_09_16_AM.png" alt="A dark-themed modal window titled &#x22;Upload App&#x22; with the &#x22;URL Upload&#x22; tab selected. It shows a &#x22;Platform&#x22; selection section with &#x22;Android&#x22; (selected, showing a robot emoji) and &#x22;iOS&#x22; (showing an apple emoji) buttons. Underneath, there is an &#x22;App URL&#x22; input field with the placeholder text &#x22;https://example.com/app.apk&#x22; and an instruction to &#x22;Enter a direct public download link to your app (e.g., from GitHub releases, CI/CD artifacts)&#x22;. &#x22;Cancel&#x22; and &#x22;Upload&#x22; buttons are in the bottom right corner." width="452"><figcaption></figcaption></figure>

### Platform Requirements: Android vs. iOS

To ensure your tests run smoothly on Rova's cloud-hosted devices, make sure your build files match these specifications:

#### Android (`.apk`)

* Format: Upload a standard `.apk` build file.
* Build Type: We highly recommend uploading a Debug build (or a release build that has debugging symbols/accessibility labels enabled). This makes it easier for Rova's AI to interact with and understand your app's element hierarchy.

#### iOS (`.ipa`)

* Format: Upload a packaged `.ipa` build file.
* Signing: Ensure your `.ipa` is signed with an appropriate provisioning profile (such as an Ad-Hoc or Enterprise distribution profile) that allows it to run on virtual or real mobile devices in a cloud environment.

### Best Practices

* Keep Accessibility Labels Intact: Rova's AI performs best when you use native UI components with clear accessibility identifiers (like `accessibilityIdentifier` in iOS and `contentDescription` in Android).
* Automate with URL Uploads: Instead of manually uploading a new build every time your team writes code, set up your CI/CD tool to ping Rova's API keys with the latest build URL.
