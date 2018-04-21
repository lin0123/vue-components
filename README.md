# vue-components
a series of usual vue components

## popup目录下
### CommonMovePopup.vue组件
#### 说明: 只基于vue的pc端弹出菜单可移动组件, 当在弹出框内点击, 可随着鼠标的移动而移动.
#### 引入方式, 在需要使用的模块 : import 自定义名称 from '组件存放的路径';
#### 参数说明:
1. v-model: boolean 类型, 设置为true显示, false隐藏;
2. selfClass: String 类型, 自定义弹出框样式;
3. 插槽name="delete-crross", 自定义删除按钮;
4. 插槽name="title", 自定义名称;
5. 插槽name="content", 自定义弹出框内容;
