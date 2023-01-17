本文内容主要流程按照官网手册展开，也是较为准确的翻译。原文可见：[Creating Actions | IntelliJ Platform Plugin SDK (jetbrains.com)](https://plugins.jetbrains.com/docs/intellij/working-with-custom-actions.html#testing-the-custom-action)

# Actions
插件可以在IDE的菜单或者工具栏中添加一些条目，也可以添加新的菜单或者工具栏。而这些被添加的东西产生的交互就被称为Actions。要完成插件的Actions必须进行定义和注册这两大步。
## 1 创建自定义Action
自定义的Action继承抽象类`AnAction`，其中你应当重载`AnAction.update()`方法，以及**必须**重载`AnAction.actionPerformed()`方法。
- `AnAction.update()`方法通过代码实现对某一action的有效和无效化
- `AnAction.actionPerformed()`方法实现action被用户调用时所执行的代码
- 面向IntelliJ Platform 2022.3以后的版本，要注意`AnAction.getActionUpdateThread()`必须实现
以下是官网的例子：
```java
public class PopupDialogAction extends AnAction { 

	@Override public void update(@NotNull AnActionEvent event) { 
		// Using the event, evaluate the context, 
		// and enable or disable the action. 
	} 
	
	@Override public void actionPerformed(@NotNull AnActionEvent event) { 
		// Using the event, implement an action. 
		// For example, create and show a dialog. 
	} 
	
	// Override getActionUpdateThread() when you target 2022.3 or later! 

}
```
> `AnAction`类没有任何形式的类作用域，这个限制放置了内存泄漏。详情可见[Action的实现](https://github.com/JetBrains/intellij-community/blob/idea/223.7571.182/platform/editor-ui-api/src/com/intellij/openapi/actionSystem/AnActionEvent.java)。

此时`update()`默认action有效，`actionPerformed()`中什么也不干。这两个方法将会在接下来进行完善。但是在这之前，为了完成其最小程度的实现，必须先进行注册。

## 2 注册你的Action
### 2.1 IDE提供的便捷注册方式
![image.png](https://s2.loli.net/2023/01/17/IKdrZq97tSCXliQ.png)

点击上图中Register Action即可得到以下界面：
![image.png](https://s2.loli.net/2023/01/17/bxsiU5Sef4apWlE.png)
Name属性是action展示在菜单中的文本，Description属性是展示的提示文本。


### 2.2 手动注册


## 3 测试最小实现

## 4 完善
