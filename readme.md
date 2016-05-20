# Sonar Media Ripping VM

The latest install instructions will always be available at https://github.com/chimericdream/Sonar-Media-Ripper

## Latest Version

The current version of the Sonar VM is 1.0.0b.

## Installation

1. Install the latest version of [Vagrant](http://downloads.vagrantup.com/)
2. Install the latest version of [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
3. Install the latest version of Ruby
	* [Windows](http://rubyinstaller.org/downloads/)
	* [Mac/Linux](http://rvm.io/)
4. Clone this repository
	* `git clone git@github.com:chimericdream/Sonar-Media-Ripper.git ~/vagrant/sonar`
5. Run the setup script
	* `cd ~/vagrant/sonar;sh setup.sh`
	* This script makes sure you have the following items installed:
		* Vagrant VBGuest Plugin
		* Vagrant Omnibus Plugin
        * [Vagrant Proxy Configuration Plugin](http://tmatilai.github.io/vagrant-proxyconf/) (this plugin is optional but is installed if you use the setup script)
	* The script may require admin rights to run, so if it fails, run the script  with `sudo`
6. Start the VM
	* `cd ~/vagrant/sonar;vagrant up`

## Copyright and License

The MIT License (MIT)

Copyright (c) 2013-16 Bill Parrott

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.