mininet 基本建構方式
執行mininet: sudo mn --topo single,3 --mac --switch ovsk --controller remote(,ip=xxx.xxx.xxx.xxx,port=xxxx) -x 
(-x 讓xterm可以執行 讓我們可以對各個拓樸上的node操作)

s1:
觀看switch狀態: ovs-vsctl show
觀看switch連接狀況: ovs-dpctl show
設定switch OpenFlow版本: ovs-vsctl set Bridge s1 protocols=OpenFlow13
觀看switch的flow table: ovs-ofctl -O OpenFlow13 dump-flows s1

建構controller c0:
ryu-manager --verbose ryu.app.simple_switch_13
(simple_switch_13可以建構OF13版本的controller address:127.0.0.1(default))

h1, h2, h3:
監聽各個host: tcpdump -en -i h1-eth0

mininet:
host互ping: h1 ping -c1 h2 

### 當要改變ryu的檔案內容時
    sudo python setup.py install
