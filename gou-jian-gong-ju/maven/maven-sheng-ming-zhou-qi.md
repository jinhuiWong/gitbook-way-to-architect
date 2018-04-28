# Maven生命周期

Maven有三种不同的生命周期（Lifecycle），分别是Clean、Default、Site。每个生命周期又包含不同的阶段（Phase）。

当我们在运行一个命令的时候，该命令都会对应某个生命周期的某个阶段，并且该生命周期中的在此阶段之前的命令都会被执行。比如，`mvn clean` 等同于 `mvn pre-clean clean` ，如果我们运行 `mvn post-clean` ，那么` pre-clean，clean` 都会被运行。这是Maven很重要的一个规则，可以大大简化命令行的输入。

具体某个阶段应该做什么工作，怎么做，Maven有默认的行为，当然也可以通过插件进行定制修改。

## **Clean Lifecycle** 

在进行真正的构建之前进行一些清理工作，Clean声明周期包含如下三个Phase。

| pre-clean | execute processes needed prior to the actual project cleaning |
| --- | --- | --- |
| clean | remove all files generated by the previous build |
| post-clean | execute processes needed to finalize the project cleaning |

比如，我们在执行mvn clean的时候，其实是让Maven做它的Clean生命周期中的clean阶段应该去做的工作（当然，包含Clean生命周期中clean阶段之前的所有阶段的工作）。

## **Default Lifecycle**

构建的核心部分，编译，测试，打包，部署等等。

| validate | validate the project is correct and all necessary information is available. |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| initialize | initialize build state, e.g. set properties or create directories. |
| generate-sources | generate any source code for inclusion in compilation. |
| process-sources | process the source code, for example to filter any values. |
| generate-resources | generate resources for inclusion in the package. |
| process-resources | copy and process the resources into the destination directory, ready for packaging. |
| compile | compile the source code of the project. |
| process-classes | post-process the generated files from compilation, for example to do bytecode enhancement on Java classes. |
| generate-test-sources | generate any test source code for inclusion in compilation. |
| process-test-sources | process the test source code, for example to filter any values. |
| generate-test-resources | create resources for testing. |
| process-test-resources | copy and process the resources into the test destination directory. |
| test-compile | compile the test source code into the test destination directory |
| process-test-classes | post-process the generated files from test compilation, for example to do bytecode enhancement on Java classes. For Maven 2.0.5 and above. |
| test | run tests using a suitable unit testing framework. These tests should not require the code be packaged or deployed. |
| prepare-package | perform any operations necessary to prepare a package before the actual packaging. This often results in an unpacked, processed version of the package. \(Maven 2.1 and above\) |
| package | take the compiled code and package it in its distributable format, such as a JAR. |
| pre-integration-test | perform actions required before integration tests are executed. This may involve things such as setting up the required environment. |
| integration-test | process and deploy the package if necessary into an environment where integration tests can be run. |
| post-integration-test | perform actions required after integration tests have been executed. This may including cleaning up the environment. |
| verify | run any checks to verify the package is valid and meets quality criteria. |
| install | install the package into the local repository, for use as a dependency in other projects locally. |
| deploy | done in an integration or release environment, copies the final package to the remote repository for sharing with other developers and projects. |

我们最常用的就是`mvn package `或者`mvn install `或者`mvn compile`了。

## **Site Lifecycle**

生成项目报告，站点，发布站点。

| pre-site | execute processes needed prior to the actual project site generation |
| --- | --- | --- | --- |
| site | generate the project's site documentation |
| post-site | execute processes needed to finalize the site generation, and to prepare for site deployment |
| site-deploy | deploy the generated site documentation to the specified web server |



## 参考

#### [Maven生命周期详解](http://juvenshun.iteye.com/blog/213959)

\[Introduction to the Build Lifecycle\]\([http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html](http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)\)
