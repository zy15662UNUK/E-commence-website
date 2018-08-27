- 安装pycharm
- 安装mySOL和mySOL安装navicat
    - 安装navicat之后链接mysql时候出现1251 Client does not support authentication protocol requested by server; consider upgrading MySQL client
    - 参见 https://zhuanlan.zhihu.com/p/36087723
    - navicat新建数据库， 字符集选择utf8 -- UTF-8 Unicode， 否则无法显示中文。 排序规则选择utf8_general_ci
    - 然后就可以新建表了。表中每一个栏位代表一列。可以规定每一列的名称，类型 长度 小数点 不是null。还可以设置是否为主键
    - 数据库的几个概念：主键，外键，索引，唯一索引： https://blog.csdn.net/xrt95050/article/details/5556411
    - 主键： 数据表唯一的索引，查找的依据，不可重复

- 初始化系统：
    - 安装：
        `pip install djangorestframework`
        `pip install markdown django-filter`
    - 新建项目： 在pycharm中新建项目即可.注意虚拟环境要选第二个已有的环境
    - 运行项目直接点右上角的
    - 将setting.py中的数据库设置改为mysql的
        
        ```
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': 'mxshop',
                'USER': 'root',
                'PASSWORD': 'lLL1314520@@',
                'HOST': 'localhost',
                'PORT': '3306',
                'OPTIONS': {'init_command': 'SET default_storage_engine=INNODB;'}
            }
        }
        ``` 
        然后同时记得安装mysqlclient: 
        直接pip install 会报错，这时候需要在 
        https://www.lfd.uci.edu/~gohlke/pythonlibs/#mysqlclient下载mysqlclient-1.3.13-cp36-cp36m-win_amd64.whl
        然后 `pip install mysqlclient-1.3.13-cp36-cp36m-win_amd64.whl`就可以
        
       - 安装pillow `pip install pillow`
       - 项目结构：
            1. template: 存放所有的html文件
            2. db_tools: 外部脚本 用来初始化
            3. apps: 保存所偶的app，users也被放进去
            4. extra_apps: 存放第三方包，例如xadmin，jwt等。向修改源码，放在这就不会安装到系统中
       - mark apps 和 extra-apps作为source root。为后续import增加方便
       - setting时设置系统路径:
       
       ```
        import sys
        # Build paths inside the project like this: os.path.join(BASE_DIR, ...)
        BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
        sys.path.insert(0, BASE_DIR)
        sys.path.insert(0, os.path.join(BASE_DIR, 'apps'))
        sys.path.insert(0, os.path.join(BASE_DIR, 'extre_apps'))
       ```
       这样设置完可以直接就`import users`而不用 `import apps.users`
       不设置这个可能会导致cmd运行时候出错