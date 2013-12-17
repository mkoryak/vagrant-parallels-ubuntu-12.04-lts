### Building a new vagrant parallels box from definitions (ubuntu-12.04-server-amd64)

**Requirements**:

 - you should have parallels installed (tested with 8)
 - make sure that you have ruby 1.9.2 installed
 - go to [http://downloads.vagrantup.com/](http://downloads.vagrantup.com/) and install it

```
vagrant plugin install vagrant-parallels
sudo gem install veewee
bundle exec veewee parallels define 'ubuntu-12.04-lts' 'https://github.com/mkoryak/vagrant-parallels-ubuntu-12.04-lts.git/definitions/parallels-ubuntu-12.04-server-amd64'
bundle exec veewee parallels build 'ubuntu-12.04-lts'  --workdir=.
bundle exec veewee parallels export 'ubuntu-12.04-lts' --workdir=.
```

Now you have a vagrant parallels box.

To import it into vagrant type:

```
vagrant box add 'ubuntu' './ubuntu-12.04-lts.box'
```

To use it:

```
vagrant init 'ubuntu'
vagrant up --provider=parallels
vagrant ssh
```

### Build another version/distro using this repo

You can build an ubuntu 12.10 or an ubuntu 13.10 and possibly even a different distro using this repo as a starting point.

You will need to pull down this repo and use one of the folders in the the defintions/ folder as a starting point. The 2 folders in there are:

- parallels-ubuntu-12.04-server-amd64-clean = a clean install containing dev tools and ruby
- parallels-ubuntu-12.04-server-amd64 = an install containing puppet, chef, dev tools and ruby

you will need to open the <code>defintion.rb</code> file and edit these 2 lines to point to the correct iso image:

```
:iso_file => "ubuntu-12.04.3-server-amd64.iso",
:iso_src => "http://releases.ubuntu.com/12.04/ubuntu-12.04.3-server-amd64.iso"
```

after that, you can build this defintion with veewee:  
```
bundle exec veewee parallels define 'box_name' 'path/to/your/defintion/dir'
bundle exec veewee parallels build 'box_nane'  --workdir=.
bundle exec veewee parallels export 'box_name' --workdir=.
```

