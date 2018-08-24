# linux 安裝nodejs

0. 进入安装目录或资源目录
cd /home/app/software/

1. 下載node包
wget https://nodejs.org/dist/v8.11.3/node-v8.11.3-linux-x64.tar.xz

2. 解压
tar -xvf node-v8.11.3-linux-x64.tar.xz

3. 移动到node目录（重命名）
mv node-v8.11.3 node

4. 建立全局软链接
ln -S /home/app/software/node/bin/npm /usr/local/bin/
ln -S /home/app/software/node/bin/node /usr/local/bin/

5. 检测是否已安装

node -v

npm -v
