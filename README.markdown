Scheduler Daemon
================

Rails 2.2.2 compatible scheduler daemon.  Replaces cron/rake pattern of periodically running rake tasks 
to perform maintenance tasks in Rails apps. Scheduler Daemon is made specifically for your Rails app, 
and only loads the environment once, no matter how many tasks run.

What's so great about it?  Well, I'm glad you asked!

- Only loads your Rails environment once on daemon start, not every time a task is run
- Allows you to easily deploy the scheduled tasks with your Rails app instead of depending on an
  administrator to update crontab
- It doesn't use rake or cron!
- Gets you up and running with your own daemon in under 2 minutes

Setup
=====

Install the plugin

    script/plugin install git://github.com/ssoroka/scheduler_daemon.git

Install required gems

    gem sources -a http://gems.github.com # if you haven't already...

    sudo gem install daemons rufus-scheduler eventmachine

If you want to be able to use english time descriptions in your scheduled tasks, like:

    scheduler.every '3h', :first_at => Chronic.parse('midnight')

then install Chronic:

    sudo gem install chronic

generate the scheduler daemon files in your rails app:

    script/generate scheduler

Usage
=====

generate a new scheduled task:

    script/generate task MyTaskName

fire up the daemon in console mode to test it out

    ruby scheduler/bin/scheduler_daemon.rb run

When you're done, get your system admin (or switch hats) to add the daemon to the system start-up, and
capistrano deploy scripts, etc.  Something like:

    ruby /path/to/rails/app/scheduler/bin/scheduler_daemon.rb start

Author
======

Steven Soroka

* [@ssoroka](http://twitter.com/ssoroka)
* [My Github repo](http://github.com/ssoroka)
* [My blog](http://blog.stevensoroka.ca)

Thanks
======

Special thanks to [Goldstar](http://www.goldstar.com) for sponsoring the plugin and promoting open-sourcesness.
