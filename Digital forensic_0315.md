## __Digital Forensics__
- 攻擊者通常來自於內部
- Ping 他人的IP位置
    - TTL(Time to Live) -> 還可以被轉發處理多少次
    - TTL presents 本主機與被ping主機之距離
        - 當去Ping每一主機時，ICMP封包經過各個路由器轉發，TTL值就會減1
    - 可藉由出現幾次TTL來判別作業系統為Windows/Linux交叉
```
2^5  windows
2^6  linux
2^7  windows
2^8  244的話代表中間有12個節點 > 距離為12, linux
```

- 因為有些網路已經到IPV6，因此有時ping的時候要輸入-4，代表要ping他的IPV4的內容

- 探勘
    - 最大資料量(ping很多)
- 分析及準備攻擊
    - 資料量很多(雖比探勘時少，但試試看的到的) but 做不了任何事情

- 取得權限&維持存取
    - 等到攻擊者近來，他就成為取得權限的人(很難找到)，而攻擊者將 水平跳轉(Account to account/host to host) or 垂直提升權限(希望從Account跳到root/administrator等最高權限)  Host最高權限則是AD server(主控中心，可控制權限)


hping3 -v() -c(打幾次) -d(封包大小) -s(syn封包) -p(FTP port) --flood(前面的還沒傳完後面一樣可以繼續送)

- 遏制階段(短期&長期)
    - 有效阻止擴散(須從識別去做)
    - 拔網路線(錯誤)

    - **signature 需找出來，才能找出後續的蒐證
- 鑑識分析
    - IOC感染指標
    - IOA攻擊指標
    - 藉由此兩指標 就可以做全面清查
- 徹底根除階段:
    1. 加密(將要刪除的檔案鎖非常徹底-> 以file level方式做加密)
    2. logical wipe(邏輯抹除) -> 檔案碎紙機
    3. partition wipe磁區抹除 -> windows的格式化
        - fast: FAT(file allocation table) modified(只改掉表面的字，容易用還原軟體還原)
        - non-fast: 多一步壞軌的檢查
        windows在xp之前會做bad block check(壞軌檢查) 但沒有wipe整個資料的抹除 e.g. 若飯店有找人確定房間是否可住人 就是bad block check
        windows7以上的版本才有抹除
    4. physical破壞 -> 燒(運送、不完整)、溶(不完整)、碎(無塵室)、磁(作用-> 到磁盤上)

- 識別階段與派送病毒的時間不相同(最久2700天->8年)

- 圖表中的測試監控-> 監控IOC IOA
- 畫線-> 分享到準備(這次的經驗是下次的準備)
### __FTK Imager__
- File -> capture memory -> destination path(輸入另外一個位置，不要放在本機端，也不可以是c槽d槽) 
    - 檔名隨便取(學號+日期)
- File -> add evidence item
	- Create disk image -> source 原始物證(法院) (clone複本 for 備用)

### __Photo in ppt16__
- 5 6 垂直提升權限(權限跳脫) root, 水平擴展
    - 6 baseline-> IP, Account, File
    - 5 Meta data去描述檔案的敘述(檔案的時戳) 找的是檔案間的relationship
- 4 vulnerable(tool path) 修補
- 3 2 Prepare(過度暴露)
