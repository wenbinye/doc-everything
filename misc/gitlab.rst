gitlab ci
------------------------------

1. 在首页或者 Admin Area 左侧菜单中 Continuous Integration

2. Add project to CI

3. 添加 runner ::

   docker pull gitlab/gitlab-runner

在 docker-compose.yml 中添加 ::

    runner:
      image: gitlab/gitlab-runner
      restart: always
      volumes:
        - /var/run/docker.sock:/var/run/docker.sock
        - ./runner-config:/etc/gitlab-runner

注册 runner ::

    docker exec -it gitlab_runner_1 gitlab-runner register

build.sh

if [[ -d $'/builds/wenbinye/scratch/.git' ]]; then
echo $'\x1b[32;1mFetching changes...\x1b[0;m'
cd $'/builds/wenbinye/scratch'
git clean -fdx
git reset --hard > /dev/null
git remote set-url origin $'http://gitlab-ci-token:b87dd87c2ab9320b7e4af3800eadb0@172.17.42.1:10080/wenbinye/scratch.git'
git fetch origin
else
echo $'\x1b[32;1mCloning repository...\x1b[0;m'
rm -rf $'/builds/wenbinye/scratch'
mkdir -p $'/builds/wenbinye/scratch'
git clone $'http://gitlab-ci-token:b87dd87c2ab9320b7e4af3800eadb0@172.17.42.1:10080/wenbinye/scratch.git' $'/builds/wenbinye/scratch'
cd $'/builds/wenbinye/scratch'
fi
echo $'\x1b[32;1mChecking out e699787a as master...\x1b[0;m'
git checkout -qf e699787a1eefae7fe14227688f7f09e5054159ce

echo

echo $'\x1b[32;1m$ composer install\x1b[0;m'
composer install
echo $'\x1b[32;1m$ phpunit tests\x1b[0;m'
phpunit tests

