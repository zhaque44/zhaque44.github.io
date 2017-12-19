---
layout: post
title: A custom fit to “testing your application”
date: 2017-11-27 04:00:00
tags: tesing application unittesting ruby python
author: Zubair Haque
---

<p>In my current project we are using Cucumber a popular BDD test framework. We basically have a wide range of tasks setup in our suite to accommodate various test needs for the rollout of features that need to be delivered within a two week sprint. The rake test tasks written in our Cucumber suite are very useful, we chain multiple “test tasks” together and leverage them, based on the regression testing we want to accomplish for the application under test.<p>
Here is a scenario we encountered recently:</i></b>
<p>I was testing on a feature branch that was implementing a major back-end change, I didn’t feel the need to run our end to end test suite due to the changes were in the back end. So I decided to create a smoke test task or a back-end test task that just runs the back-end tests. I thought this could serve as a repeatable task for developers run before they merge to our master branch, use it as somewhat of a pre-push task to make sure things are mostly intact.
</p><br><i>Creating a Rake task:</b></i><br>
<br>
Go to your Rakefile in your test directory and create your task there:
<code>
require ‘rubygems’
require ‘cucumber’
require ‘cucumber/rake/task’

Cucumber::Rake::Task.new(:backEndTests) do |t|
t.cucumber_opts = “features –color –format pretty –tags ~@backendtests -f json_pretty -o cucumber.json -f html -o cucumber.html”
end

</code>
<br><p>
The .new defines the task and allows us to name it “backEndTests”
We start our block of code with “do”
Then we utilize the “cucumber_opts” accessor to define the arguments that are being passed:
–color: shows the results of our tests in color
–format pretty: prints the contents of the feature file with proper indentation and alignment
–tags: we utilize the tag option to display exactly which set of tests we are running
-f: format output formatters for HTML & JSON
Then “end” the block of code
Once you have created the Rake task in your Rakefile, you can start going to your feature files and start tagging the back end specific tests you would like to run
Tagging scenarios:
</p><br>
<p>Feature: F111 — What my feature is doing</p><br>

<b>#Best Practice:</b> write notes for your tests, so other engineers can understand what you are testing
</p>
@backEndTests
Scenario: Explanation of the scenario I am testing
Given that I am logged in as “parameter” through the POST API request
When the user requests “parameter” in report format
Then the expected results display
<br>
Once you get to the feature file that has the back-end you are looking for add the test @tag above the scenarios you want to run in your suite.
You should be able to run your task now from the command line:
<br><code>
$rake backEndTests</code>
<br>
Once the back-end suite passes, we are ready to carry on with our regression efforts by making the proper REST calls to simulate or mimic the user actions in the back-end. After we have received successful response codes for the calls we were trying to make, we login from the UI and do validation on the front-end. As you can see our regression efforts are eagle-eye focused on the various areas that impact the changes made. Running a very targeted approach for our regressions suites saves us a lot of time and notifies us that the changes made aren’t breaking working software. In a scaled agile environment efficiency is key for Continuous Delivery.
