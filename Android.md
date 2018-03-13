# Android 发布到应用市场

## 生成签名

> Android要求所有应用都有一个数字签名才会被允许安装在用户手机上，Android开发者官网上的如何给你的 [应用签名文档](https://developer.android.com/tools/publishing/app-signing.html) 描述了签名的细节  

生成签名有两种方式：

- Keytool命令行
- Android Studio界面生成

### Keytool

Keytool 是一个Java 数据证书的管理工具 ,Keytool 将密钥（key）和证书（certificates）存在一个称为keystore的文件中，在keystore里，包含两种数据： 

- `密钥实体（Key entity` : 密钥（secret key）又或者是私钥和配对公钥（采用非对称加密） 
- `可信任的证书实体（trusted certificate entries）` : 只包含公钥

#### 常用参数

- `-genkey` : 在用户主目录中创建一个默认文件".keystore"
- `-alias` : 产生别名，默认(mykey)，mykey中包含用户的公钥、私钥和证书
- `-keystore` : 指定密钥库的名称(产生的各类信息将不在.keystore文件中)
- `-keyalg` : 指定密钥的算法，如：RSA、DSA(默认)
- `-validity` : 指定创建的证书有效期多少天，默认（90天）
- `-keysize` : 指定密钥长度，默认(1024)
- `-storepass` : 指定密钥库的密码(获取keystore信息所需的密码)
- `-keypass` : 指定别名条目的密码(私钥的密码)
- `-dname` : 指定证书拥有者信息 例如："CN=名字与姓氏,OU=组织单位名称,O=组织名称,L=城市或区域名称,ST=州或省份名称,C=单位的两字母国家代码"
- `-list` : 显示密钥库中的证书信息，keytool -list -v -keystore 指定keystore -storepass 密码
- `-v` : 显示密钥库中的证书详细信息
- `-export` : 将别名指定的证书导出到文件 ，keytool -export -alias 需要导出的别名 -keystore 指定keystore -file 指定导出的证书位置及证书名称 -storepass密码
- `-file` : 参数指定导出到文件的文件名
- `-delete` : 删除密钥库中某条目 ，keytool -delete -alias 指定需删除的别  -keystore 指定keystore  -storepass 密码
- `-printcert` : 查看导出的证书信息，keytool -printcert -file yushan.crt
- `-keypasswd` : 修改密钥库中指定条目口令，keytool -keypasswd -alias 需修改的别名 -keypass 旧密码 -new  新密码  -storepass keystore密码  -keystore sage
- `-storepasswd` : 修改keystore口令，keytool -storepasswd -keystore e:/yushan.keystore(需修改口令的keystore) -storepass 123456(原始密码) -new yushan(新密码)
- `-import` : 将已签名数字证书导入密钥库，keytool -import -alias 指定导入条目的别名 -keystore 指定keystore -file 需导入的证书

#### 生成步骤

```shell
keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000

# 也可以通过参数指定下边的其他值

输入密钥库口令:
再次输入新口令:您的名字与姓氏是什么?
  [Unknown]:  xing.he
您的组织单位名称是什么?
  [Unknown]:  github
您的组织名称是什么?
  [Unknown]:  github
您所在的城市或区域名称是什么?
  [Unknown]:  shanghai
您所在的省/市/自治区名称是什么?
  [Unknown]:  shanghai
该单位的双字母国家/地区代码是什么?
  [Unknown]:  zh
CN=xing.he, OU=github, O=github, L=shanghai, ST=shanghai, C=zh是否正确?
  [否]:  y

正在为以下对象生成 2,048 位RSA密钥对和自签名证书 (SHA256withRSA) (有效期为 10,000 天):
         CN=xing.he, OU=github, O=github, L=shanghai, ST=shanghai, C=zh
输入 <my-key-alias> 的密钥口令
        (如果和密钥库口令相同, 按回车):
[正在存储my-release-key.keystore]
```

这条命令会要求你输入密钥库（keystore）和对应密钥的密码，然后设置一些发行相关的信息。最后它会生成一个叫做`my-release-key.keystore`的密钥库文件,
在运行上面这条语句之后，密钥库里应该已经生成了一个单独的密钥，有效期为10000天。--alias参数后面的别名是你将来为应用签名时所需要用到的，所以记得记录这个别名

### Android Studio

`Build` -> `Generate Signed APK` -> `Create New` -> 输入签名参数即可自动生成，默认签名文件的后缀是`.jks`

### 查看keystore信息

```shell
keytool -list -v -keystore PATH_TO_KEYSTORE.keystore # -storepass 可以通过这个参数指定密码，也可以根据提示随后输入

输入密钥库口令:

密钥库类型: JKS
密钥库提供方: SUN

您的密钥库包含 1 个条目

别名: my-key-alias
创建日期: Mar 13, 2018
条目类型: PrivateKeyEntry
证书链长度: 1
证书[1]:
所有者: CN=xing.he, OU=github, O=github, L=shanghai, ST=shanghai, C=zh
发布者: CN=xing.he, OU=github, O=github, L=shanghai, ST=shanghai, C=zh
序列号: 18acbc01
有效期开始日期: Tue Mar 13 15:49:22 CST 2018, 截止日期: Sat Jul 29 15:49:22 CST 2045
证书指纹:
         MD5: D2:35:8B:E2:60:7E:7E:22:89:A3:22:BF:FE:89:38:3F
         SHA1: 6E:7A:47:B4:46:4D:B1:71:53:82:FE:58:F1:C7:59:B4:79:77:5F:3D
         SHA256: 9A:F0:52:EC:FA:E0:06:5F:E0:3A:5E:75:2D:75:AF:CD:62:CA:7D:10:C0:25:59:B7:B8:33:54:9B:55:F5:10:4F
         签名算法名称: SHA256withRSA
         版本: 3

扩展:

#1: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: 74 2D 71 F1 9A 65 5C 83   84 76 8D ED 1C C7 A1 8D  t-q..e\..v......
0010: D3 AF 18 F4                                        ....
]
]



*******************************************
*******************************************
```

## Gradle 配置

- 把`my-release-key.keystore`文件放到你工程中的`android/app`文件夹下。
- 编辑`~/.gradle/gradle.properties`（没有这个文件你就创建一个），添加如下的代码（注意把其中的****替换为相应密码）

```
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=*****
MYAPP_RELEASE_KEY_PASSWORD=*****
```

- 编辑`android/app/build.gradle`

```
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            storeFile file(MYAPP_RELEASE_STORE_FILE)
            storePassword MYAPP_RELEASE_STORE_PASSWORD
            keyAlias MYAPP_RELEASE_KEY_ALIAS
            keyPassword MYAPP_RELEASE_KEY_PASSWORD
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
```

## 生成发行APK包

```shell
cd android && ./gradlew assembleRelease
```

生成的APK文件位于 `android/app/build/outputs/apk/app-release.apk`

## 测试应用的发行版本

```shell
cd android && ./gradlew installRelease
```

**安装报错，尝试 `adb uninstall YOUR_PACKAGE_NAME`**  
**apk真机调试，Android Studio 中搜索 `Android Device Monitor`**  
**真机服务Server没有找到 `db reverse tcp:8081 tcp:8081`**  

## 发布

找到对应发布平台进行发布，如应用宝、豌豆荚、百度等.

## 参考文档

- [react-native#Signed-Apk](https://reactnative.cn/docs/0.51/signed-apk-android.html#content)
- [React-Native for Android 入门](https://race604.com/react-native-for-android-start/)
- [Keytool命名详解](http://blog.csdn.net/zlfing/article/details/77648430)
- [React-Native 签名打包](http://blog.csdn.net/wenzhi20102321/article/details/54174267)
- [React-Native 签名打包](https://www.cnblogs.com/520yang/articles/5390575.html)
