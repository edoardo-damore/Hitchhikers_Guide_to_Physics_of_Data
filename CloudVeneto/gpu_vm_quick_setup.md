# Booking and Setupping a CloudVeneto (GPU) virtual machine

CloudVeneto offers great tools for Physics of Data students, but somethimes it can be tricky to properly setup stuff if you've never done it before.

Always consult [the official user guide](https://userguide.cloudveneto.it/en/latest/). 

*DISCLAIMER*: this tutorial was written as I actually did the setup for a virtual machine. 
It worked fine for me, but it may contain errors and it may not suit your specific needs.
Please do not follow blindly.

## 1. Book the GPU

You can do this in the [GPU booking calendar](https://cloudveneto.ict.unipd.it/dashboard/project/calendarpanel/).

## 2. Launch instance

Launch an instance with a valid flavour (e.g. "cloudveneto.15cores90GB25G+500GB1T4").

If you do not know how to launch an istance check the guide at [section 4.1](https://userguide.cloudveneto.it/en/latest/AdminVMs-nocontext.html#creating-virtual-machines).

## 3. Reformat the ephemeral volume at /mnt

Follow the steps on the cloudveneto guide at [section 4.9.1](https://userguide.cloudveneto.it/en/latest/AdminVMs-nocontext.html#flavors-with-supplementary-ephemeral-disk).

## 4. Install Cuda-toolkit and Cuda-drivers

1. Update the system:
```bash
sudo apt update && sudo apt upgrade -y
sudo reboot
```
2. Install required dependencies and build tools:
```bash
sudo apt install -y build-essential dkms linux-headers-$(uname -r)
```
3. Go [here](https://developer.nvidia.com/cuda-downloads) and select the right options based on the vm. 
Then follow the instructions. 
	Here is an example for Ubuntu 24.04 with x86_64 architecture (as of 27/07/2025):
	1. CUDA toolkit installation:
	```bash
	wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-keyring_1.1-1_all.deb
	sudo dpkg -i cuda-keyring_1.1-1_all.deb
	sudo apt-get update
	sudo apt-get -y install cuda-toolkit-12-9
	```
	2. Drivers installation:
	```bash
	sudo apt-get install -y cuda-drivers
	```
4. Reboot the system one last time:
```bash
sudo reboot
```
5. Test the installation with:
```bash
nvidia-smi
```

## 5. (Optional) Install conda on the ephemeral volume
1. Change the permissions for `/mnt`:
```bash
chmod 777 /mnt
```
2. Create a directory for miniconda and install it:
```bash
mkdir /mnt/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /mnt/miniconda3/miniconda.sh
bash /mnt/miniconda3/miniconda.sh -b -u -p /mnt/miniconda3
rm /mnt/minconda3/miniconda.sh
```
3. Refresh terminal:
```bash
source /mnt/miniconda3/bin/activate
```
4. Initialize conda on all shells:
```bash
/mnt/miniconda3/bin/conda init --all
```
5. Create a virtual environment on the ephemeral disk:
```bash
mkdir /mnt/miniconda3/conda-envs # this folder will store all environments
conda create -p /mnt/miniconda3/conda-envs/myenv python=3.12
conda activate /mnt/miniconda3/conda-envs/myenv
```
6. (Optional) Create a soft link in the home directory for faster activation:
```bash
ln -sf /mnt/miniconda3/conda-envs/ .
```
In this way you could activate the environment just with:
```bash
conda activate ~/conda-envs/myenv
```
