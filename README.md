# 小羊记账 · 安卓 App 工程

把你的网页记账系统（奶茶分类 + PIN 门禁 + Gitee 同步）打包成了标准 **Capacitor 安卓原生工程**，可以用 **Android Studio 一键构建并装到手机**。

> ⚠️ iOS 版无法在这台 Windows 上制作（必须 macOS + Xcode + 付费开发者账号）。本工程只含安卓。

---

## 一、工程位置
```
C:\Users\Administrator\Desktop\记账App\
├─ www\                 网页资源（记账页面，已含奶茶分类/PIN门禁）
├─ android\             安卓原生工程（用 Android Studio 打开这个目录）
├─ capacitor.config.json
└─ package.json
```

## 二、在你电脑上怎么装到手机（3 步）
前置：安装 **Android Studio**（免费，https://developer.android.com/studio），首次打开会提示下载 SDK，按引导装好即可（需联网）。

1. **打开工程**
   Android Studio 启动界面 → `Open` → 选择 `C:\Users\Administrator\Desktop\记账App\android` → 等待 Gradle 同步完成（首次会联网下载 Gradle，稍慢）。

2. **连手机 或 开模拟器**
   - 真机：手机设置 → 关于本机 → 连点「版本号」7 次开启开发者模式 → 打开「USB 调试」→ 数据线连电脑，手机点「允许」。
   - 或：顶部工具栏 `Device Manager` → 新建一个模拟器（选任意机型）→ 启动。

3. **点 Run 装到手机**
   顶部绿色 ▶（Run，或 `Shift+F10`）→ 选择你的设备 → 手机上自动安装并打开「小羊记账」。

> 想导出可分享的 APK 安装包：`Build` 菜单 → `Build APK(s)` → 完成后右下角通知点 `locate` 拿到 `app-debug.apk`，发给别人直接装。

---

## 三、App 里已经有什么
- ✅ **奶茶独立分类**（41 条已从餐饮分离，饼图/统计单独算）
- ✅ **PIN 门禁**（打开要输 `521412`，每次刷新都要求输入）
- ✅ **Gitee 同步**：首次打开后在 App 右上角 ⚙ → 设置里填一遍：
  - 仓库所有者 `sh1n3y` ｜ 仓库名 `cangku` ｜ 私人令牌（你自己的 Gitee token）
  - 填好保存后，记账自动同步到云端，换手机登录也能拉回。
- ✅ 数据存在 App 自己的 WebView 里，**比网页版更稳**（清浏览器缓存也不会丢）。

## 四、注意事项
- `android/app/src/androidTest` 和 `android/app/src/test` 是 Capacitor 模板自带的占位测试，包名还是默认的，工程里它们**不参与 APK 构建、不影响装手机**。若 Android Studio 里显红，可右键这两个目录 → `Mark Directory as` → `Excluded`，或直接删掉，无影响。
- 改了网页 `www/` 里的内容后，想同步进 App：在本机装好 Node 后，到 `记账App/` 目录跑 `npx cap sync android`，再重新 Run。
- 本工程**不含**含 Gitee token 的 `cloud-config.js`（已排除），所以 App 内同步需你手动填一次 token，安全。

## 五、常见问题
- **Gradle 同步卡住/报错**：通常是没联网下载 Gradle 或 SDK 没装全。检查 Android Studio 的 SDK Manager 是否装了对应版本的 SDK Platform。
- **Run 时找不到设备**：确认手机「USB 调试」已开、数据线是数据传输线（部分充电线不行）、电脑装了手机驱动。
- **想换 app 图标/名称**：名称在 `android/app/src/main/res/values/strings.xml` 的 `app_name`；图标替换 `android/app/src/main/res/mipmap-*` 下的图片（可用 Android Studio 的 `Image Asset` 工具批量生成）。
