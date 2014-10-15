#Vagrant

##[WHY VAGRANT?][1]

Vagrant provides easy to configure, reproducible, and portable work environments built on top of industry-standard technology and controlled by a single consistent workflow to help maximize the productivity and flexibility of you and your team.

To achieve its magic, Vagrant stands on the shoulders of giants. Machines are provisioned on top of VirtualBox, VMware, AWS, or [any other provider][2]. Then, industry-standard [provisioning tools][3] such as shell scripts, Chef, or Puppet, can be used to automatically install and configure software on the machine.

##[HOW VAGRANT BENEFITS YOU][1]

If you're a ```developer```, Vagrant will isolate dependencies and their configuration within a single disposable, consistent environment, without sacrificing any of the tools you're used to working with (editors, browsers, debuggers, etc.). Once you or someone else creates a single Vagrantfile, you just need to vagrant up and everything is installed and configured for you to work. Other members of your team create their development environments from the same configuration, so whether you're working on Linux, Mac OS X, or Windows, all your team members are running code in the same environment, against the same dependencies, all configured the same way. Say goodbye to "works on my machine" bugs.

If you're an ```operations engineer```, Vagrant gives you a disposable environment and consistent workflow for developing and testing infrastructure management scripts. You can quickly test things like shell scripts, Chef cookbooks, Puppet modules, and more using local virtualization such as VirtualBox or VMware. Then, with the same configuration, you can test these scripts on remote clouds such as AWS or RackSpace with the same workflow. Ditch your custom scripts to recycle EC2 instances, stop juggling SSH prompts to various machines, and start using Vagrant to bring sanity to your life.

If you're a ```designer```, Vagrant will automatically set everything up that is required for that web app in order for you to focus on doing what you do best: design. Once a developer configures Vagrant, you don't need to worry about how to get that app running ever again. No more bothering other developers to help you fix your environment so you can test designs. Just check out the code, ```vagrant up```, and start designing.

##INSTALLATION

[Virtualbox][4]

[Vagrant][5]

##QUICKSTART

![image](https://raw.githubusercontent.com/Dakarlug/vagrant_tutorial/master/images/vagrant-box.png)

##Boxes

Instead of building a virtual machine from scratch, which would be a slow and tedious process, Vagrant uses a base image to quickly clone a virtual machine. These base images are known as boxes in Vagrant, and specifying the box to use for your Vagrant environment is always the first step after creating a new Vagrantfile.

**Installing a box
**

Boxes are added to Vagrant with ```vagrant box add```. This stores the box under a specific name so that multiple Vagrant environments can re-use it.

```
$ vagrant box add hashicorp/precise32
```
![image](https://raw.githubusercontent.com/Dakarlug/vagrant_tutorial/master/images/box_add.png)

This will download the box named "hashicorp/precise32" from [Vagrant Cloud][6], a place where you can find and host boxes. While it is easiest to download boxes from Vagrant Cloud you can also add boxes from a local file, custom URL, etc.

Add box from local file or custom URL : ```vagrant box add {title} {url}```

```
$ vagrant box add openbsdbox https://github.com/jose-lpa/veewee-openbsd/releases/download/v0.5.5/openbsd55.box
```
or 

```
$ vagrant box add mydebian /home/boxes/debian-current.box 
```
More boxes can be found on [Vagrantbox.es][7]


**Using a box**

Now that the box has been added to Vagrant, we need to configure our project to use it as a base. Open the ```Vagrantfile``` in ```mylinuxbox``` box folder and change the contents to the following:


```
$ mkdir mylinuxbox && cd mylinuxbox
mylinuxbox$ vagrant init hashicorp/precise32
```
or

```
$ mkdir debian_vm && cd debian_vm
debian_vm$ vagrant init mydebian
```
Manually first:

```
mylinuxbox$ vagrant init
mylinuxbox$ vim Vagrantfile
```
second: set box name in Vagrantfile

```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise32"
end
```
or 


```
Vagrant.configure("2") do |config|
  config.vm.box = "mydebian"
end
```

##Up and ssh
It is time to boot your first Vagrant environment. Run the following:

```
mylinuxbox$ $ vagrant up
```

![image](https://raw.githubusercontent.com/Dakarlug/vagrant_tutorial/master/images/bvagrant_up.png)

You won't actually see anything though, since Vagrant runs the virtual machine without a UI.

```
mylinuxbox$ $ vagrant ssh
```
Take a moment to think what just happened: With just one line of configuration and one command in your terminal, we brought up a fully functional, SSH accessible virtual machine. 

[1]:https://docs.vagrantup.com/v2/why-vagrant/
[2]:https://docs.vagrantup.com/v2/providers/
[3]:https://docs.vagrantup.com/v2/provisioning/
[4]:https://www.virtualbox.org/wiki/Downloads
[5]:https://www.vagrantup.com/downloads.html
[6]:https://vagrantcloud.com/
[7]:http://www.vagrantbox.es/

