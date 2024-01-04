# auto_fork_update
fork自动更新

两种方法
1、apps pull
2、action
两种方法简单分析：
1、方法1更简洁
2、方法2对 部分二次fork修改的仓库会无效，此时只能用方法1
3、方法2的同步时间可以自行调节


1、apps pull
访问地址：https://github.com/apps/pull

![image](https://github.com/tvfuns/auto_fork_update/assets/5485787/54561853-9f9a-4296-b225-a294c70c8aa8)

![image](https://github.com/tvfuns/auto_fork_update/assets/5485787/f68ced36-8483-49d6-a917-5d22796cde5f)

![image](https://github.com/tvfuns/auto_fork_update/assets/5485787/1320d0ab-b41e-4b55-bc76-5a7cb68f8875)

![image](https://github.com/tvfuns/auto_fork_update/assets/5485787/e305f245-cac6-43a1-9b81-28b8d8d84882)
上游仓库改变，过了几个小时后，自动同步成功

-------------------------------------------------------------------------------------------------------
2、action

先要检查自己的待同步仓库设置
![image](https://github.com/tvfuns/auto_fork_update/assets/5485787/d994e594-0478-4b76-9484-81ce86d595c4)


name: Sync Fork

on:

  schedule:
  
    - cron: '*/30 * * * *' # every 30 minutes
    
  workflow_dispatch: # 有这个才能手动点运行

jobs:
  sync:

    runs-on: ubuntu-latest

    steps:
      - uses: tgymnich/fork-sync@v1.8
        with:
          #token: ${{ secrets.PERSONAL_TOKEN }}    #发现并不需要
          owner: hjdhnx    #上游仓库所有者
          repo: dr_py    #上游仓库名
          base: main    #上游分支名
          head: main    #本仓库分支名

