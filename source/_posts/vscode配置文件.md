//  {
//   "editor.fontSize": 20,
//   // vscode默认启用了根据文件类型自动设置tabsize的选项
//   "editor.detectIndentation": false,
//   // 重新设定tabsize
//   "editor.tabSize": 2,
//   // #每次保存的时候自动格式化
//   "editor.formatOnSave": true,
//   // #每次保存的时候将代码按eslint格式进行修复
//   "eslint.autoFixOnSave": true,
//   // 添加 vue 支持
//   "eslint.validate": [
//     "javascript",
//     "javascriptreact",
//     {
//       "language": "vue",
//       "autoFix": true
//     }
//   ],

//   // #让prettier使用eslint的代码格式进行校验
//   "prettier.eslintIntegration": true,
//   // #去掉代码结尾的分号
//   "prettier.semi": false,
//   // #使用带引号替代双引号
//   "prettier.singleQuote": true,
//   // #让函数(名)和后面的括号之间加个空格
//   "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
//   // #这个按用户自身习惯选择
//   "vetur.format.defaultFormatter.html": "js-beautify-html",
//   // #让vue中的js按编辑器自带的ts格式进行格式化
//   "vetur.format.defaultFormatter.js": "vscode-typescript",
//   "vetur.format.defaultFormatterOptions": {
//     "js-beautify-html": {
//       "wrap_attributes": "force-aligned"
//       // #vue组件中html代码格式化样式
//     }
//   },
//   // 格式化stylus, 需安装Manta's Stylus Supremacy插件
//   // "stylusSupremacy.insertColons": false, // 是否插入冒号
//   // "stylusSupremacy.insertSemicolons": false, // 是否插入分好
//   // "stylusSupremacy.insertBraces": false, // 是否插入大括号
//   // "stylusSupremacy.insertNewLineAroundImports": false, // import之后是否换行
//   // "stylusSupremacy.insertNewLineAroundBlocks": false,
//   // "team.showWelcomeMessage": false,
//   // "workbench.iconTheme": "vscode-icons",
//   // "terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
//   // "files.autoSave": "onFocusChange",
//   // "terminal.integrated.rendererType": "dom",
//   // "editor.renderIndentGuides": false, // 两个选择器中是否换行


//   //添加每个文件的开头注释   ctrl+ait+i  自动添加创建者信息
//   "fileheader.customMade": {
//     "Author": "王永斌",
//     "Date": "Do not edit",
//     // "LastEditors": "OBKoro1",
//     "LastEditTime": "Do not edit",
//     // "Description": "",
//   },
//   "workbench.iconTheme": "vscode-icons",
//   "editor.renderIndentGuides": false,
//   "team.showWelcomeMessage": false,
//   "files.autoSave": "onFocusChange",
//   "terminal.integrated.rendererType": "dom",
//   "[html]": {
//     "editor.defaultFormatter": "vscode.html-language-features"
//   }


// }
{
  "workbench.startupEditor": "newUntitledFile",
  "terminal.integrated.shell.windows": "C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
  "prettier.singleQuote": true,
  "prettier.semi": false,
  "prettier.useTabs": true,
  "prettier.printWidth": 120,
  "eslint.autoFixOnSave": true,
  "eslint.validate": [
    //开启对.vue文件中错误的检查
    "javascriptreact",
    {
      "language": "javascript",
      "autoFix": true
    },
    {
      "language": "html",
      "autoFix": true
    },
    {
      "language": "vue",
      "autoFix": true
    }
  ],
  "git.autofetch": true,
  "emmet.triggerExpansionOnTab": true,
  "emmet.includeLanguages": {
    "vue-html": "html",
    "vue": "html"
  },
  "vetur.validation.template": false,
  "editor.tabSize": [2, 4],
  "window.zoomLevel": 0,
  "workbench.iconTheme": "vscode-icons",
  "editor.fontSize": 20,
  "files.autoSave": "onFocusChange",
  "workbench.sideBar.location": "left",
  "workbench.activityBar.visible": true,
  "window.menuBarVisibility": "default",
  "team.showWelcomeMessage": false,
  "guides.enabled": false,
  "editor.suggestSelection": "first",
  "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
  "[html]": {
    "editor.defaultFormatter": "vscode.html-language-features"
  },
  "[javascript]": {
    "editor.defaultFormatter": "remimarsal.prettier-now"
  },
  "terminal.integrated.rendererType": "dom"
}