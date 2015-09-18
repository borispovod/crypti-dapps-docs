# Environment Setup

Before we start work on your first Crypti DApp, let's setup environment.

Required:

  * Nodejs (v0.12)
  * Npm
  * Git
  * Mac OS/Linux

Please, install this all components. Right now we support developing only on Mac OS or Linux.
If you don't have it, try to install Ubuntu via [vagrant](https://www.vagrantup.com/)

## Up vagrant environment (Optional)

**Skip this step if you have Mac OS/Linux already**

Install vagran from their [site](https://www.vagrantup.com/)

Then run this command:

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


