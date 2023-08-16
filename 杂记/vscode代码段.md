### python

```json
{
	// Place your snippets for python here. Each snippet is defined under a snippet name and has a prefix, body and 
	// description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
	// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
	// same ids are connected.
	// Example:
	// "Print to console": {
	// 	"prefix": "log",
	// 	"body": [
	// 		"console.log('$1');",
	// 		"$2"
	// 	],
	// 	"description": "Log output to console"
	// }
	"python main func": {
		"prefix": "name",
		"body": [
			"if __name__ == \"__main__\":",
			"\t",
			"\t",
			"\tpass"
		],
		"description": "python main func"
	},
	"os.path.join": {
		"prefix": "opj",
		"body": [
			"os.path.join($0)",
		],
		"description": "os.path.join"
	},
	"with open file": {
		"prefix": "wop",
		"body": [
			"with open($0, 'r', encoding='utf-8') as f:",
		]
	},
	"debug": {
		"prefix": "db",
		"body": [
			"# -----------debug start-----------",
			"$0",
			"# -----------debug end-----------",
		]
	},
	"HEADER comment":{
        "prefix": "header",
        "body": [
			// "#!/usr/bin/env python",
			"# -*- encoding: utf-8 -*-",
			"\"\"\"",
			"\t@File    :   $TM_FILENAME",
			"\t@Time    :   $CURRENT_YEAR/$CURRENT_MONTH/$CURRENT_DATE $CURRENT_HOUR:$CURRENT_MINUTE:$CURRENT_SECOND",
			"\t@Author  :   mkid ",
			"\t@Version :   1.0",
			"\t@Note    :   $1",
			// "@Contact :   betterWL@hotmail.com",
			// "@License :   (C)Copyright 2017-2018, Liugroup-NLPR-CASIA",
			// "@Desc    :   None",
			"\"\"\"",
			"",
			"$2"
		],
    },
	"local function comment": {
		"prefix": "ln",
		"body": [
			"\"\"\"",
			"${1:Description}",
			"Args:",
			"\t${2:arg1}: ${3:Description}",
			"Returns:",
			"\t${4:Description}",
			"\"\"\""
		]
	}
}
```

