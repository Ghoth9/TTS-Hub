# 🏢 Enterprise Operations Hub (TTS Ops Hub)
### *All-in-One Operations, Inventory, CCTV Infrastructure & Field Service Management System*

[![Live Demo](https://img.shields.io/badge/Live_Demo-tts--ops--hub.vercel.app-6366F1?style=for-the-badge&logo=vercel&logoColor=white)](https://tts-ops-hub.vercel.app)
[![React](https://img.shields.io/badge/React_19-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript_5.0-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS_v4-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Supabase](https://img.shields.io/badge/Supabase_Cloud-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)](https://supabase.com/)
[![LINE Messaging API](https://img.shields.io/badge/LINE_Messaging_API-00C300?style=for-the-badge&logo=line&logoColor=white)](https://developers.line.biz/)

<p align="center">
  A comprehensive, cloud-native enterprise operations platform built to modernize company workflows—combining real-time inventory tracking, field technician dispatching, interactive GIS CCTV mapping, contract lifecycles, HR operations, and automated dual-bot LINE notifications.
</p>

<img width="1919" height="867" alt="image" src="https://github.com/user-attachments/assets/f07ea621-ef86-42b8-a6e8-ea9c4420ee92" />



</div>

---

## 📌 Executive Summary & Case Study

### 🎯 The Challenge
Traditional enterprise operations often suffer from fragmented tools: inventory is managed in disconnected spreadsheets, repair requests get lost in group chats, contract warranties expire unnoticed, and field technicians lack unified visibility into equipment mapping and maintenance histories.

### 💡 The Solution
**TTS Ops Hub** unifies company workflows into a single, high-performance responsive web application with real-time cloud synchronization, zero-latency state management, robust role-based access control (RBAC), and automated event-driven messaging to LINE group chats.

---

## 🚀 Key Modules & System Capabilities

### 1. 📦 Inventory & Stock Distribution
- **Real-Time Stock Auditing:** Low-stock threshold alerts, category filters, and granular inventory movements.
- **Stock Requisition & Issuance:** Digital stock checkout slips with automated deduction upon approval.
- **Isolated Iframe Print Engine:** Zero-layout-shift print generator producing official company requisition vouchers with base64 high-resolution branding.

<img width="1919" height="867" alt="image" src="https://github.com/user-attachments/assets/ef538726-49a4-4238-aaa0-7ac100956fd3" />


---

### 2. 🔄 Equipment Borrowing & Custody Tracking
- **Digital Custody Logs:** Track items currently borrowed, overdue equipment, borrower identity, and return timestamps.
- **Multi-Item Checkout:** Batch borrowing with serial number validation and one-click return processing.
- **Official Print Slips:** Auto-formatted legal handover documents ready for physical signing.

---

### 3. 📹 CCTV Infrastructure & Interactive GIS Map
- **Satellite GIS Mapping:** Interactive map marking surveillance poles, cabinets, and camera locations across client municipalities.
- **Live Node Inspection:** Click-to-inspect cabinet layouts, connected IP cameras, channel numbers, and active/offline health statuses.
- **Evidence & Video Request Workflow:** Public-facing and internal citizen request forms with timestamp and passcode verification.

<img width="1919" height="867" alt="image" src="https://github.com/user-attachments/assets/a50e565a-de2e-41eb-b9e0-60374a45d4e7" />


---

### 4. 🛠️ Field Service & Preventive Maintenance (PM)
- **Repair Ticketing Workflow:** Multi-stage lifecycle (`Pending` ➔ `In Progress` ➔ `Completed` ➔ `Canceled`).
- **PM Schedule Tracking:** Automated cycle calculation for scheduled preventive maintenance inspections.
- **Technician Dispatch:** Push instant task cards with GPS locations and issue descriptions directly to field teams.

<img width="1919" height="867" alt="image" src="https://github.com/user-attachments/assets/434e5e34-b4d3-4ac8-9239-7b1408420dce" />


---

### 5. 📄 Contract & Warranty Lifecycle Management
- **Contract Valuation:** Total contract worth, active vs. expired status tracking, and deposit management.
- **Milestone & Periodic Service Timelines:** Track cloud storage renewals, periodic server health checks, and domain renewals.
- **Automated Expiry Warnings:** Visual indicators and automated alerts before warranty lapses.

---

### 6. 👥 HR Operations & Staff Management
- **Role-Based Access Control (RBAC):** Multi-tier authorization (`Admin`, `Manager`, `Technician`, `Staff`).
- **Overtime (OT) Engine:** Accurate Thai labor law overtime calculator with supervisor approval steps.
- **Fingerprint Miss & Attendance Logs:** One-click attendance rectification forms with cloud auditing.

---

### 7. 🤖 Dual-Bot Automated LINE Messaging Architecture
- **Multi-Channel Distribution:** Two independent LINE Official Account bots to prevent single-channel quota exhaustion:
  - 📋 **TTS Task Bot:** General job assignments, progress updates, and deadline reminders.
  - 🛠️ **TTS Service Alert Bot:** Emergency repair alerts, CCTV cabinet outages, and PM notifications.
- **Real-Time Quota Telemetry:** Direct integration with LINE API to monitor monthly message consumption and warn before exhaustion.
- **Smart Failover:** Graceful fallback mechanism ensuring critical notifications are never dropped.

<img width="395" height="423" alt="image" src="https://github.com/user-attachments/assets/0d8bd2b8-0d87-422e-ac82-39c31dd8712b" />


---

## 🏗️ Architecture & Technology Stack

```mermaid
graph TD
    Client["💻 Client Web App (React 19 + Vite + Tailwind)"]
    
    subgraph "Edge & Serverless Tier (Vercel)"
        API_Push["/api/line-push (Serverless Function)"]
        API_Webhook["/api/line-webhook (Event Ingestion)"]
        API_Quota["/api/line-quota (Telemetry Engine)"]
    end
    
    subgraph "Database & Storage Tier (Supabase)"
        DB[(PostgreSQL + RLS)]
        Realtime["Realtime Channels"]
        Storage["Supabase Storage"]
    end
    
    subgraph "External Integrations"
        LINE_API["LINE Messaging API Platform"]
        LINE_Group["👥 Company Staff & Tech LINE Groups"]
    end

    Client -->|REST / RPC| DB
    Client -->|Subscribe| Realtime
    Client -->|Trigger Notification| API_Push
    Client -->|Query Telemetry| API_Quota
    
    API_Push -->|Push Flex Message| LINE_API
    API_Quota -->|Check Consumption| LINE_API
    LINE_API -->|Broadcast| LINE_Group
    LINE_Group -->|User Webhook Events| API_Webhook
    API_Webhook -->|Persist Metadata| DB
