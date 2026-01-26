# 029 - DCGM Exporter for GPU Monitoring

## Script

Your ML training job runs for 12 hours, then crashes. The GPU overheated. You had no idea because you weren't monitoring it.

This is why you need DCGM Exporter.

DCGM stands for Data Centre GPU Manager. It's NVIDIA's tool for monitoring GPU health and performance. The exporter turns those metrics into Prometheus format so you can visualise them in Grafana.

What metrics do you get? Temperature, power usage, memory utilisation, GPU utilisation, fan speed, and ECC errors. You can even see SM clock speeds and PCIe throughput.

Why does this matter?

Temperature spikes cause thermal throttling. Your training slows down and you don't know why. Memory utilisation creeping up? You're about to hit an out-of-memory error. ECC errors increasing? Your GPU might be failing.

Deploy DCGM Exporter as a DaemonSet so it runs on every GPU node. Point Prometheus at it and set up alerts.

GPU memory above 90%? Alert. Temperature above 80 degrees? Alert. ECC errors detected? Definitely alert.

Don't let your next training job fail silently. Monitor your GPUs like your models depend on it, because they do.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "12 hours, then crashes" | Training progress bar at 95%, then red crash screen |
| "GPU overheated" | GPU with thermometer showing red/critical temperature |
| "no idea" | Empty monitoring dashboard, no GPU metrics visible |
| "DCGM Exporter" | DCGM Exporter logo/icon appearing |
| "Data Centre GPU Manager" | NVIDIA logo, enterprise data centre with GPU racks |
| "Prometheus format" | Metrics flowing from GPU → DCGM → Prometheus → Grafana pipeline |
| "Temperature" | Thermometer gauge on GPU |
| "power usage" | Wattage meter showing GPU power draw |
| "memory utilisation" | Memory bar filling up (like RAM usage) |
| "GPU utilisation" | Percentage gauge showing compute usage |
| "fan speed" | Fan icon with RPM indicator |
| "ECC errors" | Error counter with warning symbol |
| "SM clock speeds" | Clock frequency display |
| "PCIe throughput" | Data transfer speed between GPU and CPU |
| "thermal throttling" | GPU clock speed dropping as temperature rises, graph correlation |
| "training slows down" | Training iteration time increasing on graph |
| "memory creeping up" | Memory usage line slowly approaching 100% limit |
| "out-of-memory error" | OOM killer message, pod getting evicted |
| "ECC errors increasing" | Error count ticking up, hardware degradation warning |
| "GPU might be failing" | GPU with warning icon, replacement needed |
| "DaemonSet" | DaemonSet pods running on each GPU node in cluster |
| "Prometheus at it" | ServiceMonitor connecting to DCGM Exporter pods |
| "set up alerts" | Alert rules in Prometheus/Alertmanager |
| "GPU memory above 90%" | Alert firing with memory threshold breach |
| "Temperature above 80" | Alert firing with thermal warning |
| "ECC errors detected" | Critical alert for hardware errors |
| "Monitor your GPUs" | Beautiful Grafana dashboard with all GPU metrics |

## Key DCGM Metrics

| Metric | Prometheus Name | Why It Matters |
|--------|-----------------|----------------|
| GPU Utilisation | `DCGM_FI_DEV_GPU_UTIL` | Is your GPU actually being used? |
| Memory Used | `DCGM_FI_DEV_FB_USED` | Approaching OOM? |
| Memory Free | `DCGM_FI_DEV_FB_FREE` | How much headroom left? |
| Temperature | `DCGM_FI_DEV_GPU_TEMP` | Thermal throttling risk |
| Power Usage | `DCGM_FI_DEV_POWER_USAGE` | Power budget and cooling |
| SM Clock | `DCGM_FI_DEV_SM_CLOCK` | Is GPU throttling? |
| Memory Clock | `DCGM_FI_DEV_MEM_CLOCK` | Memory bandwidth issues |
| ECC Errors (Single) | `DCGM_FI_DEV_ECC_SBE_VOL_TOTAL` | Correctable errors (early warning) |
| ECC Errors (Double) | `DCGM_FI_DEV_ECC_DBE_VOL_TOTAL` | Uncorrectable errors (critical) |
| PCIe TX/RX | `DCGM_FI_DEV_PCIE_TX_THROUGHPUT` | Data transfer bottlenecks |
| XID Errors | `DCGM_FI_DEV_XID_ERRORS` | Driver/hardware errors |

## Example Alert Rules

```yaml
groups:
  - name: gpu-alerts
    rules:
      - alert: GPUMemoryHigh
        expr: DCGM_FI_DEV_FB_USED / DCGM_FI_DEV_FB_FREE > 0.9
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "GPU memory usage above 90%"

      - alert: GPUTemperatureHigh
        expr: DCGM_FI_DEV_GPU_TEMP > 80
        for: 2m
        labels:
          severity: warning
        annotations:
          summary: "GPU temperature above 80°C"

      - alert: GPUECCErrors
        expr: DCGM_FI_DEV_ECC_DBE_VOL_TOTAL > 0
        labels:
          severity: critical
        annotations:
          summary: "Uncorrectable ECC errors detected"
```

## Meme Opportunity
- "This is fine" dog meme but GPU is on fire and no monitoring
- "We have monitoring at home" - monitoring at home is just `nvidia-smi` in a loop
- Drake meme: "nvidia-smi manually" ✗ vs "DCGM Exporter + Grafana" ✓
