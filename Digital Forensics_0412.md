## __Digital Forensics_0412__##
- ISO 27037 -> 給企業看的(做企業經營、永續價值)
- ACPO -> for警調單位，但沒有很大強制力
- NIJ美國司法部 -> 給政府機關看的(責任寫比較清楚)
```
考!!!!
共通點(pdf2)
1. 確保證據不受外力影響(被汙染) -> pdf p8(證據能力-> 成為*證據的資格*，須合法取得)
2. 鑑識人員須經過專業訓練(資訊人員不等於資安人員)
3. 確保證據鏈紀錄完備(與第一條相似)

證據力/證明力 -> 事實的真實程度

證據監管鏈COC -> 扣押保存傳輸分析(evidence's handover) 只要在保存過程中有被竄改，監管鏈就會斷掉(須不受外力影響)
```
- 數位證據處理準則
    > p5
```
1. 記錄所有動作
靜態資訊 -> 硬碟的序號
連續動作是用"攝影機"
蒐證環境和標的主機都是紀錄範圍
2. 確認證據與原始證據的"關聯"
```
- $ standard information & $filename -> windows的兩組時間 (windows forensic analysis)
- ISO27037  (pdf p.10) -> 證據能力
    1. evidence identification
    2. collection(蒐集)
    3. aquisition(擷取)
    4. preservation(保存)
- 蒐證現場作業流程 (pdf p.12)
    - **要蒐集揮發性資料    
    - 邏輯性資料=非揮發性資料
        1. 做RAID
        2. Cloud
    - 因為正常關機會導致數位證據回寫硬碟的問題，因此傾向使用`斷電`來臨時中斷它

- 位元串流複製方式(Bit-Stream Duplicate/ bit by bit stream copy) (pdf p.20)
    - 通常會用image做分析，而不是clone的(因為若有中毒的，image只要沒打開就不會中毒)
- HASH完整性驗證(五次) -> 完整性的查驗 => 成為證據的能力
    - MD5
    - SHA1

- 製作證據映像檔之途徑與工具(pdf p.24) => p.29 用哪個設備途徑去製作會遇到什麼問題
    - USB
    - 網路
- 驗證方式(pdf p.26 三個考題)
    - 黑色 -> CRC檢查碼 做image時先做完CRC，才會放HASH
    - **驗證時 先看HASH，再一個個看CRC
    - **MD5&SHA1 -> 完整性驗證
    - MD5 -> 128 bits ; SHA1 -> 160 bits