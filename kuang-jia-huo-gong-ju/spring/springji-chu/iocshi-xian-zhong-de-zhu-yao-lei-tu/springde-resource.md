## Resource

---

Resource是对资源的抽象，比如文件或者classpath下的资源等。

![](/assets/屏幕快照 2018-10-24 下午9.34.19.png)

InputStreamSource只定义了一个方法：`InputStream getInputStream()`，表示所有资源都可以得到输入流，然后读取。

Resource中对资源进一步增强，增加了表示：是否存在、是否可读、资源是否为文件、获取资源的URL/URI/File/等。

WritableResource则定义了对资源的写的能力：`OutputStream getOutputStream()`。

InputStreamResource、ByteArrayResource则分别是InputStream类型、字节数组类型的资源的实现，它们的实现非常简单，InputStreamResource是在类中持有一个`InputStream inputStream`，ByteArrayResource则是在类中持有一个`byte[]byteArray;`。

AbstractFileResolvingResource是“URL指向文件”类型的资源的基础实现

> URL是指统一资源定位符，标准格式如下：协议类型:\[//服务器地址\[:端口号\]\]\[/资源层级UNIX文件路径\]文件名\[?查询\]\[\#片段ID\]；
>
> 比如：
>
> 本机文件  file:///Users/yue/Desktop/%E5%9B%BE%E7%89%87.png
>
> 不加密的网页  [http://www.runoob.com/html/html-url.html](http://www.runoob.com/html/html-url.html)
>
> 加密的网页  [https://rdm.baidu.com/\#/mytask](https://rdm.baidu.com/#/mytask)
>
> 上传或下载文件  ftp://ftp.gimp.org

ClassPathResource和UrlResource则是具体的实现类，即这类资源是URL形式的，二者内部均持有`String path`。

FileUrlResource则是针对URL指向文件即“file:xxx”形式资源的实现类，内部持有`File file`。

PathResource是对`java.nio.file.Path`形式的资源的实现类。

FileSystemResource是对`java.io.File`形式的资源的实现类，内部持有`String path`和`File file`。

## ResourceLoader

---

Spring通过 Resource接口来抽象了所有资源，那么这些资源从哪来呢，如何得到呢？就需要加载这些资源的工具，这个工具就是ResourceLoader。![](/assets/屏幕快照 2018-10-24 下午9.35.24.png)ResourceLoader代表了资源加载器，主要方法为：`Resource getResource(String location);`。

DefaultResourceLoader是ResourceLoader的默认实现，其最主要的逻辑实现在`getResource(String location)`方法中，根据资源的不同类型，即`location`的格式（是否以/开头，是否以classpath:开头等等），来实例化不同的资源。如果以/开头，默认创建ClassPathContextResource的资源。

FileSystemResourceLoader与DefaultResourceLoader的不同在于，重写了getResourceByPath方法，如果以/开头，默认创建FileSystemResource的资源。

ServletContextResourceLoader与FileSystemResourceLoader类似，重写了getResourceByPath方法，如果以/开头，默认创建ServletContextResource的资源。

此外，为了加载以某种pattern配置的路径（如/WEB-INF/\*-context.xml这种Ant风格的）的资源，Spring定义了ResourcePatternResolver接口，用来加载路径下的资源（一般是多个），而ResourcePatternResolver则是其实现类。

## 参考

---

[深入Spring IOC源码之ResourceLoader](http://www.blogjava.net/DLevin/archive/2012/12/01/392337.html)

