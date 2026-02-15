# 1:

1. https://github.com/fleeshka/DevOps-Intro/actions/runs/22035534716
![successful pipeline](image.png)

2. From this quickstart, I learned that GitHub Actions uses jobs (like "Explore-GitHub-Actions") which are sets of steps that run on a virtual machine called a runner (ubuntu-latest), and these workflows are automatically triggered by events such as triggers (like on: [push]). The steps can execute shell commands, check out repository code using actions like actions/checkout, and use contextual variables like ${{ github.event_name }} to access information about the workflow run.

3. A push event to the repository triggered the workflow run.

4. The workflow execution process begins when a push event triggers the workflow, which then launches a job on an Ubuntu runner that sequentially executes each step, including running echo commands, checking out the repository code with actions/checkout, and listing files in the workspace.

# 2:

1. Remove push trigger, added manual workflow_dispatch trigger, added a new step Gather system information

2.
```
System Information:
CPU Information:
Model name:                              AMD EPYC 7763 64-Core Processor

Memory Information:
               total        used        free      shared  buff/cache   available
Mem:            15Gi       999Mi        13Gi        39Mi       1.8Gi        14Gi
Swap:          3.0Gi          0B       3.0Gi

Operating System Details:
PRETTY_NAME="Ubuntu 24.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.3 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo

Kernel Version:
Linux runnervmjduv7 6.14.0-1017-azure #17~24.04.1-Ubuntu SMP Mon Dec  1 20:10:50 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux

Disk Usage:
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       145G   53G   92G  37% /
tmpfs           7.9G   84K  7.9G   1% /dev/shm
tmpfs           3.2G 1008K  3.2G   1% /run
tmpfs           5.0M     0  5.0M   0% /run/lock
efivarfs        128M   32K  128M   1% /sys/firmware/efi/efivars
/dev/sda16      881M   63M  757M   8% /boot
/dev/sda15      105M  6.2M   99M   6% /boot/efi
tmpfs           1.6G   12K  1.6G   1% /run/user/1001

CPU Current Load:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st 
```

3. Manual triggers (workflow_dispatch) give control over when a workflow runs by requiring explicit user action through the GitHub UI, while automatic triggers (like push) execute workflows immediately whenever specified events occur in the repository without human intervention.

4. The GitHub Actions runner provides a powerful cloud-hosted virtual environment with an AMD EPYC 64-core processor, 15GB of RAM, and 145GB of storage running Ubuntu 24.04 LTS on Azure infrastructure. With near-idle CPU usage (100% idle), minimal memory consumption (only ~1GB used), and Ubuntu 24.04 with kernel 6.14, this runner offers robust performance capabilities suitable for building, testing, and deploying applications without resource constraints.
