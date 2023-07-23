# Vue的学习
## 一.Vue工程的项目结构
- 1.vite.config.js - 项目配置文件 基于vite的配置
- 2.package.json - 项目包文件 核心依赖项变成Vue3.x 和vite
- 3.main.js - 入口文件 createApp函数创建应用实例
- 4.app.vue -根组件 SFC但文件组件script-template-style 
    变化一：脚本script和模板template顺序调整
    变化二：模板template不再要求唯一跟元素
    变化三：脚本script添加setup标志支持组合式APi
- 5.index.html -单页入口 提供id为app的挂在点

## setup跟beforeCreate函数