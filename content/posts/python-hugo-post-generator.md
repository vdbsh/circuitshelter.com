+++
date="2021-07-24T14:53:09Z"
title="Hugo post generator"
description="Generating hugo posts with Python"
categories=["code"]
tags=["code", "python", "hugo", "blog"]
cover=""
+++

This python script will generate valid markdown template for hugo post and opens it in associated text editor. It's cross-platform and have no dependencies.

```python
#!/usr/bin/env python3

from datetime import datetime, timezone
from platform import system
from subprocess import call
from sys import argv

hugo_posts_dir = '/home/user/blog/content/posts'

if __name__ == '__main__':
    post_file = path.join(hugo_posts_dir, 
                          f'{argv[1].lower().replace(" ", "-")}.md')
    now = datetime.now(tz=timezone.utc)
    timestamp = now.strftime('%Y-%m-%dT%H:%M:%SZ')
    
    with open(post_file, 'w') as f:
        f.write(f'+++\n'
                f'date="{timestamp}"\n'
                f'title=""\n'
                f'description=""\n'
                f'categories=[]\n'
                f'tags=[]\n'
                f'cover=""\n'
                f'+++\n\n')

    os_id = system().lower()

    if 'windows' in os_id:
        call(('start', post_file))
    elif 'osx' in os_id or 'darwin' in os_id:
        call(('open', post_file))
    else:
        call(('xdg-open', post_file))
```
Also check out how to make [VSCode snippet for Hugo post](hugo-post-vscode-snippet).