# Apollo installation

### 1. Mandatory installation package:

* For apollo to run perfectly, Ubuntu 18.04 is recommanded

* Install Nvidia GPU driver

  ```sudo apt-get update```

  ```sudo apt-add-repository multiverse```

  ```sudo apt-get update```

  ```sudo apt-get install nvidia-driver-455```

  __Notice:__

  If nvidia-smi does not have an output, install cuda toolkit

  ```  sudo apt install nvidia-cuda-toolkit ```

  ```reboot```

* Install Docker

  Installing using the repository.

  For details: reference https://docs.docker.com/engine/install/ubuntu/

  __set up the repository:__

  * Update the apt package index and install packages to allow apt to use a repository over HTTPS:

    ``` sudo apt-get update```

    ``` sudo apt-get install ca-certificates curl gnupg lsb-release```

  * Add Docker’s official GPG key:

    ``` curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg ```

  * Use the following command to set up the **stable** repository. To add the **nightly** or **test** repository, add the word nightly or test (or both) after the word stable in the commands below.[ ](https://docs.docker.com/engine/install/)

  * ``` 
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    
    
    ```

  

* **Install Docker Engine**

  * Update the apt package index, and install the *latest version* of Docker Engine and container

    ```sudo apt-get update ```

    ``` sudo apt-get install docker-ce docker-ce-cli containerd.io```

  * Verify that Docker Engine is installed correctly by running the hello-world image.

    ``` sudo docker run hello-world```

  __Noticed:__

  * Docker user group permission deny:

    ``` sudo groupadd docker```

    ```sudo gpasswd -a $USER docker```

    ``` newgrp docker ```

* *__Solution for not able to use GPU:__*

  For NVIDIA GPU, please update driver under the *Additional Drives* in *Software & Update*

  ![img](/home/xli149/Documents/ADAS/3Yrc3qVIWOwGlNZODhZ4PoKHKUBrs8m-SZWmL7eSs_uOSW1VxcnAr6HSBIK3oD7DjV1TT-GMCH3f8V0bHuMQLcUvfC8KTi-fqgieGbcvLERxm51-lNx3b1VB_LY2NADJHbC30qhx)

   

  *For testing your GPU Performance, check Unigine_Heave benchmark*

* *__Solution for nvidia-smi with command error: Failed to initialize NVML: Driver:__*

  * Uninstall nvidia driver:

    ``` sudo apt-get purge nvidia*```

  * Check for available driver version:

    ```ubuntu-drivers devices```![img](https://lh4.googleusercontent.com/618NhziZkFy44pttDM-1cFxF4m8mnP17nYw0d_7Lxpd1niPNVfv7vXnMH04vjGrJNImSiivtlDPKPd8C695wN10QdRKVHzdX6kTx5kkwwSVWQf56HedDY266uv3dQ5wxsH8H9vKt)

  * Check kernel version:

    ```cat /proc/driver/nvidia/version```

    For example, we try to install version 440:

    ``` sudo apt-get install nvidia-driver-440 nvidia-settings nvidia-prime ```

  * Adjust System driver:

    software & update->additional Drivers

    select _nvidia-driver-440_ and click _apply changes_ and then try:

    ​	``` conda install -c anaconda pytorch-gpu```

  * Added Nvidia Container Toolkit for docker images:

    

    ```distribution=$(. /etc/os-release;echo $ID$VERSION_ID)```

    ```curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -```

    ```curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list```

    ```sudo apt-get -y update```

    ```sudo apt-get install -y nvidia-docker2```

    ```sudo systemctl restart docker```

    

# Install Apollo

* Download installation package:

  https://apollo.auto/developer_cn.html

*  Unpack the installation package:

  ``` tar -xvf apollo_v6.0_edu_amd64.tar.gz```

* Install:

  cd to root directory

  ``` ./apollo.sh```

# Use Dreamview to check data packages (For record data package)

* Access into Apollo Docker:

  ```./apollo.sh```(do not use root, or you may not be able to locate qt library)

* Start Dreamview:

  ```bash scripts/bootstrap.sh```

* Dowload demostration record data packages:

  ```wget https://apollo-system.cdn.bcebos.com/dataset/6.0_edu/demo_3.5.record```

* Play the apollo record data package:

* ```cyber_recorder play -f demo_3.5.record --loop```

  __Noticed:__ if error_cyber_recorder command not found_ pops up:

  try: ```source cyber/setup.bash ``` to add _cyber_recorder_ to the evironment path.

  option:--loop. Using for set loop play mode

* Use Dreamview to check the result:

  Type http://localhost:8888 in any browser(chrome recommanded), to access Apollo Dreamview:

  ![img](/home/xli149/Documents/ADAS/EglphIcVpq5DCHKESJlpx2PybB8ZeRHckMpqcCfNNvl_Pc1S_7J7KqbQEnF9rRb4K3uzID1gZ-1MEKKELrEu1xzp_twoqe0mBtjI0jf3s5PeQK3DG39FAEoP-xiCjY2DU4EbQNHH)

