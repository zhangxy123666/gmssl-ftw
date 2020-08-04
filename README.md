# 梳理了下完整的编译运行流程



1-  先从官网下载一份干净的代码，如果中间出错或者有改动，记得删除掉从新解压  

2-  按照官网正常流程编译，不要在Configure里面加java，加上一定编译不过   

    linux是make, windowns是nmake, 编译好之后， 进入到GmSSL的java目录，建立包名的目录  
    
    也就是建立 org/gmssl 然后把GmSSL.java移到这个目录下  
    
    先在GMSSL里面的java目录下执行 gcc -shared -fPIC -Wall -I./jni -I ../include -L ../ GmSSL.c -lcrypto -o libgmssljni.dll  
    
    然后执行编译 javac org\gmssl\GmSSL.java  
    
    （如果提示找不到动态库，就直接这样写  
    
    static {  
    
    System.load("D:\xxxxx\GmSSL-master\GmSSL-master\java\libgmssljni.dll");  
    
    }）
    然后执行 java org.gmssl.GmSSL
    
    可能会出现
    ···
        Ciphertext: Exception in thread "main" java.lang.NullPointerException
            at org.gmssl.GmSSL.main(GmSSL.java:149)

    ··· 
    解决办法是把  libcrypto.lib   libcrypto-1_1-x64.dll  复制到java文件目录下 在执行就可以了 
    上图
