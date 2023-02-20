```bash
#!/bin/bash

if [ $# -lt 2 ]

then

echo "Usage: ${prog##*/} sessName cmd1 cmd2 ..."

exit -1

fi

  

sessName=$1

shift

# 杀掉旧的同名session

screen -X -S $sessName quit > /dev/null 2>&1

  

# 创建session 
screen -dmS $sessName

  

until [ $# -eq 0 ]

do

    cmd=$1

    echo "exec cmd: $cmd"

    # stuff是命令参数，不能省略

    screen -S $sessName -p 0 -X stuff "$cmd"$'\n'

    shift;

done
```


```bash
#!/bin/bash 
screen -wipe # 免密登录的服务器 
sh createScreen.sh test-srv 'ssh 服务器IP' 'sudo -i' # 权限受限需要密码登录的服务器
sh createScreen.sh dev-srv 'ssh 服务器IP' '密码' '可选执行的命令'
```
