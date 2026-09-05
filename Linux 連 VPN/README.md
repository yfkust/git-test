## L2TP/IPsec + 预共享密钥
```context
先装 L2TP/IPsec 插件:
sudo apt update
sudo apt install -y network-manager-l2tp network-manager-l2tp-gnome

安装完后重启 NetworkManager：

sudo systemctl restart NetworkManager

然后打开：设置 → 网络 → VPN → +

选择类似：Layer 2 Tunneling Protocol (L2TP)

身份這裡：
名稱：VPN 1
Gateway：202.203.170.2
username:kmstu_hejiangtao
密碼:

✔使用L2TP ephemeral源端口

然後點擊IPsec設置，將Enable IPsec tunnel to L2TP host ✔
填入預共享密鑰：vpncnlab
保存。

先端開vpn
然后终端确认你的 VPN 名字：

nmcli connection show

確認是否是自己的vpn名稱，例如 VPN 1，執行：

nmcli connection modify "VPN 1" ipv4.never-default yes

这句话的意思是不允许这个 VPN 成为整个系统的默认互联网出口

最後添加專用路由

nmcli connection modify "VPN 1" +ipv4.routes "172.31.252.0/24"

重新連接VPN
nmcli connection up "VPN 1"

檢查：
ip route get 172.31.252.54

應該顯示：172.31.252.54 dev ppp0 ...

再檢查普通公網
ip route get 1.1.1.1

这里不应该走 ppp0，而应该走你的 Wi-Fi 接口，例如：
dev wlp5s0

測試
学校服务器：

ssh 用户名@172.31.252.54

公网：

curl -I https://github.com
