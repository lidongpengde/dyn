# DYN

声明：

此插件借鉴ATG思路，通过spring实现，提供管控界面。

功能概述：

用于在应用运行时动态的执行操作，如修改属性的值，执行spring bean中的方法。

应用场景：

修改开关等属性值、动态查询、修复清洗线上数据，或执行job等操作。

#接入流程：

```

1、clone工程到本地 编译成jar

2、在需要操作的工程中引入jar 有私服的建议使用maven方式

3、相关依赖 
	spring > 3.2.3.RELEASE  
	aspectjweaver >1.7.2 
	org.freemarker > 2.3.20 
	fastjson > 1.2.28

3、web.xml引入配置

<servlet>
		<servlet-name>dyn</servlet-name>
		<servlet-class>com.conning.compents.servlet.DynServlet</servlet-class>
</servlet>
<servlet-mapping>
		<servlet-name>dyn</servlet-name>
		<url-pattern>/dyn/admin/*</url-pattern>
</servlet-mapping>

4、启动应用,以ip为127.0.0.1,port为8080示例,访问dyn控制界面地址为:127.0.0.0:8080/dyn/admin
```

开发DEMO：

```
@Component
public class Demo {
	private String isOk;

public String getIsOk() {
		return isOk;
	}

	public void setIsOk(String isOk) {
		this.isOk = isOk;
	}

	public String areYouOk() {
		StringBuilder sb = new StringBuilder("<p>\\t step into method areYouOk </p>");
		return sb.append(isOk).toString();
	}
}
```

注:

```
-方法不能含有入参,参数以全局变量传递

-输出支持html标记语言
```

#执行：
```

- 进入127.0.0.0:8080/dyn/admin

- 输入帐号密码 默认均为admin

- 点击进入Component Browser

- 找到刚刚写好的Demo点击进去

- 在Properties一栏点击类属性isOk

- 在New value下面的输入框输入你想要输入的文字然后点击Change Value按钮

- 返回到之前Demo的页面

- 在Methods下面找到你刚刚定义的方法areYouOk

- 点击Invoke Method执行该方法获得执行结果
```