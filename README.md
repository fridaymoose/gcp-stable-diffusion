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

Please note that sometimes GCP is not able to allocate requested resources and launch your instance, see possible options below:
- wait 3-5m and try create / launch instance again
- change configuration, quite often more expensive GPU or machine type is available
- recreate your configuration in another location
- update region / zone if you're experienced enough and know what you do

## Stable Diffusion setup
Finally, you have VM up and running. It's high time to finalize the setup and get Stable Diffusion aboard
1. Navigate to `Virtual Machines - VM instances` and hit `SSH` button in the `Connect` column
2. Allow current user to manage GCP console, asked automatically
3. Setup GPU driver following [the next guide](https://cloud.google.com/compute/docs/gpus/install-drivers-gpu)
   - Run the next command `curl https://raw.githubusercontent.com/GoogleCloudPlatform/compute-gpu-installation/main/linux/install_gpu_driver.py --output install_gpu_driver.py`
   - Run the next command `sudo python3 install_gpu_driver.py`
   - Verify setup running `sudo nvidia-smi`
4. Now lets continue with Stable Diffusion setup, see more details on [preconditions](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Dependencies) and [install guide](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Install-and-Run-on-NVidia-GPUs)
   - As it was mentioned before, SD works fine with `Python 3.9.2` thus upgrade to `Python 3.10.6` can be skipped
   - Run the next command `sudo apt install wget git python3 python3-venv`
   - Clone Stable Diffusion on your machine by running `git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git`

TBD

## DreamBooth setup
TBD
