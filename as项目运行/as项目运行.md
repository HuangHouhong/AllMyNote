# 国内创建项目同步缓慢

国内环境，创建项目后可能同步速度可能十分缓慢，在新建项目的收，可以通过如下两部减少 gradle 同步时间。

1. 修改 gradle-wrapper.properties 文件
2. 修改根项目 build.gradle 文件

gradel-wrapper.properties 文件中，修改如下所示：

```groovy
# 把gradle地址指定为本地路径下的
distributionUrl=file\:///home/huang/Android/gradle/gradle-6.5-all.zip
```

在指定之前可以下载好指定版本的 gradle 文件，然后放在任意目录下，指定distributionUrl 为本地路径，就不需要从网上去下载了。

build.gradle 文件需要修改两处：

```groovy
dependencies {
    classpath "com.android.tools.build:gradle:4.1.3"
    classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
}

allprojects {
    repositories {
        maven { url 'https://maven.aliyun.com/repository/google' }
        jcenter { url 'https://maven.aliyun.com/repository/jcenter' }
    }
}
```

就是换成国内的阿里源，同步速度就可以飞起了。