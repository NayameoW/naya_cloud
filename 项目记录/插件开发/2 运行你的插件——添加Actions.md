本文内容主要流程按照官网手册展开，也是较为准确的翻译。原文可见：[Creating Actions | IntelliJ Platform Plugin SDK (jetbrains.com)](https://plugins.jetbrains.com/docs/intellij/working-with-custom-actions.html#testing-the-custom-action)

# Actions
插件可以在 IDE 的菜单或者工具栏中添加一些条目，也可以添加新的菜单或者工具栏。而这些被添加的东西产生的交互就被称为 Actions。要完成插件的 Actions 必须进行定义和注册这两大步。
## 1 创建自定义 Action
自定义的 Action 继承抽象类 `AnAction`，其中你应当重载 `AnAction.update()` 方法，以及**必须**重载 `AnAction.actionPerformed()` 方法。
- `AnAction.update()` 方法通过代码实现对某一 action 的有效和无效化
- `AnAction.actionPerformed()` 方法实现 action 被用户调用时所执行的代码
- 面向 IntelliJ Platform 2022.3 以后的版本，要注意 `AnAction.getActionUpdateThread()` 必须实现
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
> `AnAction` 类没有任何形式的类作用域，这个限制放置了内存泄漏。详情可见 [Action的实现](https://github.com/JetBrains/intellij-community/blob/idea/223.7571.182/platform/editor-ui-api/src/com/intellij/openapi/actionSystem/AnActionEvent.java)。

此时 `update()` 默认 action 有效，`actionPerformed()` 中什么也不干。这两个方法将会在接下来进行完善。但是在这之前，为了完成其最小程度的实现，必须先进行注册。

## 2 注册你的 Action
### 2.1 IDE 提供的便捷注册方式
![image.png](https://s2.loli.net/2023/01/17/IKdrZq97tSCXliQ.png)

点击上图中 Register Action 即可得到以下界面：
![image.png](https://s2.loli.net/2023/01/17/bxsiU5Sef4apWlE.png)
Name 属性是 action 展示在菜单中的文本，Description 属性是展示的提示文本。


### 2.2 手动注册
直接在 `plugin.xml` 文件中加入需要的属性即可。相关的声明元素和属性列表可以在[这里](https://plugins.jetbrains.com/docs/intellij/basic-action-system.html#registering-actions-in-pluginxml)找到。
如下是一个完整的注册示例：
```xml
<action 
		id="org.intellij.sdk.action.PopupDialogAction" 
		class="org.intellij.sdk.action.PopupDialogAction" 
		text="Action Basics Plugin: Popup Dialog Action" 
		description="SDK action example" 
		icon="SdkIcons.Sdk_default_icon"> 
	<override-text place="MainMenu" text="Popup Dialog Action"/>
	<keyboard-shortcut 
			keymap="$default" 
			first-keystroke="control alt A" 
			second-keystroke="C"/> 
	<mouse-shortcut 
			keymap="$default" 
			keystroke="control button3 doubleClick"/>
	<add-to-group group-id="ToolsMenu" anchor="first"/> 
</action>
```

**Override-Text**
这个例子中使用了 `override-text` 元素，在 IntelliJ 平台 2020.1 版本之后，通过这个元素，action 的文本可以根据其出现的位置而变得不同，比如菜单、工具栏等。这个例子中，只有主菜单上显示较短的"Popup Dialog Action"，其余则是默认的"Action Basics Plugin: Popup Dialog Action"。


## 3 测试最小实现
在完成了上述步骤之后，我们已经得到了可以运行的最小体量的插件。通过 `compile and run` 这个插件，你可以在工具栏（Tools）中看到你添加的文本。
为了测试上面提到的 `override-text` 文本，可以在 **Help | Find Action...** 中查找你的 action。

## 4 完善 AnAction 方法
接下来我们要做的事情就是在新的 action 中实现 `update()` 和 `actionPerformed()` 了。

### 4.1 actionPerformed
这个方法完成的功能，直观上来说就是点击先前添加到菜单栏中的插件后，插件所做的事情。
还是放上官网的示例代码：
``` java
@Override
public void actionPerformed(@NotNull AnActionEvent event) {
  // Using the event, create and show a dialog
  Project currentProject = event.getProject();
  StringBuilder message =
      new StringBuilder(event.getPresentation().getText() + " Selected!");
  // If an element is selected in the editor, add info about it.
  Navigatable selectedElement = event.getData(CommonDataKeys.NAVIGATABLE);
  if (selectedElement != null) {
    message.append("\nSelected Element: ").append(selectedElement);
  }
  String title = event.getPresentation().getDescription();
  Messages.showMessageDialog(
      currentProject,
      message.toString(),
      title,
      Messages.getInformationIcon());
}
```

## 4.2 update
通过完成 `update()` 方法，可以更好地控制 action 的可见性和可用性。在下面展示的代码中，`update()` 方法要求 `Project` 实体是可用的。这要求意味着想要插件可见， IDE 中至少得打开一个项目。而可用性则通过 `Presentation` 实体确定。
``` java
@Override
public void update(@NotNull AnActionEvent event) {
  // Set the availability based on whether a project is open
  Project currentProject = event.getProject();
  event.getPresentation().setEnabledAndVisible(currentProject != null);
}
```

