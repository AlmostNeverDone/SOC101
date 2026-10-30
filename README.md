# SOC Alert Triage & Phishing Investigation Using Elastic SIEM

使用 Elastic SIEM 進行 SOC 警報分類與釣魚事件調查

<br/>

---------

<h2>Outline｜調查簡介</h2>

This project demonstrates a structured Security Operations Center (SOC) alert triage and phishing investigation workflow using the TryHackMe SOC Simulator and Elastic SIEM.

本專題透過 TryHackMe SOC Simulator 與 Elastic SIEM，展示一套結構化的安全營運中心 (SOC) 警報分類與釣魚事件調查流程。

The scenario contained five security alerts involving suspicious inbound emails and related firewall activity. Initial triage was performed to identify shared indicators, affected users, and potential relationships between alerts, allowing the alerts to be grouped into three investigation cases with different priorities.

本次情境共包含五筆安全警報，涉及可疑入站郵件與相關防火牆活動。首先透過 Initial Triage 識別共同指標、受影響使用者與警報之間可能存在的關聯，並將五筆警報整理為三個不同優先層級的調查案例。

The investigation used email and firewall telemetry in Elastic SIEM, employee and asset inventory information, and TryDetectThis threat intelligence to correlate events, validate suspicious indicators, distinguish legitimate business activity from malicious behavior, and assess whether existing security controls successfully contained the activity.

調查過程結合 Elastic SIEM 中的電子郵件與防火牆遙測資料、員工與資產清單，以及 TryDetectThis 威脅情報，進行事件關聯與可疑指標驗證，並區分合法業務活動與惡意行為，同時評估既有安全控制是否成功阻擋相關活動。

The three cases resulted in different outcomes: a phishing attempt successfully blocked by the firewall, a malicious connection requiring escalation, and legitimate HR onboarding emails confirmed as false positives. The project therefore focuses not only on detecting suspicious activity, but also on evidence-based classification, risk reassessment, escalation decisions, and SOC case reporting.

三個案例最終呈現不同結果，包括遭防火牆成功阻擋的釣魚活動、需要升級處理的惡意連線，以及經確認為誤報的合法 HR onboarding 郵件。因此，本專題不僅著重於偵測可疑行為，也強調以證據為基礎的事件分類、風險重新評估、升級判斷與 SOC 案例報告能力。

<br/>

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

<br/>

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

<br/>

---------

<h2>Tools and Concepts Covered｜涵蓋工具與概念</h2>


| Category (分類) | Tools / Concepts (工具 / 概念) |
| --- | --- |
| SOC Operations <br/>SOC 安全營運 | Alert triage, alert ownership, case investigation <br/>警報分類、警報接手、案例調查 |
| SIEM Investigation <br/>SIEM 調查 | Elastic SIEM |
| Security Telemetry <br/>安全遙測資料 | Email logs, Firewall logs<br/>電子郵件日誌、防火牆日誌 |
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
<img src="https://i.imgur.com/hvtpShK.png" height="80%" width="80%" alt="Initial SOC Alert Queue"/>
<br />
* Five alerts were identified in the initial queue, including four suspicious inbound email alerts and one High-severity firewall alert.<br/>初始警報佇列共包含五筆警報，包括四筆可疑入站郵件警報與一筆 High Severity 防火牆警報<br/>
<br />
<br />
<b>Case A: Alerts 8815 & 8816 - Amazon Delivery Phishing<br/> (Case A：Amazon 包裹釣魚郵件)</b><br/>
<img src="https://i.imgur.com/uehyYVq.png" height="80%" width="80%" alt="Alerts 8815 and 8816"/>
<br />
* Alerts 8815 and 8816 were grouped because both involved the same suspicious shortened URL, <br/>while Alert 8816 was a High-severity firewall alert associated with the affected user's workstation.<br/>Alert 8815 與 8816 因涉及相同的可疑短網址而合併處理，<br/>其中 Alert 8816 為 High Severity 防火牆警報，並與受影響使用者的工作站產生關聯<br/>
<br />
* The combination of suspicious email activity and related network activity <br/>resulted in this case receiving the highest initial investigation priority.<br/>由於同時出現可疑郵件與相關網路活動，因此本案例被列為最高初步調查優先級<br/>
<br />
<br />
<b>Case B: Alert 8817 - Microsoft Lookalike Phishing<br/> (Case B：Microsoft 仿冒釣魚郵件)</b><br/>
<img src="https://i.imgur.com/lZ0PlfG.png" height="80%" width="80%" alt="Alert 8817"/>
<br />
* Alert 8817 contained a Microsoft lookalike domain and a suspicious login lure, indicating a potential credential-phishing attempt.<br/>Alert 8817 包含 Microsoft 仿冒網域與可疑登入誘導，可能涉及憑證釣魚行為<br/>
<br />
* No related network alert was visible during the initial review, so further SIEM investigation was required to determine the actual risk level.<br/>初步檢視時尚未發現相關網路警報，因此需要進一步透過 SIEM 調查以確認實際風險程度<br/>
<br />
<br />
<b>Case C: Alerts 8814 & 8818 - HR Onboarding Emails<br/> (Case C：HR Onboarding 郵件)</b><br/>
<img src="https://i.imgur.com/RKIL7rY.png" height="80%" width="80%" alt="Alerts 8814 and 8818"/>
<br />
* Alerts 8814 and 8818 were grouped because they shared the same sender, recipient, subject, and external onboarding domain.<br/>Alert 8814 與 8818 因具有相同寄件者、收件者、主旨與外部 onboarding 網域，因此合併為同一案例<br/>
<br />
* No High-severity network activity or clear malicious behavior was visible during the initial review, <br/>so this case was assigned a lower investigation priority pending further validation.<br/>初步檢視時尚未發現 High Severity 網路活動或明確惡意行為，<br/>因此本案例列為較低調查優先級，等待後續驗證<br/>
<br />
<br />

