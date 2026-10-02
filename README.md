# SOC Alert Triage & Phishing Investigation Using Elastic SIEM

使用 Elastic SIEM 進行 SOC 警報分類與釣魚事件調查

---------

<h2>Outline｜專題簡介</h2>

Simulated SOC environment with real-world alert triage and incident response workflow. This scenario is a basic phishing event with a total of 5 alerts. SIEM tools available include Elastic, Splunk, and Sentinel. It also includes the analyst VM and TryDetectThis (a scenario-based version of VirusTotal).

模擬安全營運中心 (SOC) 環境，包含真實世界的警報分類和事件回應工作流程。本次情境為入門級釣魚事件，警報總數 5。SIEM工具可選 Elastic, Splunk, 以及 Sentinel。同時含有分析師 VM 及 TryDetectThis (情境版VirusTotal)

---------

<h2>👥 Employee Asset Inventory｜員工資產清單</h2>


| Name | Department | Email | Logged-in Host | IP Address |
|------|------------|-------|----------------|------------|
| Ethan Johnson | Editorial <br/>編輯部| e.johnson@thetrydaily.thm | win-3451 | 10.20.2.1 |
| Julia Garcia | Content <br/>內容部| j.garcia@thetrydaily.thm | win-3452 | 10.20.2.8 |
| Isabella Martinez | Marketing <br/>行銷部| i.martinez@thetrydaily.thm | win-3453 | 10.20.2.9 |
| Benjamin Lopez | Sales <br/>業務部| b.lopez@thetrydaily.thm | win-3454 | 10.20.2.10 |
| Henry Thomas | Operations <br/>營運部| h.thomas@thetrydaily.thm | win-3455 | 10.20.2.14 |
| Andrew Moore | IT <br/>資訊部| a.moore@thetrydaily.thm | win-3456 | 10.20.2.16 |
| Hannah Harris | Human Resources <br/>人力資源部 (HR)| h.harris@thetrydaily.thm | win-3457 | 10.20.2.17 |
| Tyler Young | Project Management <br/>專案管理| t.young@thetrydaily.thm | win-3458 | 10.20.2.24 |
| Grace Wright | Content <br/>內容部| g.wright@thetrydaily.thm | win-3459 | 10.20.2.27 |
| Jacob Carter | IT Support (Helpdesk)<br/>資訊技術支援部| j.carter@thetrydaily.thm | win-3460 | 10.20.2.30 |
| Chloe Scott | Content <br/>內容部| c.scott@thetrydaily.thm | win-3461 | 10.20.2.21 |
| Caleb Anderson | Content <br/>內容部| c.anderson@thetrydaily.thm | win-3462 | 10.20.2.13 |
| Charlotte Allen | Web Development <br/>網頁開發| c.allen@thetrydaily.thm | win-3463 | 10.20.2.25 |



---------
<h2>Investigation Workflow｜調查工作流程</h2>

[Alert Intake & Triage (警報接收與初判)]
* Review alert details and logic<br/>
  查看警報詳情和邏輯</b>
* Identify initial IOCs (IP, domain, URL)<br/>
  確定初始入侵指標 (IP 位址、網域名稱、URL)</b>
* Assign priority based on severity<br/>
  根據嚴重性分配優先級</b>
<br/>
<br/>

[Context Enrichment via SIEM (SIEM 擴展調查)]
* Query related logs<br/>
  查詢相關日誌<br/>
* Identify affected users and hosts<br/>
  識別受影響的使用者和主機<br/>
* Build activity timeline<br/>
  建構活動時間軸<br/>

* Escalation Decision<br/>
  是否升級

---------

<h2>Tools and Concepts Covered｜涵蓋工具與概念</h2>

<div align="center">
</p>

| Category 分類                          | Tools / Concepts 工具與概念                                     |
| -------------------------------------- | -------------------------------------------------------------- |
| Credential Access <br/>憑證存取         | Mimikatz, LSASS memory dumping <br/>Mimikatz、LSASS 記憶體轉儲  |
| Windows Internals Windows <br/>內部機制 | SAM database, registry hive <br/>SAM 資料庫、登錄單元            |
| Authentication <br/>驗證機制            | NTLM hash, plaintext credentials <br/>NTLM 雜湊值、明文憑        |
| Post-Exploitation <br/>攻擊後階段       | Credential dumping, privilege escalation <br/>憑證轉儲、提權     |
| Password Cracking <br/>密碼破解         | CrackStation, hash cracking                                     |
| Security Concepts <br/>安全概念         | Memory security, credential exposure <br/>記憶體安全、憑證洩露   |



</div>
<br/>



---------


<h2>Materials and Methods｜材料與方法</h2>

[Environment]
* Windows 10 (VM)</b>




