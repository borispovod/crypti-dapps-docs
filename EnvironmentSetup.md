# Setting up an Environment

Before we can start building our first Crypti dapp, we must first setup our development environment.

Please ensure the below requirements are met before continuing.

* Mac OS X or Linux
* [Nodejs](https://nodejs.org/dist/latest-v0.12.x/) (v0.12)
* [SQLite](https://www.sqlite.org/download.html) (v3.8)
* [Npm](https://www.npmjs.com/)
* [Git](http://www.git-scm.com/)

Currently we only support development on Mac OS X and Linux operating systems. If you don't have either, see below for instructions on installing an Ubuntu based environment using [Vagrant](https://www.vagrantup.com/).

**One important note**: Crypti's VM (Virtual Machine) is only secured on Linux operating systems. **Mac OS X** can be used for development purposes, **but in production you will need to use Linux based master nodes**.

## Vagrant Environment Setup (Optional)

**Skip this step if you are already using Mac OS X or Linux.**

1. Download and install the latest version of the following applications:

  * [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
  * [VirtualBox](https://www.virtualbox.org/)
  * [Vagrant](https://www.vagrantup.com/)

2. Open a Windows command prompt. Then make a directory to store your environment.

  ```sh
  mkdir crypti
  cd crypti
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
  sudo apt-get install git nodejs nodejs-legacy npm build-essential sqlite3 unzip
  ```

7. Your virtual machine environment should now be ready.

By default, Vagrant synchronizes your project directory between the local machine and client VM. For example, the contents of ```C:\Users\User\crypti``` are accessible as ```/vagrant``` on the client VM and vice versa.

For further information about using vagrant, please read the [official vagrant documentation](https://docs.vagrantup.com/v2/).

## Install Crypti

To start work on our dapp, we first need to install an **Open Testnet** version of Crypti. This can be done by running the following commands:

On **Mac OS X** operating systems:

```sh
wget http://downloads.crypti.me/crypti-node/development/macos-0.5.0.zip
unzip macos-0.5.0.zip
cd 0.5.0
npm install --production
```

On **Linux** operating systems (or vagrant):

**TIP:** If using vagrant, it is a good idea to change to the shared: `/vagrant` directory as described above. This way, you can easily access your dapp's files from within the host operating system.

```sh
wget http://downloads.crypti.me/crypti-node/development/linux-0.5.0.zip
unzip linux-0.5.0.zip
cd 0.5.0
npm install --production
```

Then launch Crypti and verify our base testnet is working correctly:

```sh
node app.js
```

If successful, Crypti will launch and connect to the base testnet network.

Now let's install **crypti-cli** and finally start work on our first dapp:

```sh
sudo npm install -g crypti-cli
```

After installation completes, check that **crypti-cli** is installed correctly:

```sh
crypti-cli -h
```

If successful **crypti-cli** should yield the following output:

```
Usage: crypti-cli [options] [command]

Commands:

    dapps [options]      Manage your dapps
    contract [options]   contract operations
    crypto [options]     crypto operations

Options:

    -h, --help     output usage information
    -V, --version  output the version number
```

Congratulations! We are now ready to create our first dapp! Let's continue with the [next tutorial](BasicDapp.md).
