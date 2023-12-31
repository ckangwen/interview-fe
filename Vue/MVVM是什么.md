#Vue 


M（Model）：模型
负责存储和管理数据，负责与服务器交互

V（View）：视图
用户看到的交互界面，负责显示数据并向视图模型发送用户操作的请求

VM（View Model）：视图模型
负责从模型中获取数据并将其转换为视图可以使用的格式
将用户的操作转换为模型可以理解的格式


**解决的问题**
- 分离关注点：将应用程序的核心业务逻辑与用户界面分离开，使得开发人员能够更加关注与业务逻辑的实现
- 提高可维护性：将应用程序的不同部分分离开来，使得代码的组织更加清晰，从而提供程序的可维护性


**Vue 体现MVVM的地方**
- 数据绑定：视图与模型之间的同步变的非常容易
- 模板语法：能够将模型中的数据绑定到视图上
- 计算属性与侦听器：处理复杂逻辑，将逻辑分离出来，让视图更加明了
- 组件化：将整个应用拆解为更小、更简单的组件，更容易组织代码和管理代码的复杂性