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


</p>

| Category (分類) | Tools / Concepts (工具 / 概念) |
| --- | --- |
| SOC Operations <br/>SOC 安全營運 | Alert triage, alert ownership, case investigation <br/>警報分類、警報接手、案例調查 |
| SIEM Investigation <br/>SIEM 調查 | Elastic SIEM |
| Security Telemetry <br/>安全遙測資料 | Email logs, Firewall logs, ModSecurity Audit Logs <br/>電子郵件日誌、防火牆日誌、ModSecurity 稽核日誌 |
| Alert Prioritization <br/>警報優先排序 | Risk-based prioritization, severity assessment <br/>風險導向優先排序、嚴重度評估 |
| Event Correlation <br/>事件關聯 | Cross-alert correlation, email-to-network correlation <br/>跨警報關聯、郵件與網路事件關聯 |
| Asset Context <br/>資產情境 | Employee and workstation asset inventory <br/>員工與工作站資產清單 |
| Threat Intelligence <br/>威脅情報 | TryDetectThis, IP reputation analysis <br/>TryDetectThis、IP 信譽分析 |
| Indicators of Compromise <br/>入侵指標 | IP addresses, domains, URLs, sender addresses <br/>IP 位址、網域、URL、寄件者位址 |
| Phishing Analysis <br/>釣魚郵件分析 | Brand impersonation, lookalike domains, URL shortening, social engineering <br/>品牌仿冒、相似網域、短網址、社交工程 |
| Incident Classification <br/>事件分類 | True Positive, False Positive <br/>真陽性、誤報 |
| Incident Escalation <br/>事件升級 | Escalation decision, containment assessment <br/>升級判斷、控制措施成效評估 |
| Case Reporting <br/>案例報告 | 5Ws, affected entities, attack indicators, closure rationale <br/>5W 分析、受影響實體、攻擊指標、結案理由 |
| SOC Performance <br/>SOC 調查績效 | MTTR, report scoring, investigation feedback <br/>平均回應時間、報告評分、調查回饋 |



</div>
<br/>



---------


<h2>Materials and Methods｜材料與方法</h2>

[Environment]
* TryHackMe SOC Simulator (SOC 模擬調查平台)</b>
* Elastic SIEM (安全事件與日誌調查平台)</b>
* Analyst Workstation (SOC 分析師工作站)</b>
* TryDetectThis (情境式威脅情報與 IP 分析工具)</b>
* Employee and Asset Inventory (員工與資產清單)</b>
* Office Network: 10.20.2.0/24
* Alert Queue and Case Reporting Interface (警報佇列與案例報告介面)</b>

</div>
<br/>

[Available Data Sources]
* Email Logs (電子郵件日誌)</b>
* Firewall Logs (防火牆日誌)</b>
* ModSecurity Audit Logs (ModSecurity 稽核日誌)</b>

</div>
<br/>

[Investigation Activities]
* Review SOC Documentation and Alert Triage Playbook (檢視 SOC 文件與警報分類手冊)</b>
* Review Alert Queue and Identify Initial Indicators (檢視警報佇列並識別初始指標)</b>
* Group Related Alerts into Investigation Cases (將相關警報關聯為調查案例)</b>
* Perform Initial Risk-Based Triage and Prioritization (執行初步風險分類與優先排序)</b>
* Correlate Employees, Workstations, and Internal IP Addresses (關聯員工、工作站與內部 IP 位址)</b>
* Investigate Email and Firewall Events in Elastic SIEM (使用 Elastic SIEM 調查郵件與防火牆事件)</b>
* Correlate Suspicious Emails with Subsequent Network Activity (將可疑郵件與後續網路活動進行關聯)</b>
* Validate Malicious Network Indicators with TryDetectThis (使用 TryDetectThis 驗證惡意網路指標)</b>
* Distinguish Legitimate Business Activity from Malicious Activity (區分合法業務活動與惡意活動)</b>
* Classify Alerts as True Positive or False Positive (將警報分類為真陽性或誤報)</b>
* Assess Containment Effectiveness and Escalation Requirements (評估安全控制成效與升級需求)</b>
* Document Affected Entities, Indicators, Timeline, and Investigation Findings (記錄受影響實體、指標、時間軸與調查結果)</b>
* Submit Case Reports and Close Investigated Alerts (提交案例報告並關閉已完成調查的警報)</b>
* Review Investigation Scores and Automated SOC Feedback (檢視調查評分與自動化 SOC 回饋)</b>

</div>
<br/>

---------

<h2>Initial Triage & Prioritization｜初步警報分類與優先排序</h2>

<p align="center">
<b>Initial SOC Alert Queue<br/> (初始 SOC 警報佇列)</b><br/>
<img src="YOUR_ALERT_QUEUE_IMAGE" height="80%" width="80%" alt="Initial SOC Alert Queue"/>
<br />
* Five alerts were identified in the initial queue, including four suspicious inbound email alerts and one High-severity firewall alert.<br/>初始警報佇列共包含五筆警報，包括四筆可疑入站郵件警報與一筆 High Severity 防火牆警報<br/>
<br />
<br />
<b>Case A: Alerts 8815 & 8816 - Amazon Delivery Phishing<br/> (Case A：Amazon 包裹釣魚郵件)</b><br/>
<img src="YOUR_CASE_A_IMAGE" height="80%" width="80%" alt="Alerts 8815 and 8816"/>
<br />
* Alerts 8815 and 8816 were grouped because both involved the same suspicious shortened URL, while Alert 8816 was a High-severity firewall alert associated with the affected user's workstation.<br/>Alert 8815 與 8816 因涉及相同的可疑短網址而合併處理，其中 Alert 8816 為 High Severity 防火牆警報，並與受影響使用者的工作站產生關聯<br/>
* The combination of suspicious email activity and related network activity resulted in this case receiving the highest initial investigation priority.<br/>由於同時出現可疑郵件與相關網路活動，因此本案例被列為最高初步調查優先級<br/>
<br />
<br />
<b>Case B: Alert 8817 - Microsoft Lookalike Phishing<br/> (Case B：Microsoft 仿冒釣魚郵件)</b><br/>
<img src="YOUR_CASE_B_IMAGE" height="80%" width="80%" alt="Alert 8817"/>
<br />
* Alert 8817 contained a Microsoft lookalike domain and a suspicious login lure, indicating a potential credential-phishing attempt.<br/>Alert 8817 包含 Microsoft 仿冒網域與可疑登入誘導，可能涉及憑證釣魚行為<br/>
* No related network alert was visible during the initial review, so further SIEM investigation was required to determine the actual risk level.<br/>初步檢視時尚未發現相關網路警報，因此需要進一步透過 SIEM 調查以確認實際風險程度<br/>
<br />
<br />
<b>Case C: Alerts 8814 & 8818 - HR Onboarding Emails<br/> (Case C：HR Onboarding 郵件)</b><br/>
<img src="YOUR_CASE_C_IMAGE" height="80%" width="80%" alt="Alerts 8814 and 8818"/>
<br />
* Alerts 8814 and 8818 were grouped because they shared the same sender, recipient, subject, and external onboarding domain.<br/>Alert 8814 與 8818 因具有相同寄件者、收件者、主旨與外部 onboarding 網域，因此合併為同一案例<br/>
* No High-severity network activity or clear malicious behavior was visible during the initial review, so this case was assigned a lower investigation priority pending further validation.<br/>初步檢視時尚未發現 High Severity 網路活動或明確惡意行為，因此本案例列為較低調查優先級，等待後續驗證<br/>
<br />
<br />

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
