94imm爬虫修复版，新增自动下载视频脚本，演示网站：<https://imeizi.me>，保姆级教程：<https://v2raytech.com/imeizi-tutorial/>

# 安装说明
参数配置
> 配置文件为根目录下的config.py
```python
# 数据库信息，一键脚本自动添加
mysql_config = {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '94imm',
        'USER': '94imm',
        'PASSWORD': '94imm',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
# 数组形式，可以添加多个域名
allow_url=["imeizi.me","127.0.0.1"]
# 缓存超时时间，服务器性能好可缩短此时
cache_time=300
# 使用的模板（暂时开放一个）
templates="zde"
# 网站名
site_name="爱妹子"
# 一键脚本自动添加
site_url = "https://imeizi.me"
# 网站关键词
key_word = "爱妹子,美女写真,性感美女,美女图片,高清美女"
# 网站说明
description = "每日分享最新最全的美女图片和高清性感美女图片，性感妹子、日本妹子、台湾妹子、清纯妹子、妹子自拍以及街拍美女图片"
# 底部联系邮箱
email = "admin@imeizi.me"
# 网站调试模式
debug = False
# 友联
friendly_link = [{"name":"网络跳跃","link":"https://hijk.art"},{"name":"V2ray科技","link":"https://v2raytech.com"}]
```

# 使用说明
> 进入项目根目录
```shell
启动网站
./run.sh s
关闭网站
./run.sh stop
重启网站
./run.sh r
清空网站缓存（使所做的修改立即生效）
./run.sh c
```
> 项目模板目录templates，base.html中可直接添加统计代码

# 手动安装说明
> 项目依赖python3.6 mysql5.6

```
git clone https://github.com/hijkpw/94imm.git
cd 94imm
vi config.py  #参照配置说明修改
vi uwsgi.ini  #修改uwsgi配置
```
如需使用反向代理，在nginx.conf中添加如下server段
```
server {
    listen       80;
    server_name  localhost; # 网站域名

    root /var/www/94imm;
    location / {
        proxy_pass http://127.0.0.1:8000;
    }
    location /static {
        expires max;
    }

    location /favicon.ico {
        root /var/www/94imm/static;
    }
}
```

***补充***
```
install.sh 不适用于 Debian 系列，也就是手动操作
apt install -y mariadb-server python3 python3-setuptools nginx

pip3 install -r requirements.txt 安装过程有个模块缺少依赖搜索解决
重新装了补充
正如这里提到的，你应该这样做：
sudo apt-get install python3-dev default-libmysqlclient-dev build-essential
Debian / Ubuntu
sudo yum install python3-devel mysql-devel
红帽 / CentOS
之后就做 pip install mysqlclient

手动替换dj_pagination的pagination.html 这里是3.8版本路径有点区别
rm -f /usr/local/lib/python3.8/dist-packages/dj_pagination/templates/pagination/pagination.html
cp templates/zde/pagination.html /usr/local/lib/python3.8/dist-packages/dj_pagination/templates/pagination/pagination.html

run.sh 我的环境报错，需要删除function声明，原因不明,到这里就妥啦
nginx配置按需要弄

附一些能用到的命令
查看服务器 8000 端口的占用情况： lsof -i:8000
内网请求下数据确认OK： curl http://127.0.0.1:8000
```
