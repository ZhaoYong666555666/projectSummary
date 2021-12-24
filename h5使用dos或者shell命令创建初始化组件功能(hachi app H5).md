### hachi app h5 dos\shell命令式创建初始化组件功能
1.目的：统一创建hachi app h5组件化的html、css、js、vue文件的模板。

2.根本原因：早期h5组件化由于外包使用的技术比较原始，过度到组件话的过程中不得不保留.html模板，引用之间也耦合了很多东西。为了兼容这种原始版本的代码，开发的编译流程也规定了html、css、js、vue文件的目录和文件名必须保持统一。但是，创建模板不但工作流程冗余而且容易出错，极为不便。



3.流程：只有一步。在编译目录下，终端执行命令node generator.js，只需要输入要被创建的目录名和文件名，即可生成一套具有对应关系的html、css、js、vue文件原始模板，并且他们之间有正确的引用关系。

4.效果：

红色部分会询问输入

![截图一](https://s2.loli.net/2021/12/24/fQdWxyNTqhU6mIr.png)




生成的文件，目录统一
![截图二](https://s2.loli.net/2021/12/24/bSceNsqYJdmTKgZ.png)




vue和js的alias引用关系正确 ✅

![截图三](https://s2.loli.net/2021/12/24/Tt9heUbsWNuD6VI.png)

![截图四](https://s2.loli.net/2021/12/24/g7pdvWNEt5ol6ZT.png)
