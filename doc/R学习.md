## Rserver ##
### Rserver简介 ###
Rserve是一个基于TCP/IP协议的，允许R语言与其他语言通信的C/S结构的程序，支持C/C++,Java,PHP,Python,Ruby,Nodejs等。 Rserve提供远程连接，认证，文件传输等功能。我们可以设计R做为后台服务，处理统计建模，数据分析，绘图等的任务。

官方介绍：http://www.rforge.net/Rserve/

### 下载安装包 ###
R for windows 客户端下载地址</br>[https://cran.r-project.org/bin/windows/base/](https://cran.r-project.org/bin/windows/base/ "R下载地址")  </br>

R 服务端纯净安装包
[http://www.rforge.net/Rserve/files/](http://www.rforge.net/Rserve/files/ "R服务器")

### 安装 ###
客户端安装教程</br>[https://jingyan.baidu.com/article/f79b7cb36a443d9144023efd.html?st=2&net_type=&bd_page_type=1&os=0&rst=&word=%E4%B8%8B%E6%94%AF%E5%8F%91%E5%86%B7](https://jingyan.baidu.com/article/f79b7cb36a443d9144023efd.html?st=2&net_type=&bd_page_type=1&os=0&rst=&word=%E4%B8%8B%E6%94%AF%E5%8F%91%E5%86%B7 "R安装教程")
服务端安装教程</br>
解压即可

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
