
# 关于 ./mvnw install
You can also install Maven (>=3.3.3) yourself and run the mvn command in place of ./mvnw in the examples below. If you do that you also might need to add -P spring if your local Maven settings do not contain repository declarations for spring pre-release artifacts.
您也可以自己安装 Maven (>=3.3.3) 并运行 mvn 命令代替下面示例中的 ./mvnw。 如果您这样做，您可能还需要添加 -P spring 如果您的本地 Maven 设置不包含 spring 预发布工件的存储库声明。

1.保证idea中的maven设置是使用maven wrapper，而不是使用系统的mvn
2.也就是会执行.mvn/wrapper/maven-wrapper.jar 同时会将 maven.config中的参数传递到 mvn命令中
maven.config 中配置了
-DaltSnapshotDeploymentRepository=repo.spring.io::default::https://repo.spring.io/libs-snapshot-local -P spring

-P其实就是指定 profile，类似于 当前项目中的.settings.xml中的profile
为什么要指定profile呢？因为profile中配置了仓库的地址，如果不通过这种方式指定仓库的地址，maven wrapper还是会使用系统的settins.xml到aliyun仓库下载依赖。实际有些snapshot依赖在aliyun找不到。


```agsl
Activate the Spring Maven profile
Spring Cloud projects require the 'spring' Maven profile 
to be activated to
 resolve the spring milestone and snapshot repositories. 
 Use your preferred IDE to set this profile to be active, 
 or you may experience build errors.
```
上面这段内容主要是说 我们需要使用一个叫做 spring的 maven profile 来构建spring cloud项目，这个profile会将spring的仓库地址添加到maven的配置中，否则会出现构建错误。
而名称叫做spring的 profile 在 项目的.settings.xml文件中有配置。 因此我们的idea maven设置中 更改使用当前项目中的.settings.xml作为配置文件


# build project 
mvnw.cmd install -X -Dmaven.test.skip=true
