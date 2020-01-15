# zookeeper
zookeeper源码分析

### 代码下载
[zookeeper源码下载](https://github.com/apache/zookeeper/releases)

### 源码编译
1. zookeeper是用ant构建，需要安装ant环境
2. 生成eclipse源码  

		cd E:\github\zookeeper
		ant eclipse

### 导入项目
1.  导入eclipse
2.	错误处理
		
		错误1：编译完成后，用Eclipse打开编译错误，显示Java compiler level does not match 
		      和 '<>' operator is not allowed for source level below 1.7错误。
		修改方法：右键项目--属性--勾选Enable project  specific  settings--Compiler compliance level--选择1.7--OK。
		
		错误2：org.apache.zookeeper.Version报错，org.apache.zookeeper.version.Info这个接口找不到。
		修改方法：这个接口可以通过运行org.apache.zookeeper.version.util.VerGen的Main方法来生成这个文件，方法需要传递3个参数

```java(3个参数写死)
		public static void main(String[] args2) {
        String[] args =new String[]{"1.0.0"," ",""};
        System.out.println("args's length:"+args.length);
        if (args.length != 3)
            printUsage();
        try {
            Version version = parseVersionString(args[0]);
            if (version == null) {
                System.err.println(
                        "Invalid version number format, must be \"x.y.z(-.*)?\"");
                System.exit(1);
            }
            String rev = args[1];
            if (rev == null || rev.trim().isEmpty()) {
                rev = "-1";
            } else {
                rev = rev.trim();
            }
            generateFile(new File("."), version, "", args[2]);
        } catch (NumberFormatException e) {
            System.err.println(
                    "All version-related parameters must be valid integers!");
            throw e;
        }
    }
```

### 项目运行

`zkServer`入口方法为`org.apache.zookeeper.server.ZooKeeperServerMain` 
   
复制`conf/zoo.sample.cfg`为 `/conf/zoo.cfg`  
  
右键`Run As` -> `Run Configurations` -> `Arguments` -> `Program arguments` -> 添加 `conf/zoo.cfg`

### 参考文档

[搭建ZooKeeper源码工程](https://www.cnblogs.com/gudi/p/8068610.html)