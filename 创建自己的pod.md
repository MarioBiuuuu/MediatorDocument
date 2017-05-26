# 创建自己的pod
1. 首先在github新建repo
![github.png](http://upload-images.jianshu.io/upload_images/619614-88e5eb205fc358a7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. clone仓库至本地
![clone.png](http://upload-images.jianshu.io/upload_images/619614-70e66e207c99f686.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3. 初始化项目
![initial.png](http://upload-images.jianshu.io/upload_images/619614-5513aa4b930aab35.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. 创建podspec文件  
```
pod spec create MBMediator https://github.com/MarioBiuuuu/MBMediator.git
``` 
![podspec.png](http://upload-images.jianshu.io/upload_images/619614-3b7ea31e4afa23a6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
5. 配置podspec 
```
Pod::Spec.new do |s|
  s.name         = "MBMediator"
  s.version      = "0.0.1"
  s.summary      = ""
  s.description  = <<-DESC
                   DESC
  s.homepage     = "https://github.com/MarioBiuuuu/MBMediator"
  s.license      = "MIT"
  s.author             = { "AuthorName" => "AuthorEmail" }
  s.platform     = :ios, "7.0"
  s.source       = { :git => "https://github.com/MarioBiuuuu/MBMediator.git", :tag => s.version}
  s.source_files  = "MBMediator", "MBMediator/**/*.{h,m}"
end
```
s.source_files = ' ' 的多种写法
```
ss.source_files = 'MBMediator/Class/*.{h,m}'
```
表示MBMediator/Class/目录下的所有 .h 和 .m 文件
```
s.source_files = 'MBMediator/**/ .'
```
/后面的 . 应是 星号，MarkDowm语法冲突在此不能正常显示
表示MBMediator/ 目录下所有文件，包括子目录下所有文件。 **/.表示递归
当有多个文件时，应用,隔开
```
 s.source_files = 'MBMediator/Class.{h,m}', 'MBMediator/Util*'
```
6. 给项目打tag，并push到远程仓库
```
git tag 0.0.1
```
push到远程仓库
```
git push origin --tags
```
7. 验证podspec是否正确
```
pod lib lint
``` 
![liblint.png](http://upload-images.jianshu.io/upload_images/619614-1e465e879397bbde.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

8. pod Trunk注册
```
 pod trunk register email地址 'MBMediator'
```
![trunk.png](http://upload-images.jianshu.io/upload_images/619614-00e15db242b858b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
根据提示前往邮箱确认，然后执行
```
pod trunk me
```
![trunkme.png](http://upload-images.jianshu.io/upload_images/619614-490266cef2ef11e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
9. 上传MBMediator.podspec 到 CocoaPods/repo
```
pod trunk push MBMediator.podspec
```
![result.png](http://upload-images.jianshu.io/upload_images/619614-0d319bb830952f39.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

10. 检验
```
pod search MBMediator
```

11. 上传成功后搜索不到自己的库怎么办？
```
[!] Unable to find a pod with name, author, summary, or descriptionmatching '······'
```
删除`~/Library/Caches/CocoaPods`目录下的`search_index.json`文件
由于`pod setup`成功后会生成`~/Library/Caches/CocoaPods/search_index.json`文件。
终端输入`rm ~/Library/Caches/CocoaPods/search_index.json`
删除成功后再执行`pod search`

