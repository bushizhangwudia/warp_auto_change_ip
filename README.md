# warp_auto_change_ip

## Describtion
This is a script for warp.

You can use it to change your IP of warp which was blocked by Netflix.

## What's more
Most of the code comes from the streaming media detection script of lmc999, thank you very much!

At present, it is possible to lock the region (for example, if the Singapore IP is locked, the IP will be changed again after being assigned to the Japanese IP until the IP is Singaporean).

After the changeing is completed, it will continue to monitor (every 10s, you can change it by yourself), and you can put it on the screen for background execution.

If you need one-time use, change sleep 10 to break.

You'd better use the range of IPv4 of 193, it can better unlock the streaming media, if he is not clear, please use my script to install warp.

## How to use
```bash
wget https://github.com/luoxue-bot/warp_auto_change_ip/raw/main/warp_change_ip.sh && chmod +x warp_change_ip.sh && ./warp_change_ip.sh
```

PS：Will use the result of directly executing curl to Netflix as a benchmark.


注意：脚本需要挂在后台，可以使用screen
进入screen后运行脚本

设置：每隔多长时间检测一下ip的解锁是否有效
脚本36行            echo -e "Region: ${region} Done, monitoring..."
脚本37行            sleep 6
第37行的sleep 6可以改成任意时间，单位是秒，一般来说，1分钟即sleep 60就行，ip基本都可以存活一整天以上，不需要那么频繁的检测

（先进入screen）
wget https://github.com/luoxue-bot/warp_auto_change_ip/raw/main/warp_change_ip.sh && chmod +x warp_change_ip.sh && ./warp_change_ip.sh

如果之前没用安装过warp，首次运行脚本，根据提示"Is warp installed? [y/n] " 选择n，它会安装warp
然后再次运行脚本，选y

接下来，"Input the region you want(e.g. HK,SG):"
这个地方输入vps所在的国家名字，例如HK US SG UK
注意：一定要大写字母，小写不行
美国的小鸡不可能刷出新加坡的ip，所以填小鸡的真实位置即可

当显示“Region: XX Done, monitoring..."的时候，就说明ok了
从screen退出，运行流媒体检测脚本
bash <(curl -L -s check.unlock.media)
会看到“您的网络为: Cloudflare Warp”，ipv4可以解锁奈飞

和 "题字"(v2，trojan)    的使用相关：
先搭好 题字，确认是通的能上网。再运行这个，不需要额外的设置，直接就可以上网看奈飞了

开启warp后，ipv4的流量会被接管，这时无法申请域名的证书。停止，申请证书，再打开 即可

停止warp
systemctl stop wg-quick@wgcf
启动
systemctl start wg-quick@wgcf
重启
systemctl restart wg-quick@wgcf
