# Step by step guide to set up a Logstash development environment

If you're keen to contribute to the Logstash project, you can do so by either contributing to the main [Logstash project][1] or to any of the [Logstash plugins][2]. Which ever you choose, you'll need to set up your Logstash development environment. This post will take you through setting it up.<!-- more -->

This can either by done by using a tool such as [rvm][4] or [rbenv][5], or, by following the steps set out below.  Both the manual method, as well as using rvm has been formalized as [Ansible playbooks][3].

## 1. Install Dependencies

You need to ensure that you have a JDK installed. Git is also a good idea. On Ubuntu you can do the following:

~~~
sudo apt-get install git openjdk-7-jdk
~~~

## 2. Install JRuby

* Download and extract the version of JRuby you want
* Set `JRUBY_HOME` and add `JRUBY_HOME/bin` to the `PATH` environment variable. This is best done in `/etc/environment`
* Install the bundler and rspec gems:
    * `gem install bundler`
    * `gem install rspec`

## 3. Get the source

All that's left is to get the source of Logstash (or the plugin) you want to work on, and initialize the install:

~~~
git clone https://github.com/elasticsearch/logstash.git
cd logstash
bundle install
~~~

Or, if you're working on a plugin:

~~~
git clone https://github.com/logstash-plugins/logstash-filter-mutate.git
cd logstash-filter-mutate
bundle install
~~~

If `bundle install` or `bundle exec rspec` fails, it might be that bundle / ruby is pointing to a MRI installation of Ruby, not the JRuby version. The error messages you're likely to receive are as follows:

~~~
$ bundle install
Gem::FilePermissionError: You don't have write permissions for the /usr/local/rvm/gems/jruby-1.7.18/bin directory.
~~~

The fix for this is to add `export GEM_HOME=$(ruby -e 'puts Gem.user_dir')` to your `.bashrc` file.

~~~
$ bundle exec rspec
You have requested:
  logstash-devutils >= 0

The bundle currently has logstash-devutils locked at 0.0.7.
Try running `bundle update logstash-devutils`
Run `bundle install` to install missing gems.
~~~

You're probably using an MRI install of bundler. Ensure that you switch to JRuby and install the JRuby gems.

## 4. Get to work

If `bundle install` was successful, the logstash base would have been initialized with the necessary gems and plugins. If you're developing a plugin, the logstash source would have been added as a gem dependency, and you'll be ready to start developing and testing it. You can now run `bundle exec rspec` to run the tests for the plugin.

## Extra Resources

* Elasticsearch post on [plugin changes][6]
* [Ansible playbook and Vagrant setup][3] that automates all of this.
* [Ansible playbook to install RVM][7]
* [EagerELK - The Elasticsearcmh, Logstash and Kibana][8] Blog

--------------------------

Created and Maintained by [Jrgns][9], maintainer of [EagerELK][8].

[1]: https://github.com/elasticsearch/logstash/
[2]: https://github.com/logstash-plugins/
[3]: https://github.com/EagerELK/logstash-development-environment
[4]: https://rvm.io/
[5]: http://rbenv.org/
[6]: http://www.elasticsearch.org/blog/plugin-ecosystem-changes/
[7]: https://github.com/rvm/rvm1-ansible
[8]: http://blog.eagerelk.com/
[9]: http://jrgns.net

