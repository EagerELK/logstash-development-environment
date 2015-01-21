# Step by step guide to set up a Logstash development environment

If you're keen to contribute to the Logstash project, you can do so by either contributing to the main [Logstash project][1] or to any of the [Logstash plugins][2]. Which ever you choose, you'll need to set up your Logstash development environment. This post will take you through setting it up.<!-- more -->

This has been formalized as an [Ansible playbook][3], but for completeness here are the manual steps.

## 1. Install JRuby

This can either by done by using a tool such as [rmv][4] or [rbenv][5], or, if you want to do it manually:

* Download and extract the version of JRuby you want
* Set `JRUBY_HOME` and add `JRUBY_HOME/bin` to the `PATH` environment variable. This is best done in `/etc/environment`
* Install the bundler and rspec gems:
    * `gem install bundler`
    * `gem install rspec`

## 2. Install Dependencies

You need to ensure that you have a JDK installed. Git is also a good idea. On Ubuntu you can do the following:

~~~
sudo apt-get install git openjdk-7-jdk
~~~

## 3. Get the source

All that's left is to get the source of Logstash (or the plugin) you want to work on:

~~~
git clone https://github.com/elasticsearch/logstash.git
~~~

## 4. Get to work

If you're working on a plugin, you need to run `bundle install` in the plugin's root. This will add the logstash source to the plugin (as it depends on logstash) and also add anything else you might need to test and develop the plugin. You can now run `bundle exec rspec` to run the tests for the plugin.

## Extra Resources

* Elasticsearch post on [plugin changes][6]
* [Ansible playbook and Vagrant setup][3] that automates all of this.

[1]: https://github.com/elasticsearch/logstash/
[2]: https://github.com/logstash-plugins/
[3]: https://github.com/EagerELK/logstash-development-environment
[4]: https://rvm.io/
[5]: http://rbenv.org/
[6]: http://www.elasticsearch.org/blog/plugin-ecosystem-changes/
