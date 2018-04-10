---
layout: post
title: The power of unittests paired with
date: 2018-04-10 04:00:00
tags: unittesting flexibility requests
author: Zubair Haque
---

<amp-img width="100" height="50" layout="responsive" src="../assets/images/unittesting.JPG"></amp-img>

In my current role I am the only Software Development Engineer in Test in charge of all Quality Control Processes and activities in a fast paced <i><b>Continuous Integration</b></i> model. The team that I am a part of is working on modernizing a product platform that is currently deployed in several countries worldwide. The APIs have documentation which describes what endpoints require what <i><b>headers and parameters</b></i>, as well as what different <i><b>response status codes</b></i> to expect and so on. Being short-staffed, I needed to pick a framework that would be <i><b>lightweight</b></i> & <i><b>easy to pick up</b></i>. Also, it should be something the <i><b>entire</b></i> team is comfortable with (I <i><b>stress</b><i/> that the most, because of the following):

When your team is <b><i>continuously</i></b> making changes and you have coverage with a <b><i>good set of tests</i></b>, your team members will rely on the <b><i>testing suite</i></b> prior to merging changes.

I decided to go with <b><i>unittest</i></b>, it’s pretty easy to understand and has tons of good documentation (if you like JUnit, unittest should be even easier to pick up). The <b><i>unittest</i></b> module comes with Python’s standard library, providing a <b><i>class</i></b> called <code>TestCase</code>

```python
class NameofClass(unittest.TestCase):
```
by passing in <i>(unittest.Testcase)</i> as an argument it basically allows you to pull in all of the goodness that is built in to <b><i>unittest</i></b>.

You can have an unlimited amount of <b><i>test_methods</i></b> in your test class, just remember you have to preface the name of all test methods with <b><i>test:</i></b>

<code>def test_name(self, session):</code>

Now once you defined all of your test methods in your <code>TestCase</code> you must add <code>unittest.main()</code> at the end of the file:

```python
if __name__ == '__main__':
    unittest.main()
```

when <code>unittest.main()</code> is called, it imports the entire module, then examines it by getting a list of all <b><i>functions</i></b> in that file and then runs them.

Make sure to <code>add__init.py__</code> at the <b><i>BASEDIR</i></b> level of your test suite, your directory structure should look like:

```python
└── test
    ├── __init__.py         
    └── test_validation_of_service.py
```

<code>__init__.py</code> is used to initialize Python packages (for now let’s leave it empty). The file can be used to import selected <b><i>classes</i></b> & <b><i>functions</i></b> into the package level so they can be conveniently imported.

```ruby
#example

from package import file
```
Now you can run your test suite:

```ruby
$ python3 -m unittest
```

and <b><i>voila!</i></b> It’s that simple. Now, I’m ready to test the various <b><i>web services</i></b> that belong to the API. As mentioned above, I need to validate that the <b><i>proper response status codes</i></b> are being returned as well as asserting the <b><i>JSON</i></b> being returned from each request.
