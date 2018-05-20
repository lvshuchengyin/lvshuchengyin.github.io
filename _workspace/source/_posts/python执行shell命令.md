title: python执行shell命令
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 11:26:00
---
### popen
~~~ python
def _command_execute(command_s):
    """执行命令，例如command_s=['ls', '-al']"""
    sp = Popen(command_s, stdout=PIPE, stderr=STDOUT, close_fds=True)
    output_content = ''
    for line in iter(sp.stdout.readline, b''):
        output_content += line
 
        if len(output_content) > 1024 * 4:
            break
    sp.wait()
    return int(sp.returncode), output_content
~~~