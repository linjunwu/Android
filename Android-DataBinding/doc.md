# 过程通俗描述：
<b>
1、databinding插件遍历res/layout目录下所有的布局文件，如果布局文件是以layout为根节点就将该布局文件加入到用于生成Binding类的布局文件列表中。<br\>
2、databinding插件生成各个布局文件对应的Binding类文件。<br\>
3、databinding插件生成一个BindingMap类，该类可以通过layoutId,获取对应的Binding类。（有点类似工厂模式)<br\>
4、在Activity中通过向工具类DataBindingUtil传递layoutId获取Activity对应的Binding类。<br\>
</b>