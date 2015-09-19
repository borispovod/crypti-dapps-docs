# Environment Setup

Before we start work on your first Crypti DApp, let's setup environment.

Required:

  * Nodejs (v0.12)
  * Npm
  * Git
  * Mac OS/Linux

Please, install this all components. Right now we support developing only on Mac OS or Linux.
If you don't have it, try to install Ubuntu via [vagrant](https://www.vagrantup.com/)

**One important note**: Crypti VM (Virtual Machine) secured only on Linux packages, because you can use **Mac OS** for developing, **but you need to use Linux packages on master nodes**.

## Up vagrant environment (Optional)

**Skip this step if you have Mac OS/Linux already**

Install vagran from their [site](https://www.vagrantup.com/).

To up virtual machine with Ubuntu package. Run this command:

```sh
vagrant init ubuntu/trusty32
vagrant up
vagrant ssh
```

After you logined to machine install git/nodejs/npm/build-essential:

``` sh
sudo apt-get install git
sudo apt-get install nodejs
sudo apt-get install nodejs-legacy
sudo apt-get install npm
sudo apt-get install build-essential
```

Great! Now you can [sync any folder](https://docs.vagrantup.com/v2/synced-folders/basic_usage.html) on your local machine with vagrant instance or just enable your IDE to working under ssh.

More info about vagrant [here](https://docs.vagrantup.com/v2/).

## Install Crypti

So, to start work on DApp we need to install Crypti Open Testnet Version.

``` sh
wget <link to crypti open testnet version>
unzip 0.5.0-testnet.zip
cd 0.5.0-testnet
npm install --production
```

Test that all installed good and base tesnet works:
``` sh
node app.js
```

Crypti must launched and connected to base testnet network .After installation successful done, let's install *crypti-cli* and finally start work on your first dapp:

``` sh
sudo npm install -g crypti-cli
```

After installation, check that all installed good:
``` sh
crypti-cli -h
```

Yes! We ready to create new dapp! Let's continue with next step.