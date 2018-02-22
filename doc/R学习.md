## Rserver ##
### Rserver简介 ###
Rserve是一个基于TCP/IP协议的，允许R语言与其他语言通信的C/S结构的程序，支持C/C++,Java,PHP,Python,Ruby,Nodejs等。 Rserve提供远程连接，认证，文件传输等功能。我们可以设计R做为后台服务，处理统计建模，数据分析，绘图等的任务。

官方介绍：http://www.rforge.net/Rserve/

### 优缺点 ###

- 优点</br>
1、资源比较丰富：网络上有很多涵盖各个行业的算法</br>
2、良好的可扩展性：可添加自定义函数</br>
3、完备的帮助系统：?函数名  或者  help()  可直接调出函数说明文档，并在最后附带实例</br>
4、开源

- 缺点</br>
1、要熟记命令</br>
2、占用内存 ： 所有的数据处理都是在内存中进行，不适合处理超大规模的数据。</br>
3、运行速度稍慢 ： 即时编译，约相当于C语言的1/20</br>

### 下载安装 ###
- 下载安装包</br>
 R for windows 客户端+服务端 下载地址</br>[https://cran.r-project.org/bin/windows/base/R-3.4.3-win.exe](https://cran.r-project.org/bin/windows/base/R-3.4.3-win.exe "R-3.4.3-win下载地址")  </br>

- 安装</br>
1、选择安装位置</br>
2、安装组件</br>
注意：根据自身电脑操作系统的位数选择，但64位系统可全选，因为64位向下兼容32位系统。
3、启动选项 选择no </br>
4、安装结束

- 服务器安装</br>
R 服务端纯净安装包（win+linux）,解压缩安装</br>
[http://www.rforge.net/Rserve/files/](http://www.rforge.net/Rserve/files/ "R服务器安装包下载")

### 安装RStudio ###


- 下载地址</br>[https://www.rstudio.com/products/rstudio/download/#download](https://www.rstudio.com/products/rstudio/download/#download "RStudio下载地址")</br>


- 编辑器说明![](http://img.blog.csdn.net/20161023220439328)

### 启动服务 ###
在Windows命令窗口进入R_HOME\library\Rserve\libs\i386目录中执行如下命令（我的Windows7是32位的，如果是64位系统对应目录为R_HOME\library\Rserve\libs\x64）：</br>
R CMD Rserve 

上面的启动命令使用的本地模式，如果想远程连接需要增加参数 –RS-enable-remote </br>
R CMD Rserve --RS-enable-remote  

## java调用R ##

### 添加依赖包 ###
下载依赖jar包，地址：[http://www.rforge.net/Rserve/files/](http://www.rforge.net/Rserve/files/ "R依赖下载")</br>
共两个jar包，下载完成后将它们加入到项目的classpath中即可：

 REngine.jar</br>
 RserveEngine.jar

 
### 简单测试 ###
<pre style="font-size:14px">
import org.rosuda.REngine.REXPMismatchException;  
import org.rosuda.REngine.Rserve.RConnection;  
import org.rosuda.REngine.Rserve.RserveException;  
  
public class RserveBegin {  
    public static void main(String[] args) {  
        try {  
            callRserve();  
        } catch (RserveException e) {  
            e.printStackTrace();  
        } catch (REXPMismatchException e) {  
            e.printStackTrace();  
        }  
    }  
      
    static void callRserve() throws RserveException, REXPMismatchException {  
        RConnection rConnection = new RConnection("192.168.1.195");  
          
        String rv = rConnection.eval("R.version.string").asString();  
        System.out.println(rv);  
          
        double [] arr = rConnection.eval("rnorm(10)").asDoubles();  
        for(double d : arr) {  
            System.out.println(d);  
        }  
    }  
} 
</pre>

### 调用.R文件 ###
<pre style="font-size:14px">
<code>
       
</code>
</pre>

### 注意事项 ###
