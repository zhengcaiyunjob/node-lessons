# webpack打包优化-第二种方式：利用CommonsChunkPlugin
##通过分拆代码，来实现js分拆的目的：参考官方文档：https://github.com/webpack/webpack/tree/webpack-1/examples/multiple-commons-chunks
###webpack配置文件如下所示：
```javascript
var path = require("path");
var CommonsChunkPlugin = require("../../lib/optimize/CommonsChunkPlugin");
module.exports = {
    entry: {
        pageA: "./pageA",
        pageB: "./pageB",
        pageC: "./pageC",
        adminPageA: "./adminPageA",
        adminPageB: "./adminPageB",
        adminPageC: "./adminPageC",
    },
    output: {
        path: path.join(__dirname, "js"),
        filename: "[name].js"
    },
    plugins: [
        new CommonsChunkPlugin("admin-commons.js", ["adminPageA", "adminPageB"]),
        new CommonsChunkPlugin("commons.js", ["pageA", "pageB", "admin-commons.js"], 2),
        new CommonsChunkPlugin("c-commons.js", ["pageC", "adminPageC"]),
    ]
}
```
