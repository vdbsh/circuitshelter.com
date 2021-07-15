+++
date = "2021-07-15T03:19:47Z"
title = "VSCode snippet for Hugo post"
description = "Simple Hugo post generation with VSCode"
tags = ["code", "hugo", "vscode"]
+++

```json
{
	// Setup your timezone after ${CURRENT_SECOND}, default: "Z" (UTC)

	"Hugo Post": {
		"prefix": ["hugo"],
		"scope": "markdown",
		"body": [
			"+++",
			"date = \"${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE}T${CURRENT_HOUR}:${CURRENT_MINUTE}:${CURRENT_SECOND}Z\"",
			"title = \"$1\"",
			"description = \"$2\"",
			"tags = [\"$3\"]",
			"+++\n",
			"$0"],
		"description": "A Hugo post template"
	  }
}
```

# Guide
https://code.visualstudio.com/api/language-extensions/snippet-guide