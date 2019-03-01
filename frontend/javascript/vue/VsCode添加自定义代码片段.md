# vscode添加自定义代码片段

vscode已经是前端界最受欢迎的开发工具之一了。
插件丰富、界面简洁、小巧灵活，主题色丰富、还有很好的代码提示和扩展功能。

### 今天我们就学习一个非常好用的功能： **自定义代码片段**
> 像emmet一样能够打几个字符出现一堆内置的自己想要的代码一样的功能。 snippet

1、 打开vscode按住 command + p 会出现命令行   输入 「>snippet」      会出现 「配置用户代码片段  configure user snppets」 按回车
2、 然后会出现下拉选项，选择 「新建全局代码片段文件」， 这个时候就会出现新建文件，并且让您重命名后保存的界面。 起一个与代码关联的名字并回车就好了
3、 然后新文件里面就会有一些内置的代码和解释
```
// Place your global snippets here. Each snippet is defined under a snippet name and has a scope, prefix, body and 
// description. Add comma separated ids of the languages where the snippet is applicable in the scope field. If scope 
// is left empty or omitted, the snippet gets applied to all languages. The prefix is what is 
// used to trigger the snippet and the body will be expanded and inserted. Possible variables are: 
// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. 
// Placeholders with the same ids are connected.
// Example:
// "Print to console": {
// 	"scope": "javascript,typescript",
// 	"prefix": "log",
// 	"body": [
// 		"console.log('$1');",
// 		"$2"
// 	],
// 	"description": "Log output to console"
// }
```

Example后面是一个完整的代码段的内容

+ scope表示，在什么文件内会自动提示
+ prefix：表示您输入哪几个字符的时候会提示完整的代码段，也就是输入这个关键字回车就能把完整代码段输出
+ body： 就是您要完整输出的代码段
+ 您的代码段需要用字符串数组的方式表示，每一行代码就是一个数组中的一项， 如果有空行，就用   「"",」 表示并单独放一行，以保证输出您想要的格式排列
+『$1, $2』表示您想要在输出完代码段后，第一时间编辑哪个位置，编辑完后 敲tab键可以调到下一个$n位置，依次进行输入。

好了，方法讲完了，下面我们展示一下Vue常用的代码片段  和 vue + typescript 版本代码段
+ vue component
```json
{
    "Print to console": {
        "prefix": "vuet",
        "body": [
            "<template>",
            "",
            "</template>",
            "",
            "<script>",
            "export default {",
            "  name: '$0',",
            "",
            "  data () {",
            "    return {",
            "    }",
            "  },",
            "",
            "  methods: {}",
            "}",
            "</script>",
            "",
            "<style lang='' >",
            "",
            "</style>",
            ""
        ],
        "description": "vue file template init"
    }
}
```

+ vue + typescript
```json
{
	"Print to console": {
		"scope": "javascript,typescript",
		"prefix": "vuets",
		"body": [
				"<template>",
				"",
				"</template>",
				"",
				"<script lang='ts'>",
				"import { Component, Vue } from 'vue-property-decorator'",
				"@Component()",
				"export default class $0 extends Vue{",
					"",
				"}",
				"</script>",
				"",
				"<style lang='' >",
				"",
				"</style>",
				""
		],
		"description": "vue typescript Component template init"
	}
}
```

~ 您们还有什么好的代码片段，欢迎提issues
