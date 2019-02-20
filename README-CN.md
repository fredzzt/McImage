# McImage

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/mcimage/McImage)

[Android优雅的打包时自动化获取全部res资源)](https://smallsoho.com/android/2018/07/26/Android-Android%E4%BC%98%E9%9B%85%E7%9A%84%E6%89%93%E5%8C%85%E6%97%B6%E8%87%AA%E5%8A%A8%E5%8C%96%E8%8E%B7%E5%8F%96%E5%85%A8%E9%83%A8res%E8%B5%84%E6%BA%90/)

McImage是无侵入式的全量压缩资源图片插件

包括

- Jar包中的图
- AAR中的图
- 子Module中的图

插件使用算法

- [pngquant](https://github.com/pornel/pngquant)算法压缩png
- [guetzli](https://github.com/google/guetzli)算法压缩jpg
- [cwebp](https://developers.google.com/speed/webp/)算法转换webp

### Release Success!

1.0.1版本现在支持全版本的build.gradle脚本！

### Feature

- 全量压缩png和jpg图片，每张图能节省百分之70大小
- 最大化收益下对图片进行webp转换 (after v0.0.3 support)
- 插件自动化匹配当前操作系统，包括Linux，Mac，Windows (after v0.0.4 support)
- 插件接入简单，无感知，仅要一行代码

### Update Log

> v0.0.2以后的用户更新到0.0.2以上需要升级你的mctools文件夹，已经上传到release。

- 1.0.1 : 修复了maxSize无法使用浮点数的问题
- 1.0.0 : 正式支持了AAPT2，现在不需要使用android.enableAapt2=false关闭了，可以去掉这个flag
- 0.1.5 : Bug fix，添加了不处理的图片的白名单，添加了对图片宽高的检查的Feature
- 0.1.2 : Bug fix，修复了检查图片大小功能不生效的问题
- 0.1.1 : Bug fix，修复了在module中apply无法编译通过的问题，修复了enableWhenDebug开关无法使用的问题
- 0.0.4 : 添加了自动识别操作系统的支持，去掉了webpQuality选项（设置不好对图片压缩会肉眼可见，强制使用默认值），优化了Log写法
- 0.0.3 : 添加了对webp的支持。会在压缩之后自动将你符合规则的图片转换为webp格式，并且会比对大小，如果转换之后更大则舍弃转换，并且插件对API 14 和API 18的webp问题进行了处理，具体问题请google查询。
- 0.0.2 : 完善了日志的输出

### Who is using

如果你使用McImage，我可以把你的icon放在这里并且加上一个链接~ 发到我的邮箱b3069741@gmail.com并备注mcimage即可

PS:目前我司项目正在使用此仓库进行压缩

### Use

首先，修改你根目录的build.gradle.

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.smallsoho.mobcase:McImage:1.0.1'
    }
}
```

然后在你想要压缩的Module的build.gradle中应用这个插件，注意如果你有多个Module，请在每个Module的build.gradle文件中apply插件

```groovy
apply plugin: 'McImage'
```

最后将我代码中的mctools文件夹放到项目根目录，此文件在[这里下载](https://github.com/Mobcase/McImage/releases)

```
mctools
```

### Config

你可以在build.gradle中配置插件的几个属性，如果不设置，所有的属性都使用默认值

```groovy
McImageConfig {
  isCheck true //default true   是否进行图片大小超标的检查
  isCompress true //default true  是否进行图片压缩
  maxSize 1*1024*1024 //default 1MB  图片大小超标的标准大小
  isWebpConvert true //default true 是否进行对图片的webp处理
  isJPGConvert true //default true 是否对jpg进行webp处理
  enableWhenDebug true //default true 是否在debug的时候启用插件
  isCheckSize true //default true 是否开启图片宽高检查
  maxWidth 500 //defualt 500 如果开启图片宽高检查，默认的最大宽度
  maxHeight 500 //defualt 500 如果开启图片宽高检查，默认的最大高度
  whiteList = [
    "drawable-xxhdpi-v4/img_five_stars.png" //默认为空，如果添加，对图片不进行任何处理
  ]
}
```

图片大小检查:一种是图特别大，一种是图宽高特别大，提示"You have big Img!!!! "，来避免OOM和包增大。

### Thanks

[pngquant](https://github.com/pornel/pngquant)

[guetzli](https://github.com/google/guetzli)

[cwebp](https://developers.google.com/speed/webp/)

License
-------

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
    
       http://www.apache.org/licenses/LICENSE-2.0
    
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
