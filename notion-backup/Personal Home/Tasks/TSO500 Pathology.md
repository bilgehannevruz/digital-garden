---
Status: Not started
Priority: Medium
---
## Description

```Mermaid
flowchart LR
  START --> TSO500_GS
	START --> TSO500_AUMC
  START --> TSO500_AUMC+HRD_samples
  TSO500_GS --> STOP
	TSO500_AUMC --> STOP
	TSO500_AUMC+HRD_samples --> STOP
```

  

  

## Franklin requires

- BAM
- VCF
- QualityMetrics (QualityMetrics.tsv)
- OS update is up to us. Once we verify, they trust us.

  

- 15 custom panels 600 samples each year. Each week 12 samples