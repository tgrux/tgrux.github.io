1. Download and install [Vagrant](https://www.vagrantup.com/) and [VirtualBox](https://www.virtualbox.org/)

2. Download and extract the virtual box you need:
IE Box Locations:
* [Windows XP with IE6](http://aka.ms/ie6.xp.vagrant)
* [Windows XP with IE8](http://aka.ms/ie8.xp.vagrant)
* [Windows Vista with IE7](http://aka.ms/ie7.vista.vagrant)
* [Windows 7 with IE8](http://aka.ms/ie8.win7.vagrant)
* [Windows 7 with IE9](http://aka.ms/ie9.win7.vagrant)
* [Windows 7 with IE10](http://aka.ms/ie10.win7.vagrant)
* [Windows 7 with IE11](http://aka.ms/ie11.win7.vagrant)
* [Windows 8 with IE10](http://aka.ms/ie10.win8.vagrant)
* [Windows 8.1 with IE11](http://aka.ms/ie11.win81.vagrant)
* [Windows 10 with MSEdge](http://aka.ms/msedge.win10.vagrant)
 
3. run `Vagrant init`
4. update the vagrantfile 
  * `config.vm.box = "IE10 - Win8.box"`
  * Uncomment:
```
config.vm.provider "virtualbox" do |vb|
  # Display the VirtualBox GUI when booting the machine
  vb.gui = true

  # Customize the amount of memory on the VM:
  vb.memory = "4096"
end
```
5. run `vagrant up` to start ... might take a wile
6. run `vagrant destroy` to stop