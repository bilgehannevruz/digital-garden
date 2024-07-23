---
Created: 2024-07-17T10:32
---
# GPU NODE

- [ ] OS is installed on RAM disk. Pbc01 should have similar as setup as gpu

  

  

- Followed steps
    - Register yum: `sudo subscription-manager attach --auto`
    - Install samba: `yum install samba`
    - Copy `passdb.tdb` file from previous os
- Network setup:
    - modify `ifcfg-Store10G`
        - …