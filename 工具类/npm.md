# npm - 换淘宝源

安装Node时Node 的模块管理器 npm 会一起安装好。
之前一开始安装想切换淘宝源
    
    npm i --registry=https://registry.npm.taobao.org
但是这样不方便，每次都要打`--registry=https://registry.npm.taobao.org`，之后在网上寻找看有没有便捷的方法，找到了，以下
        
    $ npm config set registry https://registry.npm.taobao.org/

执行下面的命令，确认是否切换成功。
            
    $ npm config get registry

成功之后直接`npm i`即可