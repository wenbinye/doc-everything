gerrit
==============================

安装
------------------------------


下载 gerrit-2.*.war ，运行命令 ::

   sudo adduser gerrit2
   sudo su gerrit2
   java -jar gerrit.war init -d /home/gerrit2/site

下载太慢的话 ::

   cp bcprov-jdk16-144.jar /home/gerrit2/site/lib

etc/gerrit.config ::

    [gerrit]
    	basePath = git
    [database]
    	type = h2
    	database = db/ReviewDB
    [auth]
    	type = HTTP
    [sendemail]
    	smtpServer = localhost
    [container]
    	user = gerrit2
    	javaHome = /usr/lib/jvm/java-7-openjdk-amd64/jre
    [sshd]
    	listenAddress = *:29418
    [httpd]
    	listenUrl = http://*:8081/
    [cache]
    	directory = cache

nginx 配置 ::

    # -*- mode:nginx -*-
    server {
        listen 80;
        server_name gerrit.chaozhuo.in;
    
        location / {
            auth_basic "Restricted";
            auth_basic_user_file /home/ywb/local/etc/htpasswd;
            proxy_pass        http://127.0.0.1:8081;
            proxy_set_header  X-Forwarded-For $remote_addr;
            proxy_set_header  Host $host;
        }
    }
  
使用 hooks
------------------------------

hooks/ref-updated ::

    #!/usr/bin/env perl
    use strict;
    use warnings;
    use POSIX qw/strftime/;
    use Getopt::Long qw(:config pass_through);
    my ($oldrev, $newrev, $refname, $project);
    
    GetOptions(
        "oldrev=s" => \$oldrev,
        "newrev=s" => \$newrev,
        "refname=s" => \$refname,
        "project=s" => \$project,
    );
    
    my $url = "http://192.168.1.161/gitlab-hook.php";
    my $file = '/tmp/git-hooks.log';
    open(my $fh, ">>", $file) or die "Can't create file $file: $!";
    log_it("argv: " . join(" ", @ARGV));
    
    my $repo = 'git@gitlab.chaozhuo.net:chaozhuo/' . $project . ".git";
    my $msg = qq|{"ref": "$refname", "repository": {"url": "$repo"}}|;
    system("wget -q --post-data='$msg' $url -O /dev/null");
    
    sub log_it {
        print {$fh} strftime('%F %T', localtime), " ", @_, "\n";
    }