---------

<h2>Case Investigation｜案例調查</h2>

<p align="center"><p align="center">
<b>Case A1-Email and Firewall Correlation<br/> (郵件與防火牆事件關聯)</b><br/>
<img src="https://i.imgur.com/dyS3KJv.jpeg" height="80%" width="80%" alt="Email and Firewall Correlation"/>
<br />
* Elastic SIEM identified the same shortened URL in both the suspicious Amazon email and the related firewall event.<br/>Elastic SIEM 在可疑 Amazon 郵件與相關防火牆事件中發現相同短網址<br/>
* Source IP 10.20.2.17 matched Hannah Harris's assigned workstation.<br/>來源 IP 10.20.2.17 可對應至 Hannah Harris 的工作站<br/>
<br />
<br />
<b>Case A2-Network Activity Investigation<br/> (網路活動調查)</b><br/>
<img src="https://i.imgur.com/F695V1t.jpeg" height="80%" width="80%" alt="Network Activity Investigation"/>
<br />
* The outbound request targeted 67.199.248.11 on port 80 and was blocked by the Blocked Websites firewall rule.<br/>外連請求以 67.199.248.11 的 Port 80 為目的地，並由 Blocked Websites 防火牆規則成功阻擋<br/>
* No additional suspicious activity associated with the phishing URL was identified in the available firewall logs.<br/>現有防火牆日誌中未發現與該釣魚網址相關的其他可疑活動<br/>
<br />
<br />
<b>Case B1-Suspicious Network Activity Investigation<br/> (可疑網路活動調查)</b><br/>
<img src="https://i.imgur.com/l0yKB2v.jpeg" height="80%" width="80%" alt="Suspicious Network Activity Investigation"/>
<br />
* Elastic SIEM identified an HTTPS connection from Charlotte Allen's workstation IP 10.20.2.25 to the suspicious Microsoft lookalike URL.<br/>Elastic SIEM 發現 Charlotte Allen 的工作站 IP 10.20.2.25 對可疑 Microsoft 仿冒網址發起 HTTPS 連線<br/>
* The connection reached destination IP 45.148.10.131 on port 443 and was allowed by the firewall.<br/>該連線以 45.148.10.131 的 Port 443 為目的地，且未遭防火牆阻擋<br/>
<br />
<br />
<b>Case B2-Workstation Network Activity Investigation<br/> (工作站網路活動調查)</b><br/>
<img src="https://i.imgur.com/GoQlJNA.jpeg" height="80%" width="80%" alt="Threat Intelligence Enrichment"/>
<br />
* Searching *10.20.2.25* identified outbound network activity from Charlotte Allen's workstation.<br/>The firewall recorded the request to 45.148.10.131 on port 443 as allowed.<br/>搜尋 *10.20.2.25*，確認 Charlotte Allen 的工作站存在相關外連活動。<br/>防火牆記錄顯示，前往 45.148.10.131、Port 443 的請求獲准通過<br/>
<br />
<br />
<b>Case B3-Threat Intelligence Enrichment<br/> (威脅情報擴展)</b><br/>
<img src="https://i.imgur.com/CiyK9YN.jpeg" height="80%" width="80%" alt="Threat Intelligence Enrichment"/>
<br />
* TryDetectThis returned CLEAN for the IP address 102.89.222.143 embedded in the phishing email, <br/>while the destination IP 45.148.10.131 observed in firewall telemetry was classified as MALICIOUS.<br/>TryDetectThis 將釣魚郵件內提供的 IP 102.89.222.143 判定為 CLEAN，<br/>而防火牆遙測中實際觀察到的目的 IP 45.148.10.131 則被判定為 MALICIOUS<br/>
<br />
<br />
<b>Case C1-Related Email Event Correlation<br/> (相關郵件事件關聯)</b><br/>
<img src="https://i.imgur.com/5ryILWJ.jpeg" height="80%" width="80%" alt="Related Email Event Correlation"/>
<br />
* Searching hrconnex.thm identified three related email events, including two onboarding emails and an internal HR-to-IT conversation.<br/>搜尋 hrconnex.thm 後發現三筆相關郵件事件，包括兩封 onboarding 郵件與一封 HR 和 IT Support 之間的內部郵件<br/>
<br />
<br />
<b>Case C2-Firewall Activity Review<br/> (防火牆活動檢視)</b><br/>
<img src="https://i.imgur.com/yvf8lr1.jpeg" height="80%" width="80%" alt="Firewall Activity Review"/>
<br />
* Firewall activity associated with Julia Garcia's workstation IP 10.20.2.8 was reviewed for related network activity.<br/>檢視 Julia Garcia 工作站 IP 10.20.2.8 的防火牆活動，以確認是否存在相關網路行為<br/>
* No connection to hrconnex.thm was identified in the available firewall logs.<br/>現有防火牆日誌中未發現對 hrconnex.thm 的連線<br/>
<br />
<br />


