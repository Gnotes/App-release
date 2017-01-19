# IOS 发布到App Store

基本是copy&paste参考文档的，请认真阅...

## 步骤

- [`创建应用App IDs和Boudle ID`](#创建应用app-ids和boudle-id)
- [`创建ios证书`](#创建ios证书)
- [`创建本地证书`](#创建本地证书)
- [`添加证书`](#添加证书)
- [`在App Store开辟空间`](#在app-store开辟空间)
- [`填写App审核信息`](#填写app审核信息)

### 创建应用App IDs和Boudle ID

- 点击[`开发者中心`](https://developer.apple.com)登录.

- 选择菜单`Overview`     

<img src="./image/overview.jpg" width="200">    

- 点击 `Certificates, Identifiers & Profiles`  

<img src="./image/certificate.jpg" width="400">    

- 选择`Identifiers` -> `App IDs`

<img src="./image/appis.jpg" width="200">   

- 点击 **`+`** 号 添加App IDs

<img src="./image/addappids.jpg" width="300"> 

- 填写`Name`

App ID Description `Name` 可以自定义，一般为`工程名`，便于记忆和分辨，例如：`MyApp`

<img src="" width="400">

- 填写`Bundle ID`

App ID Suffix 中勾选`Explicit App ID` 

<img src="" width="400">

`Bundle ID`一般格式为`com.companyName.ProjectName`，bundle id 在打包工程的时候会用的，请注意填写,如:`com.someCompany.MyApp`   
在`xcode`中可以查看到项目的`Bundle Indentifier`

<img src="./image/bundle.jpg" width="400">

- 点击`continue`

<img src="" width="400">

- 点击`Submit`

<img src="" width="400">

- 点击`Done`

<img src="" width="400">

### 创建ios证书

点击`Production`后，点击 **`+`** 号

<img src="./image/product.jpg" width="200">   

<img src="./image/addproduct.jpg" width="400">

- 点击`App Store and Ad Hoc`

<img src="./image/hoc.jpg" width="400">

- 点击`Continue`

<img src="./image/hoccontinue.jpg" width="400">

- 点击`Continue`

<img src="./image/certificatecontinue.jpg" width="400">

- **页面不要关闭，稍后上传证书**

### 创建本地证书

- 打开`钥匙串访问`生成本地证书

<img src="./image/key.jpg" width="400">

- 打开钥匙串访问，点击电脑左上角的`钥匙串访问` –> `证书助理` –> `从证书颁发机构请求证书`

<img src="./image/requestkey.jpg" width="200">

- 填写好信息，`保存到本地`

常用名称：`证书保存名字，会添加到钥匙串访问中`

<img src="./image/savekey.jpg" width="400">

- 选择`存储到桌面`，`存储`，点击`完成`

<img src="./image/savetodesktop.jpg" width="400">

- 桌面上就可以看到证书

<img src="./image/keyondesktop.jpg" width="200">

### 添加证书

- 然后回到浏览器，点击`choose File..` 选择创建好的：`CertificateSigningRequest.certSigningRequest` 文件，点击`Generate`

<img src="./image/uploadkey.jpg" width="400">

- 点击`Download`下载创建好的发布证书（cer后缀的文件），然后点击`Done`，你创建的发布证书就会存储在帐号中

<img src="./image/ios_cer.jpg" width="200">

`双击安装`（如果安装不上，可以直接将证书文件拖拽到钥匙串访问的列表中）

**注**：一般一个开发者帐号创建一个发布证书就够了，如果以后需要在其他电脑上上架App，只需要在钥匙串访问中创建p12文件，把p12文件安装到其他电脑上。这相当于给予了其他电脑发布App的权限

- 找到`Provisioning Profiles` ，点击`All`，然后点击右上角 **`+`** 号

<img src="./image/proall.jpg" width="200">    

<img src="./image/proalladd.jpg" width="400">

- 选择`App Store`，点击`Continue`

<img src="./image/appstoreprofile.jpg" width="400">

- 在`App ID` 这个选项栏里面找到你刚刚创建的：`App IDs（Bundle ID） 类型的套装`，点击`Continue`

<img src="./image/appid.jpg" width="400">

- 选择你刚创建的发布证书（或者生成p12文件的那个发布证书），点击`Continue`

<img src="./image/continuekey.jpg" width="400">

- 在`Profile Name`栏里输入一个名字（这个是`PP`文件的名字，可随便输入，在这里我用工程名字，便于分别），然后点击`Generate`

<img src="./image/generate.jpg" width="400">

- `Download`生成的PP文件，然后点击`Done`

<img src="./image/downloadanddone.jpg" width="400">

### 在App Store开辟空间

- 回到`Member Center`，点击`iTunes Connect`

<img src="./image/itunesconnect.jpg" width="400">

- 登录itunes

<img src="./image/ituneslogin.jpg" width="400">

- 点击`我的App`

<img src="./image/myapp.jpg" width="400">

- 点击`新建 iOS App`

<img src="./image/newiosapp.jpg" width="200">

- 填写信息并创建

平台：勾选 `iOS`   
名称：为应用的名称，是直接展示在手机上的名称   
语言选择：简体中文   
套装ID：选择刚创建的套装ID，为我们的bundle identifier   
SKU：套装ID与SKU主要是app的唯一标识吧，我是用的项目中Bundle Identifier的内容

<img src="./image/entermsg.jpg" width="200">

### 填写App审核信息

**注意啦：填写完每一项信息请记得`存储`，这个很重要滴，不是`提交审核`哈**

部分信息请参照提示填写

- 填写app信息&价格与定价

<img src="./image/appmsg.jpg" width="200">

- 上传APP截图

`这里需要不同屏幕的截图，可以直接用模拟机运行后截图。待模拟器运行开始的时候，按住cmd+S, 模拟器的屏幕截图就直接保存在桌面上`    
`模拟器需要100%，不然上传的图片会出错`    
`4.7英寸 ——>iphone6          5.5英寸——>iphone 6 plus       4英寸 ——>iphone5S            3.5英寸 ——> iphone 4S`    

<img src="./image/uploadscreenshut.jpg" width="400">

- 上传App Icon

上传App Icon的时候，需要上`1024*1024`的，而且不能有圆角效果哦！

- 生成.ipa文件

**在打包之前请确认配置是否正确...**   
**是否为release版**   
**version 是否正确**   
**bundle indentifier 是否正确**   
**info.plist 是否正确**   
等等...


打开`xcode` -> `Product` -> `Arichive` 生成打包文件

<img src="./image/arichive.jpg" width="400">

- Validate

打包完成后点击`Validate` 验证是否通过审核,这里会需要选择相对应的证书，就是我们刚生成的证书

- Export

点击`Export` 导出文件到本地

<img src="./image/validateandexport.jpg" width="200">

- ipa包上传

我使用的是`Applicaton Loader`,点击`选取`，选择导出的ipa的文件，然后选择对应的信息

<img src="./image/loader.jpg" width="200">

- 构建版本

上传成功后刷新页面，在构建版本出可以选择刚上传的app

<img src="./image/createversion.jpg" width="400">

- 添加测试账号

这个是必须的哟，不然会审核拒绝

- 联系人电话

中国区的号码请记得加区号`+86`，如`+86 18912345678`

- 提交审核