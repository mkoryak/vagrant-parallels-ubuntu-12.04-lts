### Building a new vagrant box from definitions (ubuntu-12.04-server-amd64)

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


