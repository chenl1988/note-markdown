## babel 原理

- ES6、7 代码输入 -> babylon 进行解析 -> 得到 AST（抽象语法树） -> plugin 用 babel-traverse 对 AST 树进行遍历编译 -> 得到新的 AST 树 ->用 babel-generator 通过 AST 树生成 ES5 代码
