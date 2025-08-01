# 🛠️ Istio Canary Deployment Monitoring with Flagger

## ✅ Prerequisites
Before setting up this monitoring:
1. **Kube-Prometheus Stack** is installed (provides Prometheus and Grafana in the `monitoring` namespace).
2. **Istio Prometheus** is installed (collects Istio traffic metrics from Envoy sidecars).

---

## 🔄 Flow Overview
- The **Istio Prometheus** collects **Istio traffic metrics** that are used by the dashboard.  

## ✅ We have 2 Prometheus instances:
1. **Kube-Prometheus Stack Prometheus**  
2. **Istio Prometheus**

---

### First Panel 3 Metrics Used:
- **Primary Traffic Shift**  && **Status of Canary Deployment**  && **Canary Traffic Shifts**
- The dashboard relies on **Flagger metrics** (e.g., canary deployment status, traffic shifting) exposed by the Flagger pod that we are collecting metrics through `ServiceMonitor` resources that we created and that monitord by **Kube-Prometheus Stack Prometheus** .

These metrics are scraped from the **Flagger pod**, which by default exposes its metrics in the `istio-system` namespace.

![ Grafana Dashboard Preview ](/Canary-Monitoring/.images/first-panel.png)

### Other Metrics in Below Panel:
- Below all panel metrics from Istio Prometheus.

These metrics are scraped from the **Flagger pod**, which by default exposes its metrics in the `istio-system` namespace.

---

## 📡 Apply the Files and Import the Dashboard into Grafana

1. **Apply the required manifests:**
   ```bash
   kubectl apply -f flagger-service.yaml
   kubectl apply -f flagger-servicemonitor.yaml

2. Import the JSON dashboard into Grafana:

    - During the import process, you will be prompted to select two Prometheus datasources:

        - **Kube-Prometheus Stack Prometheus**
        - **Istio Prometheus**---

--
## 🖼️ Dashboard Preview

![ Grafana Dashboard Preview ](/Canary-Monitoring/.images/Canary-Deployment-Flagger-1.png)
![ Grafana Dashboard Preview ](/Canary-Monitoring/.images/Request-CPU-1.png)
![ Grafana Dashboard Preview ](/Canary-Monitoring/.images/Request-CPU-2.png)