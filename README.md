# AI-AWS-GPU-EC2-Config

DETAILS CONFIGURATION FOR A GPU EC2 INSTANCE ON A VIRTUAL AWS CLOUD SERVER

WARNING: Check AWS Fees, As This Can Become Expensive!!

Set up to do AI with CMake compiler

INSTALL

I set up my own Amazon AWS EC2 instance without using an NVIDIA GPU CLOUD image due to some repos' inability to use the latest CUDA and cuDNN versions. The EC2 instance was an Ubuntu 16.04 virtual server. I accessed it with Putty and WinSCP from my Windows 10 machine.

I used CUDA 8 and cuDNN 7.3.1

The way I set up the instance was by going to http://aws.amazon.com/contact-us/ec2-request and creating a case regarding a service limit increase, limit type EC2 Instances, and requesting a p2.xlarge instance type. If you type exactly "fast.ai MOOC" in the case description, they will get back to you extremely fast.

I set up Docker and pulled a Tensorflow image that worked with those CUDA and cuDNN versions. I set 120 GB for my instance when setting it up.

I was in the /home/ubuntu directory. ubuntu was the username that the server gave me. This is the code I wrote:

sudo apt-get update

sudo apt-get upgrade

sudo apt-get install openjdk-8-jdk git python-dev python3-dev python-numpy python3-numpy build-essential python-pip python3-pip python3-venv swig python3-wheel libcurl3-dev

sudo apt-get install -y gcc g++ gfortran git linux-image-generic linux-headers-generic linux-source linux-image-extra-virtual libopenblas-dev

sudo add-apt-repository ppa:graphics-drivers/ppa -y

sudo apt-get update

sudo apt-get install -y nvidia-375 nvidia-settings

wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb

sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb

sudo apt-get update

sudo apt-get install cuda

nvidia-smi

sudo apt-get update

sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository “deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable”

sudo apt-get update

sudo apt-get install docker-ce

sudo docker run hello-world

sudo usermod -aG docker $USER

docker pull tensorflow/tensorflow:latest-gpu-py3

sudo apt-get install -y python3-venv

python3 -m venv my_env

source my_env/bin/activate

pip install tensorflow

I then set up cmake by downloading the appropriate .sh file on my local machine and using WinSCP to transfer the file to the virtual server. I used ./<cmake_filename>.sh to install cmake I then connected it to my PATH using PATH=$PATH:/<bin_directory_with_cmake_file>

And you should be good to go!