---------

<h2>Results｜調查結果與專題結論</h2>

This project demonstrated a complete SOC alert triage and investigation workflow using Elastic SIEM, asset information, firewall telemetry, email logs, and threat intelligence enrichment.

本專題展示了一套完整的 SOC 警報分類與調查流程，透過 Elastic SIEM、資產資訊、防火牆遙測、電子郵件日誌與威脅情報進行事件分析。

Five alerts were initially reviewed and correlated into three investigation cases based on shared users, URLs, network activity, and business context.

初始共檢視五筆警報，並依據共同使用者、URL、網路活動與業務情境，將相關警報整合為三個調查案例。
<br/>
<br/>

| Case | Related Alerts | Classification | Escalation | Investigation Result |
| --- | --- | --- | --- | --- |
| A | 8815, 8816 | True Positive | No | The suspicious Amazon-themed email was correlated with a subsequent request to the same shortened URL. The firewall successfully blocked the connection.<br/>可疑 Amazon 主題郵件與後續相同短網址的連線活動成功關聯，且防火牆成功阻擋該連線。 |
| B | 8817 | True Positive | Yes | The affected workstation connected to the Microsoft lookalike URL, the connection was allowed, and the destination IP was classified as MALICIOUS by TryDetectThis.<br/>受影響工作站成功連線至 Microsoft 仿冒網址，該連線未遭防火牆阻擋，且目的 IP 經 TryDetectThis 判定為 MALICIOUS。 |
| C | 8814, 8818 | False Positive | No | Internal HR-to-IT communication confirmed that hrconnex.thm was a legitimate third-party HR partner, supporting closure of the onboarding alerts as false positives.<br/>HR 與 IT Support 的內部郵件確認 hrconnex.thm 為合法第三方 HR 合作夥伴，因此兩筆 onboarding 警報最終判定為誤報。 |

<br/>

The investigation demonstrated that alert severity and suspicious indicators alone are not sufficient to determine the final incident outcome. Case A represented genuine malicious activity that was successfully contained, Case B required escalation because an allowed connection reached a confirmed malicious destination, while Case C demonstrated how legitimate business activity can trigger security detections.

本次調查顯示，僅依靠警報嚴重度或可疑指標並不足以決定最終事件結果。Case A 為真實惡意活動，但已由安全控制成功阻擋；Case B 因成功連線至確認為惡意的目的地而需要升級處理；Case C 則展示合法業務活動同樣可能觸發安全偵測。

The SOC Simulator assessment also provided feedback on case-reporting quality. The reports received 95/100 for Alert 8815, 108/110 for Alert 8816, 90/100 for Alert 8817, and full scores for Alerts 8814 and 8818. Feedback highlighted the importance of clearly explaining threat-actor objectives, associating timestamps with individual events, and ensuring remediation recommendations remain proportional to the actual impact.

SOC Simulator 同時對案例報告品質提供自動化評估。Alert 8815 獲得 95/100、Alert 8816 獲得 108/110、Alert 8817 獲得 90/100，而 Alert 8814 與 8818 均獲得滿分。評估結果指出，後續仍應加強攻擊者目的說明、將時間戳記明確對應至各項事件，並確保補救建議與實際影響程度保持適當比例。

