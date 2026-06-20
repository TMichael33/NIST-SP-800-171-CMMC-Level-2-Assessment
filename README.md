# Project 2: NIST SP 800-171 & CMMC Level 2 Assessment

## 🛡️ Executive Summary
This project simulates a comprehensive gap analysis and readiness assessment for a mid-sized aerospace component manufacturer ("Titan Aerospace") preparing for a Cybersecurity Maturity Model Certification (CMMC) Level 2 third-party audit. Titan Aerospace handles Controlled Unclassified Information (CUI) and must demonstrate 100% implementation of the 110 controls defined in NIST SP 800-171. 

The objective of this project was to establish a System Security Plan (SSP) baseline, identify critical gaps in the **Access Control (AC)** and **Audit & Accountability (AU)** domains, and generate a formal Plan of Action and Milestones (POA&M) to achieve full audit readiness.

---

## 📋 Methodology & Assessment Scope
The assessment was conducted against the 14 families of NIST SP 800-171. Controls were scored using a binary model:
*   **Compliant (C):** The control is fully implemented, documented in the SSP, and supported by artifacts.
*   **Non-Compliant (NC):** A gap exists. The control must be deferred to the POA&M with a defined remediation path and target date.

---

## 📝 Plan of Action and Milestones (POA&M)

Below is an extraction of the active POA&M tracking high-priority gaps discovered during the assessment. 

<table width="100%">
  <thead>
    <tr>
      <th width="10%">Control ID</th>
      <th width="20%">Control Description</th>
      <th width="25%">Identified Gap / Deficiency</th>
      <th width="25%">Remediation Plan & Milestone</th>
      <th width="10%">Target Date</th>
      <th width="10%">Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>3.1.1</b> (AC)</td>
      <td>Limit system access to authorized users, processes, or devices.</td>
      <td>Engineering workstations lack unique individual logins. Multi-user "shop floor" accounts are actively shared among shifts.</td>
      <td>• Enforce individual Active Directory domain logins.<br>• Implement Microsoft Entra ID with Role-Based Access Control (RBAC).</td>
      <td>Q3 2026</td>
      <td><span style="color:orange;"><b>In Progress</b></span></td>
    </tr>
    <tr>
      <td><b>3.1.2</b> (AC)</td>
      <td>Limit system access to the types of transactions and functions that authorized users are permitted to execute.</td>
      <td>Local administrator accounts are active on 40% of corporate endpoints, allowing unauthorized software installation.</td>
      <td>• Revoke local admin rights via Group Policy Objects (GPO).<br>• Deploy a Privileged Identity Management (PIM) solution for temporary access elevation.</td>
      <td>Q3 2026</td>
      <td><span style="color:orange;"><b>In Progress</b></span></td>
    </tr>
    <tr>
      <td><b>3.3.1</b> (AU)</td>
      <td>Create and retain system audit logs and records to the extent needed to enable the monitoring, analysis, and investigation of unlawful or unauthorized system activity.</td>
      <td>Firewalls and domain controllers are logging locally. Logs are overwritten every 14 days; no centralized long-term retention exists.</td>
      <td>• Procure and configure a centralized SIEM solution.<br>• Establish immutable cloud storage to enforce a strict 1-year log retention policy.</td>
      <td>Q4 2026</td>
      <td><span style="color:red;"><b>Not Started</b></span></td>
    </tr>
    <tr>
      <td><b>3.4.1</b> (CM)</td>
      <td>Establish and maintain baseline configurations and inventories of organizational systems throughout the respective system development lifecycles.</td>
      <td>No centralized, authorized baseline exists for engineering workstations. Engineers routinely install ad-hoc software variants, creating configuration drift.</td>
      <td>• Establish a formal Change Control Board (CCB).<br>• Deploy Microsoft Intune to enforce standardized configuration baselines and block unapproved software.</td>
      <td>Q4 2026</td>
      <td><span style="color:orange;"><b>In Progress</b></span></td>
    </tr>
    <tr>
      <td><b>3.5.3</b> (IA)</td>
      <td>Use multifactor authentication (MFA) for local and network access to privileged accounts and for network access to non-privileged accounts.</td>
      <td>MFA is enforced for remote VPN access, but is completely missing for internal local workstation network logins.</td>
      <td>• Enforce mandatory MFA via Windows Hello for Business or hardware tokens (YubiKeys) across all internal network infrastructure.</td>
      <td>Q2 2026</td>
      <td><span style="color:green;"><b>Completed</b></span></td>
    </tr>
    <tr>
      <td><b>3.8.3</b> (MP)</td>
      <td>Sanitize or destroy information system media containing CUI before disposal or release for reuse.</td>
      <td>Decommissioned hard drives from engineering machines are stored in an unlocked IT closet without tracking or formal sanitization records.</td>
      <td>• Implement a secure, locked media disposal bin.<br>• Mandate NIST 800-88 R1 compliant physical destruction/degaussing and require signed Certificates of Destruction for all assets.</td>
      <td>Q2 2026</td>
      <td><span style="color:green;"><b>Completed</b></span></td>
    </tr>
  </tbody>
</table>
---

## 🗺️ System Security Plan (SSP) Baseline Framework
To achieve audit readiness, an artifact index was established to serve as the baseline evidence for the upcoming CMMC assessment:
1.  **Access Control Policy (v2.1):** Outlines the corporate rules for individual accountability and authorization constraints.
2.  **Network Architecture Diagram (Sanitized):** Documents the boundaries of the CUI environment (Federal boundary isolation).
3.  **SIEM Log Configuration Manifest:** Proves centralized logging pipelines map directly to the AU control domain requirements.

---

## 💡 Key Insights & Business Alignment
1.  **POA&M Accountability:** In defense contracting, a POA&M isn't just a basic to-do list; it is a legally binding compliance roadmap. If a contractor self-attests to compliance but fails to meet their POA&M target dates, they face substantial operational and legal liabilities under the False Claims Act.
2.  **Balancing Security and Production:** Revoking local administrator rights (Control 3.1.2) frequently creates pushback from production teams. The remediation strategy leverages an enterprise PIM solution to provide Just-In-Time (JIT) access elevation, allowing engineers to maintain speed while meeting compliance criteria.
3.  **Continuous Monitoring (ConMon):** Meeting CMMC Level 2 requirements is not a "one-and-done" checkbox audit. Centralizing logs via a SIEM architecture (Control 3.3.1) changes the organizational posture from a static annual audit compliance view to a dynamic, continuous monitoring model.
