phabricator
==============================

安装
------------------------------

密码： SEc0bvVZ3!T

安装

./bin/config set mysql.pass pe

phd 代码分析
------------------------------

/home/ywb/src/php/phabricator/src/applications/daemon/management/PhabricatorDaemonManagementWorkflow.php

/home/ywb/src/php/libphutil/src/parser/argument/PhutilArgumentParser.php

PhutilArgumentParser::parseWorkflows($workflows)

PhabricatorDaemonManagementWorkflow
    |-[+] PhabricatorDaemonManagementDebugWorkflow(PhabricatorDaemonManagementDebugWorkflow)
    |-[+] PhabricatorDaemonManagementLaunchWorkflow(PhabricatorDaemonManagementLaunchWorkflow)
    |-[+] PhabricatorDaemonManagementListWorkflow(PhabricatorDaemonManagementListWorkflow)
    |-[+] PhabricatorDaemonManagementLogWorkflow(PhabricatorDaemonManagementLogWorkflow)
    |-[+] PhabricatorDaemonManagementReloadWorkflow(PhabricatorDaemonManagementReloadWorkflow)
    |-[+] PhabricatorDaemonManagementRestartWorkflow(PhabricatorDaemonManagementRestartWorkflow)
    |-[+] PhabricatorDaemonManagementStartWorkflow(PhabricatorDaemonManagementStartWorkflow)
    |-[+] PhabricatorDaemonManagementStatusWorkflow(PhabricatorDaemonManagementStatusWorkflow)
    |-[+] PhabricatorDaemonManagementStopWorkflow(PhabricatorDaemonManagementStopWorkflow)
    `-[+] 0(PhutilHelpArgumentWorkflow)

/home/ywb/src/php/phabricator/src/applications/daemon/management/
    
实际运行：PhabricatorDaemonManagementStartWorkflow

phd.pid-directory = /var/tmp/phd/pid

{
   "pid" : 18572,
   "daemons" : [
      {
         "pid" : 18573,
         "id" : "18572:j53m55",
         "config" : {
            "argv" : [],
            "autoscale" : [],
            "class" : "PhabricatorRepositoryPullLocalDaemon"
         }
      },
      {
         "pid" : 18574,
         "config" : {
            "argv" : [],
            "class" : "PhabricatorTriggerDaemon",
            "autoscale" : []
         },
         "id" : "18572:cku73i"
      },
      {
         "pid" : 18577,
         "id" : "18572:c2cyci",
         "config" : {
            "autoscale" : {
               "pool" : 4,
               "reserve" : 0,
               "group" : "task"
            },
            "class" : "PhabricatorTaskmasterDaemon",
            "argv" : []
         }
      }
   ],
   "start" : 1437269309,
   "config" : {
      "log" : "/var/tmp/phd/log/daemons.log",
      "piddir" : "/var/tmp/phd/pid",
      "daemons" : [
         {
            "class" : "PhabricatorRepositoryPullLocalDaemon"
         },
         {
            "class" : "PhabricatorTriggerDaemon"
         },
         {
            "autoscale" : {
               "pool" : 4,
               "group" : "task",
               "reserve" : 0
            },
            "class" : "PhabricatorTaskmasterDaemon"
         }
      ],
      "daemonize" : true
   }
}

PhabricatorDaemonManagementWorkflow::executeDaemonLaunchCommand

/home/ywb/src/php/libphutil/src/future/exec/ExecFuture.php
/home/ywb/src/php/libphutil/src/future/Future.php
ExecFuture
cwd = /home/ywb/src/php/phabricator/scripts/daemon/
Future::resolve
参数从 stdin 传入
exec ./phd-daemon 

./phd status
10  19508:7pobvk localhost 19508    Jul 19 2015, 2:30:29 AM PhabricatorRepositoryPullLocalDaemon 
11  19508:zvamnn localhost 19508    Jul 19 2015, 2:30:29 AM PhabricatorTriggerDaemon             
12  19508:lczuzq localhost 19508    Jul 19 2015, 2:30:29 AM PhabricatorTaskmasterDaemon          

启动 daemon: launch_daemon.php
PhutilDaemonHandle::startDaemonProcess

/home/ywb/src/php/phabricator/src/infrastructure/daemon/workers/PhabricatorTaskmasterDaemon.php
/home/ywb/src/php/phabricator/src/infrastructure/daemon/workers/PhabricatorTriggerDaemon.php
/home/ywb/src/php/phabricator/src/applications/repository/daemon/PhabricatorRepositoryPullLocalDaemon.php
基类：
/home/ywb/src/php/phabricator/src/infrastructure/daemon/PhabricatorDaemon.php
/home/ywb/src/php/libphutil/src/daemon/PhutilDaemon.php