[Tasks]
* Execute Mimikatz with Elevated Privileges (以系統管理員權限執行 Mimikatz)</b>
* Enable Debug Privileges (啟用 Debug 權限)</b>
* Extract Credentials from LSASS Memory (從 LSASS 記憶體提取憑證)</b>
* Enable Debug Privileges (啟用 Debug 權限)</b>
* Crack NTLM Hash to Recover Plaintext Password (破解 NTLM 雜湊還原明文密碼)</b>

---------

<h2>Initial Triage & Prioritization｜初步警報分類與優先排序</h2>

---------

<h2>Practice 實踐</h2>

<p align="center">
<b>Task 1: Execute Mimikatz with Elevated Privileges<br/> (以系統管理員權限執行 Mimikatz)</b><br/>
<img src="https://i.imgur.com/To4gugT.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<b>Task 2: Enable Debug Privileges<br/> (啟用 Debug 權限)</b><br/>
<img src="https://i.imgur.com/F67mJSx.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
* This command enables debug privileges, allowing access to sensitive system processes such as LSASS.<br/>此指令啟用 Debug 權限，使工具能存取如 LSASS 等敏感系統程序 <br/>
<br />
<br />
<b>Task 3: Extract Credentials from LSASS Memory<br/> (從 LSASS 記憶體提取憑證)</b><br/>
<img src="https://i.imgur.com/bxonO6d.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
* In modern Windows systems, plaintext credentials are no longer stored in LSASS memory by default <br/>due to security enhancements such as disabling WDigest authentication.<br/>在現代 Windows 系統中，由於安全性增強措施（例如停用 WDigest 驗證），預設不再將明文憑儲存在 LSASS 記憶體中 <br/>
<br />
<br />
<b>Task 4: Dump Password Hashes from SAM Database(從 SAM 資料庫擷取密碼雜湊)</b><br/>
<img src="https://i.imgur.com/skO1g6s.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<b>Task 5: Crack NTLM Hash to Recover Plaintext Password<br/> (破解 NTLM 雜湊還原明文密碼)</b><br/>
<img src="https://i.imgur.com/WuhzWHT.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
* This indicates that this password is not strong enough or is already present in public cracking databases.<br/>這表示該密碼強度不夠，或已經存在於公開的破解資料庫中 <br/>
<br />
<br />



---------

<h2>Results 專題結論</h2>

This project demonstrated how credentials can be extracted from a compromised Windows system using Mimikatz. By accessing LSASS memory and the SAM database, sensitive authentication data such as NTLM hashes were successfully obtained.

本專題展示了如何使用 Mimikatz 從已入侵的 Windows 系統中提取憑證。透過存取 LSASS 記憶體與 SAM 資料庫，成功取得 NTLM 雜湊等敏感驗證資訊。

Although plaintext passwords were not initially available (displayed as Password: (null)), this behavior aligns with modern Windows security mechanisms where cleartext credentials are not stored by default.

雖然初始階段未取得明文密碼（顯示為 Password: (null)），但這符合現代 Windows 的安全設計，即預設不在記憶體中儲存明文憑證。

To further validate the attack workflow, a controlled weak credential was introduced, allowing successful cracking of the NTLM hash using CrackStation and recovery of the plaintext password.

為了驗證攻擊流程，本專題建立弱密碼帳號，並成功透過 CrackStation 破解 NTLM 雜湊並還原明文密碼。

This confirms that credential exposure remains a critical risk, regardless of whether plaintext passwords are directly accessible.

這證實即使無法直接取得明文密碼，憑證外洩仍然構成重大安全風險。


---------

<h2>Security Insight 安全洞察</h2>

Even when plaintext passwords are not stored in memory, attackers can still extract credential artifacts such as NTLM hashes and Kerberos-related data from LSASS.

即使系統未儲存明文密碼，攻擊者仍可從 LSASS 中提取 NTLM 雜湊與 Kerberos 憑證資料。

The successful cracking of weak credentials highlights the importance of strong password policies. Passwords that are short or commonly used are highly vulnerable to dictionary-based attacks.

成功破解弱密碼顯示強式密碼政策的重要性。短密碼或常見密碼極易遭字典攻擊破解。

Mitigating credential dumping attacks requires a combination of defensive measures, including:

防禦憑證提取攻擊需採取多層防護措施，包括：

* Restricting administrative privileges<br/>
  限制系統管理員權限
  
* Enabling LSASS protection mechanisms<br/>
  啟用 LSASS 保護機制

* Monitoring abnormal process access to LSASS<br/>
  監控對 LSASS 的異常存取行為

* Enforcing strong password and credential policies<br/>
  強制實施強式密碼與憑證管理政策


---------

<h2>Reference 參考</h2>

[UniSQ] [CSC6101 - Penetration Testing](https://handbook-guide.unisq.edu.au/course/2026/CSC6101)<br/>
[EC-Council] [Certified Ethical Hacker](https://aspen.eccouncil.org/Home)<br/>
<br/>
