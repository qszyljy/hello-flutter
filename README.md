# Hello Flutter

最小的 Flutter 示例：一个页面，点右下角「加一」数字 +1。零第三方依赖。

代码全在 `lib/main.dart`，约 45 行。`android/`、`ios/` 那几百个文件由
`flutter create` 生成，所以仓库里不放。

---

## 方式 A：云端编译，手机直接下载安装（不需要电脑）

### 1. 推到 GitHub

新建一个空仓库，把本目录三个东西传上去：

- `pubspec.yaml`
- `lib/main.dart`
- `.github/workflows/build-apk.yml`

手机浏览器在 GitHub 上点 **Add file → Create new file**，文件名直接填
`.github/workflows/build-apk.yml`（斜杠会自动建目录），粘贴内容即可。

### 2. 编译

仓库页 **Actions → build-apk → Run workflow**，等 3～5 分钟。
产物在本次运行页底部的 **Artifacts → hello-flutter-apk.zip**（要解压）。

### 3. 更省事的下载方式

仓库页 **Releases → Draft a new release**，Tag 随便填 `v1`，发布。
workflow 会自动把 APK 挂成 `hello-flutter.apk`，手机点链接直接下载，
不用解压。

### 4. 安装

下载后点开，第一次会拦「不允许安装未知应用」——去设置里对这个浏览器
开启「允许安装」，再回来点一次就行。

APK 用 debug 签名，自己装没问题，传不了 Google Play。

---

## 方式 B：电脑上编译

1. 装 Flutter SDK（<https://docs.flutter.dev/get-started/install>），国内加镜像：
   ```bash
   export PUB_HOSTED_URL=https://pub.flutter-io.cn
   export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
   ```
2. 生成平台工程（`src` 指本仓库目录）：
   ```bash
   flutter create hello_flutter
   cp src/pubspec.yaml  hello_flutter/pubspec.yaml
   cp src/lib/main.dart hello_flutter/lib/main.dart
   ```
3. 跑 / 打包：
   ```bash
   cd hello_flutter
   flutter run                   # 接手机或模拟器
   flutter run -d chrome         # 看网页版，不用 Android SDK
   flutter build apk --release   # 产物 build/app/outputs/flutter-apk/
   ```
4. 传到手机（三种任选）：
   - **数据线**：手机选「传输文件」，拷到 `Download/` 后点开安装
   - **同一 WiFi**：电脑 `python3 -m http.server 8000`，手机浏览器开
     `http://电脑IP:8000/` 下载
   - **微信/QQ**：微信会拦 apk，先改名成 `.apk.1` 发过去再改回来

---

## 改点什么

- 标题：`main.dart` 里两处 `'Hello Flutter'`
- 主题色：`colorSchemeSeed: Colors.indigo` → `Colors.teal` 之类
- 按钮文字：`'加一'`
- 数字样式：`textTheme.displayMedium`
