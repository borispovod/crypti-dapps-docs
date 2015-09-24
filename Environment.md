# Environment Setup

Before we can start building our first Crypti DApp. We first need to setup our development environment.

Please ensure the below requirements are met before continuing.

* Mac OS X or Linux
* Nodejs (v0.12)
* SQLite (v3.8)
* Npm
* Git

Currently we only support development on Mac OS X or Linux operating systems. If you don't have either, see below for instructions on installing a Ubuntu based environment using [Vagrant](https://www.vagrantup.com/).

**One important note**: Crypti's VM (Virtual Machine) is only secured on Linux operating systems. **Mac OS X** can be used for development purposes, **but in production you will need to use Linux based master nodes**.

## Vagrant Environment Setup (Optional)

**Skip this step if you are already using Mac OS X or Linux.**

1. Download and install the latest version of the following applications:

  * [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
  * [VirtualBox](https://www.virtualbox.org/)
  * [Vagrant](https://www.vagrantup.com/)

2. Open a Windows command prompt. Then make a project directory to store your environment.

  ```sh
  mkdir myfirstdapp
  cd myfirstdapp
  ```

3. Setup a Ubuntu based virtual machine using vagrant:

  ```sh
  vagrant init ubuntu/trusty32
  vagrant up
  ```

  Once the virtual machine has finished installing, you should have a fully functioning environment running Ubuntu 14.04 LTS 32-bit.

4. Verify the status of the virtual machine using the following command:

  ```sh
  vagrant status
  ```

  Vagrant should state the VM is running, and give instructions on how to shutdown or suspend it.

5. Next open PuTTY and login to your newly created VM using the following credentials:

  * IP address: 127.0.0.1
  * Port: 2222
  * Username: vagrant
  * Password: vagrant

6. Upon successful logon to your VM. Install the following required packages:

  ```sh
  sudo apt-get install git nodejs nodejs-legacy npm build-essential sqlite3
  ```

7. Your virtual machine environment should now be ready.

By default, Vagrant synchronizes your project directory between the local machine and client VM. For example, the contents of ```C:\Users\User\myfirstdapp``` are accessible as ```/vagrant``` on the client VM and vice versa.

For further information about using vagrant, please read the [official vagrant documentation](https://docs.vagrantup.com/v2/).

## Install Crypti

So, to start work on our DApp we first need to install an **Open Testnet** version of Crypti. This can be done by running the following commands:

```sh
wget <link to crypti open testnet version>
unzip 0.5.0-testnet.zip
cd 0.5.0-testnet
npm install --production
```

Then launch Crypti and verify our base testnet is working correctly:

```sh
node app.js
```

If successful, Crypti will launch and connect to the base testnet network.

Now let's install *crypti-cli* and finally start work on our first DApp:

```sh
sudo npm install -g crypti-cli
```

After installation completes, check that *crypti-cli* is installed correctly:

```sh
crypti-cli -h
```

Congratulations! We are now ready to create our first DApp! Let's continue with the next tutorial.
