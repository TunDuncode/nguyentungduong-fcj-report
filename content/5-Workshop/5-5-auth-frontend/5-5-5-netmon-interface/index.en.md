---
title: "5.5.5. Operate the NetMon Management Interface"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 5
---

# 5.5.5. Operate the NetMon Management Interface

## Step 1 – Configuration and connection

Open NetMon with Live Server at `http://localhost:5500/` and sign in as described in 5.5.4. Select **Configuration & connection (Cấu hình & kết nối)** and verify the Invoke URL, Region `us-east-1`, routes and Cognito information. The screenshot shows 80% CPU/RAM display thresholds and a 60-second refresh interval. Save changes if needed. These browser settings do not automatically update CloudWatch or Lambda thresholds; never enter an AWS Secret Access Key.

{{< netmonimg src="images/netmon-workshop/69-netmon-configuration-connection.png" alt="API configuration, display thresholds and refresh interval" caption="Figure 69 – API configuration, display thresholds and refresh interval" >}}

## Step 2 – System overview

Select **Overview (Tổng quan)**. The dashboard shows device counts, active and abnormal devices, unhandled alerts, and CPU/RAM trends sampled in the browser. In the initial screenshot, all five devices are active with no abnormal devices.

{{< netmonimg src="images/netmon-workshop/58-netmon-dashboard-overview.png" alt="System overview with five active devices" caption="Figure 58 – System overview with five active devices" >}}

Scroll down to review recent alerts and AWS integration status. API Gateway/DynamoDB, alert data and CloudWatch Metrics show responses; SNS is not confirmed by the frontend, so this screenshot does not establish email delivery.

{{< netmonimg src="images/netmon-workshop/59-netmon-dashboard-aws-integration.png" alt="Recent alerts and AWS integration status" caption="Figure 59 – Recent alerts and AWS integration status" >}}

## Step 3 – Device management

Select **Device management (Quản lý thiết bị)**. Search by name, ID, IP or location and filter by status. In AWS mode, CRUD requests go through API Gateway → Lambda → DynamoDB.

{{< netmonimg src="images/netmon-workshop/60-netmon-device-list.png" alt="Device list and filters" caption="Figure 60 – Device list and filters" >}}

### 3.1. Add a device

Click **Add device**, enter ID `TEST005`, name `Switch Test`, type Switch, IP `10.0.0.99`, location Floor 4 and status ONLINE. Enter 95% CPU/RAM to exercise the threshold and save. These are simulated metrics, not measurements from a physical switch.

{{< netmonimg src="images/netmon-workshop/61-netmon-add-device.png" alt="Add Switch Test with 95% CPU and RAM" caption="Figure 61 – Add Switch Test with 95% CPU and RAM" >}}

After saving, the device row shows a warning label and both metrics at 95%. The display label can differ from the stored ONLINE status because the configured threshold is exceeded.

{{< netmonimg src="images/netmon-workshop/62-netmon-device-warning.png" alt="Switch Test flagged at 95%" caption="Figure 62 – Switch Test flagged at 95%" >}}

### 3.2. View details

Click **View (Xem)** on TEST005 to inspect ID, name, IP, location, status and metrics.

{{< netmonimg src="images/netmon-workshop/63-netmon-device-detail.png" alt="View TEST005 device details" caption="Figure 63 – View TEST005 device details" >}}

### 3.3. Edit a device

Click **Edit (Sửa)**, change the required information, and save. The screenshot shows the editing form, but does not separately demonstrate saving a changed value.

{{< netmonimg src="images/netmon-workshop/64-netmon-edit-device.png" alt="Device editing form" caption="Figure 64 – Device editing form" >}}

### 3.4. Delete a device

Click **Delete (Xóa)** on Switch Test and choose OK in the confirmation dialog. Delete only test devices.

{{< netmonimg src="images/netmon-workshop/65-netmon-delete-confirmation.png" alt="Switch Test deletion confirmation" caption="Figure 65 – Switch Test deletion confirmation" >}}

After deletion, verify the list returns to five devices and TEST005 is no longer present.

{{< netmonimg src="images/netmon-workshop/66-netmon-device-list-after-delete.png" alt="List returns to five devices after deletion" caption="Figure 66 – List returns to five devices after deletion" >}}

## Step 4 – Monitoring and anomaly detection

Follow CPU/RAM in Overview and open **Performance & Metrics (Hiệu năng & Metrics)** to inspect data sources. EC2 uses CloudWatch metrics when configured; routers and switches use simulated data. In a later screenshot, six devices are listed, with one abnormal device: Router-A002 at 93% CPU and 94% RAM. Unhandled alerts remain at zero; a UI warning does not establish that an AWS alert or SNS email was generated.

{{< netmonimg src="images/netmon-workshop/70-netmon-dashboard-abnormal-device.png" alt="Dashboard flags Router-A002 with 93% CPU and 94% RAM" caption="Figure 70 – Dashboard flags Router-A002 with 93% CPU and 94% RAM" >}}

## Step 5 – Alert center

Select **Alerts & incidents (Cảnh báo & sự cố)** to review times, devices, incidents, severity and handling status. Data is displayed from NetworkAlerts via API Gateway. The screenshot includes handled and recovered events. Investigate new incidents before acknowledging them; acknowledgment does not reset a CloudWatch alarm to OK.

{{< netmonimg src="images/netmon-workshop/67-netmon-alert-center.png" alt="Alert and incident center" caption="Figure 67 – Alert and incident center" >}}

## Step 6 – Network and infrastructure diagrams

Open **Infrastructure diagram (Sơ đồ hạ tầng)** to review the designed model. Simulated routers and switches do not establish physical links or automatic topology discovery. A separate screenshot of this page has not been supplied.

## Step 7 – History logs

Select **History (Nhật ký lịch sử)** to search by action or device. The screenshot records adding TEST005 at 15:48:50 and deleting it at 15:49:37 on November 18, 2026, with Browser as the source. Distinguish local action history from AWS/DynamoDB alerts; browser logs are not a centralized audit log. Use **Reload AWS history** to refresh AWS records.

{{< netmonimg src="images/netmon-workshop/68-netmon-history-log.png" alt="Browser action history" caption="Figure 68 – Browser action history" >}}

## Recorded results

NetMon Cloud illustrate listing, adding, viewing, opening the edit form, deleting a test device, flagging anomalies and reviewing alerts, history and settings. Compare DynamoDB records and Lambda logs to verify AWS persistence. SNS delivery, detailed EC2 metrics and diagrams require separate evidence.

[← Back to chapter](../)
