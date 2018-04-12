---
title: "如何给apk签名(翻译自ionic官方文档)"
date: 2018-04-11T00:06:57+08:00
draft: true
---

如果你想将你的app发布到google play 商店，你需要为你的apk文件签名。在此之前，你需要新增一个新的证书/密钥库。

让我们使用jdk提供的`keytool`命令来生成你的私钥(一般在`jdk/bin`目录下)：

```bash
keytool -genkey -v -keystore my-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-alias
```

命令首先会提示为你的密钥库设置密码。然后，回答这个出色工具剩余的问题，当这些全部完成，你的当前目录应该有了一个名字为`my-release-key.jks`的文件。

注意：确保将这个文件保存到安全的地方，如果丢失你将无法为你的app提交更新！

为了给未签名的apk签名，运行同样由jdk提供的`jarsigner`工具：

```bash
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.jks android-release-unsigned.apk my-alias
```

这将完成APK的签名。最后，我们需要运行zip对齐工具来优化APK。`zipalign`工具位于`/path/to/Android/sdk/build-tools/VERSION/zipalign`。例如，在安装了Android Studio 的 OS X系统中，zipalign 位于`~/Library/Android/sdk/build-tools/VERSION/zipalign`

```bash
zipalign -v 4 android-release-unsigned.apk HelloWorld.apk
```

为了确保你的apk已经被签名，运行`apksigner`。`apksigner` 位于`zipalign` 同一目录下

```bash
apksigner verify HelloWorld.apk
```

现在我们拥有了我们的最终发行版二进制文件HelloWorld.apk，下面我们可以在谷歌应用商店发布它，让全世界使用！