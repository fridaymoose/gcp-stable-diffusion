#  How to deploy Stable Diffusion on Google Cloud Platform (GCP)

## Preconditions
1. Register an account on [Google Cloud Platform](https://cloud.google.com/free)
2. Activate `Free Tier`, you need a creadit card with $1
3. Request GPU quota `1`

## VM instance
1. Navigate to `Virtual Machines - VM instances` and hit `Create instance` button
2. Pick region and zone
   - Specific GPU might not be available in target region / zone
   - Prefer closes region to eliminate network lags
3. Under `Machine Configuration` select `GPUs` tab
4. `NVidia T4` is offered by default, leave it as is
5. Navigate to `Machine type` and select from compatible N-series
   - you need at least 2 vCPU
   - you need at least 16Gb of RAM
   - as it goes from practice, `n1-highmem-4` is good enough even for multiuser mode
6. Under `Boot disk` ensure that `Debian GNU/Linux 11 (bullseye)` is selected
   - Debian 11 has `Python 3.9.2` preinstalled thus no additional update is necessary
   - ensure that disk has at least 20Gb of space because each nice model is 2-4Gb
   - don't worry about GPU driver, it can be setup later
7. Under `Firewall` section tick `Allow http` and `Allow https` checkboxes
   - exposed ports can be easily adjusted later
