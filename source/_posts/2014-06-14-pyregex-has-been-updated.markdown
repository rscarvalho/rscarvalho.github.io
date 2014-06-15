---
layout: post
title: "PyRegex has been updated!"
date: 2014-06-14 19:02
comments: true
categories: pyregex, python, regex, open source
---

Today I have been rolled a new version of [PyRegex](http://www.pyregex.com), with quite a big changeset on the backend.
PyRegex users are not expected to see any changes neither in behavior nor UI, but I'd like to cover the changes here in more detail.
The basic topics are:

* Flask as python webapp framework
* Python 3.4


#### Flask as python webapp framework

As some of you know, PyRegex started as a Google AppEngine app back in 2009. At that time, it was the only viable option given the project has no funding,
so it had to run on a free hosting provider. After the first release, I got some personal issues and wasn't able to maintain the project for a long time.

In 2013 I have decided do rebuild PyRegex from scratch. It was still on Google AppEngine, but I made use of some cool stuff on the frontend:
HTML5 and [AngularJS](http://angularjs.org).
On the backend I have changed the strategy, focusing on a RESTful API using [webapp2](http://webapp-improved.appspot.com/),
which is already included by default in the Google AppEngine SDK. The result was good overall (especially on the UI side), but the final product
were a bit overcomplicated and hard to maintain.

Unfortunately I had to move away from Google AppEngine due to restrictions on the runtime. I ended up hosting it on Heroku <sup>
[[1][issue]][[2][heroku]]
</sup>. I decided to keep `webapp2` as the web framework because it also runs outside Google AppEngine.

But as of now, I decided to remove the last Google AppEngine reference to PyRegex, and it is now a "pure python" application.

Recently I have looked at the [Flask webapp microframework](http://flask.pocoo.org). It's a very interesting project, very simple and flexible, which gives
power to the developer to do some really cool things.
application running on heroku.

PyRegex has now ported its API server to run on Flask without any drawbacks.

<p>&nbsp;</p>

#### Bumped runtime version to Python 3.4

Yes, I did it. PyRegex is officially running on py3k now. Some of you may say "But the majority of projects are still running on Python 2.x.
Python 2.x EOL [is set for 2020](http://legacy.python.org/dev/peps/pep-0373/)".

![Migrate to Python 3](https://i.imgflip.com/9knu7.jpg)

I have been planning to make this change for a long time, but I didn't manage my time to do so until now.
Python 3 is up for [more than 5 years now](https://www.python.org/download/releases/3.0/), and it's more than time for people and organizations to migrate.

And time has come to PyRegex. It's on Python 3.4 and it's not expected that you run into any issues testing your regular expressions, given the regex
matches didn't change from Python 2.x to 3.x.

As usual, you are more than welcome to [fork the project][github] on Github and/or [create an issue][all_issues] if you run into any problems!

[issue]: https://github.com/rscarvalho/pyregex/issues/9
[heroku]: http://heroku.com
[github]: https://github.com/rscarvalho/pyregex
[all_issues]: https://github.com/rscarvalho/pyregex/issues
