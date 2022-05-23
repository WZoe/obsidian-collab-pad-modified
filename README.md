# obsidian-collab-pad-modified


本 repo 基于 [GitHub - egradman/obsidian-etherpad-lite](https://github.com/egradman/obsidian-etherpad-lite) (master: 0cb6a05)修改，修复和调整了一些功能表现，并增加了一些我认为比较有用的功能。

This repo is an Obsidian plugin modified from [GitHub - egradman/obsidian-etherpad-lite](https://github.com/egradman/obsidian-etherpad-lite) (master: 0cb6a05) . I've changed some function behaviors and added some new features that I feel useful.

> This plugin uses an Etherpad-Lite server as a lightweight collaboration tool. Etherpad-Lite is a web-based collaborative editor. With this plugin, you can upload any note to an Etherpad-Lite server, share the URL, and allow others to collaboratively edit. The document remains in your vault. Each time it's opened, its contents will be replaced with the latest version from the Etherpad-Lite server.

## 功能调整和修复
- 现在本地文档以及对应 etherpad_id 等信息储存在一个额外的数据 json 中，而不是 yaml 头。
-  修改了 [GitHub - tomassedovic/etherpad-lite-client-js: JavaScript wrapper for the Etherpad Lite API](https://github.com/tomassedovic/etherpad-lite-client-js)，现在本地文档内容 push 到云端时的接口方法由 GET 改为 POST，数据不再暴露在请求头内，并且解除了文档大小的限制（原先上传文档不可以大于 8k）。
- 解决了原插件每次从云端 pull 到本地时，md 每一行末尾会多出几个空格，导致某些语法失效的问题。

## 新增功能
- 现在本地和云端互相同步内容时会检查目的文档是否有改动，只在可以安全覆盖的时候替换本地/远端文档内容，防止意外覆盖数据损失（但并不提供 diff 和 merge）。
- obsidian 本地文档有改动时会自动上传至云端。
- 增加本地文档解绑 etherpad_id 的命令。
- 增加手动安全 push/pull 和强制 push/pull 的命令。
- 在设置中查看当前同步中的文档。
- 同步中文档，状态栏会有绿色图标显示。

## Fixes and Modifications
- I have put the etherpad_id and local file mappings into a new data json. They are now not shown in the yaml headers.
- I did some modifications to [GitHub - tomassedovic/etherpad-lite-client-js: JavaScript wrapper for the Etherpad Lite API](https://github.com/tomassedovic/etherpad-lite-client-js), which made it possible to send the content of local files to the Etherpad server through POST instead of GET, so that data was not exposed in the request header. This modification also helped remove the file upload limitation of 8k.
- The problem that pulling from the server always appends extra whitespaces at the tail of each line was solved. This problem originally results in wrong rendering of some syntax like the code fence  `` `.

## New Helpful Features
- Now every time you push or pull the content, the plugin will check if there are modifications to the target document. To prevent unwanted full-text replacement or data loss, push/pull only happens automatically when it's safe. (BUT, diff and merge are not provided)
- Whenever you edit the local document, modifications  are pushed to the Etherpad server automatically under safe conditions.
- Added the command to remove the etherpad_id binding of a local file.
- Added commands to manually safe/force push/pull.
- You can now view all files that are in sync with the Etherpad server in Settings.
- You can now see a green note emoji at the status bar for files in sync.