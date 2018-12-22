# Annotion-Servlet3.0-demo
基于注解的方式配置Servlet （Servlet 3.0）的简单示例

### 配置javax.servlet.ServletContainerInitializer

1、在src目录创建META-INF，META-INF目录下创建services,在services目录下创建javax.servlet.ServletContainerInitializer文件

##### 配置引用接口ServletContainerInitializer

创建类MyWebConfig

~~~

package myWeb;

import javax.servlet.ServletContainerInitializer;
import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.HandlesTypes;
import java.util.Set;

@HandlesTypes(value = SpringWeb.class)
public class MyWebConfig implements ServletContainerInitializer {
    @Override
    public void onStartup(Set<Class<?>> set, ServletContext servletContext) throws ServletException {
        System.out.println("sadsa");
        for (Class<?> aClass : set) {
            SpringWeb o = null;
            try {
                o = (SpringWeb) aClass.newInstance();
                o.config();
            } catch (InstantiationException e) {
                e.printStackTrace();
            } catch (IllegalAccessException e) {
                e.printStackTrace();
            }
        }
    }
}

~~~

接口 + 实现类

~~~

package myWeb;

public interface SpringWeb {
    void config();
}


package myWeb;

public class SpringWebInitializer implements SpringWeb {
    //配置
    @Override
    public void config() {
        System.out.println("初始化");
    }
}

~~~

访问地址HttpServlet

~~~

@WebServlet("/login")
public class ServletWeb extends HttpServlet {
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Asdds");
    }
}

~~~