Overall, this project strengthened practical skills in risk-based alert triage, event correlation, phishing investigation, threat intelligence validation, incident classification, escalation decision-making, and SOC case reporting.

整體而言，本專題強化了風險導向警報分類、事件關聯、釣魚郵件調查、威脅情報驗證、事件分類、升級判斷，以及 SOC 案例報告等實務能力。

<br/>
<br/>

---------

<h2>Security Insight｜安全洞察</h2>

Alert triage is not simply a process of identifying whether an alert is malicious. Effective SOC investigation requires analysts to correlate multiple data sources, understand business context, evaluate the effectiveness of existing security controls, and continuously reassess risk as new evidence becomes available.

警報分類並不只是判斷警報是否具有惡意。有效的 SOC 調查需要分析師關聯多種資料來源、理解業務情境、評估現有安全控制措施的有效性，並隨著新證據出現持續重新評估風險。

<br/>

Risk-Based Prioritization (風險導向優先排序)

Alert severity is an important triage factor, but it should not be treated as the final risk assessment. Initial priority should consider available indicators, affected assets, observable network activity, and potential impact, while the final risk level should be updated after investigation.

警報嚴重度是重要的初步分類依據，但不應直接等同於最終風險。初步優先順序應同時考量可用指標、受影響資產、可觀察到的網路活動與潛在影響，並在完成調查後重新評估最終風險。

<br/>

True Positive Does Not Always Require Escalation (真陽性不一定需要升級)

Case A demonstrated that a confirmed malicious activity can still be closed without escalation when existing security controls successfully contain the threat and no evidence of further compromise is identified.

Case A 顯示，即使事件確認為真陽性，只要現有安全控制成功阻擋威脅，且未發現進一步入侵證據，仍可能不需要升級處理。

<br/>

Successful Connection Changes the Risk (成功連線會改變風險程度)

Case B demonstrated the importance of evaluating whether preventive controls actually stopped the activity. An allowed connection to a destination independently classified as malicious significantly increased the potential impact and justified escalation for further investigation.

Case B 顯示，分析師必須確認預防性安全控制是否真正阻止事件。當工作站成功連線至經獨立威脅情報確認的惡意目的地時，潛在影響將明顯增加，因此需要進一步升級調查。

<br/>

Business Context Is Critical for False Positive Analysis (業務情境對誤報分析十分重要)

Case C demonstrated that suspicious external links should not automatically be treated as malicious. Internal communication and business context confirmed that the external HR domain was part of a legitimate onboarding process, preventing unnecessary escalation.

Case C 顯示，包含可疑外部連結的郵件不應直接被視為惡意。透過內部通訊與業務背景確認該外部 HR 網域屬於合法 onboarding 流程，可避免不必要的事件升級與資源消耗。

<br/>

Telemetry Must Be Distinguished from Attacker-Supplied Content (安全遙測應與攻擊者提供的內容區分)

During Case B, the IP address shown inside the phishing email was classified as CLEAN, while the destination IP actually observed in firewall telemetry was classified as MALICIOUS. This highlights the importance of distinguishing attacker-controlled content from indicators directly observed by security systems.

在 Case B 中，釣魚郵件內容所提供的 IP 被判定為 CLEAN，而防火牆實際觀察到的目的 IP 則被判定為 MALICIOUS。這說明調查時必須區分攻擊者自行提供的內容，以及由安全系統實際觀察到的威脅指標。

<br/>

Evidence Boundaries and Reporting Accuracy (證據邊界與報告精準度)

The available SIEM telemetry was limited primarily to Email, Firewall, and Webserver logs. Therefore, conclusions regarding user actions, credential submission, or endpoint compromise should not exceed what the available evidence can support.

本次 SIEM 可用的遙測資料主要限制於 Email、Firewall 與 Webserver 日誌，因此針對使用者實際操作、憑證是否遭提交，以及端點是否已遭入侵等結論，都不應超出現有證據所能支持的範圍。

High-quality SOC reporting should clearly distinguish confirmed observations from assumptions, associate timestamps with specific events, explain the likely objective of the threat actor, and recommend remediation proportional to the actual impact.

高品質 SOC 報告應清楚區分已確認事實與推測、將時間戳記明確對應至特定事件、說明攻擊者可能的目的，並依據事件實際影響程度提出適當的補救措施。

<br/>
<br/>


---------

<h2>Reference｜參考</h2>

[TryHackMe] [SOC Simulator](https://tryhackme.com/soc-sim)<br/>
<br/>
