---
published: false
---
Took on a Ruby issue from [Operation Code's Backend](https://github.com/OperationCode/operationcode_backend) to do some url validation when creating/updating a listing in their Code Schools. The validation part was simple enough using some Regular Expression for the 'format' part of the model validation and ensuring the school was using HTTPS. The tricky part came when I had to go clean up the tests. The individual test I wrote for the validation worked fine but not a few other tests were broken from the change. Turns out, the FactoryGirl Faker they were using to mock data for testing was generating HTTP urls. Tests were throwing errors every time they created a new mock code school to test against. This was good, because that meant my validation was working, but then I had to go learn how to update the FactoryGirl so it would spit out HTTPS.

Before figuring out the FactoryGirl stuff, I wanted to see what was going on in the tests. However, in the Makefile for `make test`, it was using `docker-compose run ${RAILS_CONTAINER} bash -xc 'export RAILS_ENV=test && bundle exec rake db:test:prepare && bundle exec rake test && bundle exec rubocop'`.

Let's break that down a bit:

- `docker-compose run ${RAILS_CONTAINER}` *bash -xc 'export RAILS_ENV=test && bundle exec rake db:test:prepare && bundle exec rake test && bundle exec rubocop'* 
	- This tells docker that we're about to run a command in a new specified container
- *docker-compose run ${RAILS_CONTAINER}* `bash -xc` *'export RAILS_ENV=test && bundle exec rake db:test:prepare && bundle exec rake test && bundle exec rubocop'* 
	- This allows you to run a bash command. The `x` switch tells it to output every command broken up by `&&` on it's own line and generally makes it cleaner (IMHO). The `c` switch tells bash that we're going to give it a string that is the command to be run.
- *docker-compose run ${RAILS_CONTAINER} bash -xc* `'export RAILS_ENV=test && bundle exec rake db:test:prepare` *&& bundle exec rake test && bundle exec rubocop'*
	- The first command sets an environment variable so Rails knows we're testing. The next rakes the DB with test data to make sure we have something to test against in the upcoming command.<br>
- *docker-compose run ${RAILS_CONTAINER} bash -xc 'export RAILS_ENV=test && bundle exec rake db:test:prepare &&* `bundle exec rake test` *&& bundle exec rubocop'*
	- Now we get to the actual test running. This is where I was hung up for a while trying to figure out verbose output to see which tests were throwing errors. I could have just searched the tests for `create(:code_school)` but that didn't dawn on me right away and I wanted to figure this bit out. First I tried `bundle exec rake test --verbose` to no avail. 
- Then I dug into a number of things:
	- Wanted to ensure each bash command was run as I thought, thus the `-x` switch for bash. Understanding `docker-compose run` was also good to make sure things went well.
	- Next I looked into MiniTest and how to make the `test` command verbose. But that led no where.
	- It was actually the combination of `rake test` that was causing the hangout. It needed some special syntax to enable verbose output. Also along that line fo thinking, I researched how to run only one specific test file instead of the whole thing (`bundle exec rake test TEST=test/controllers/api/v1/code_schools_controller_test.rb`).
- *docker-compose run ${RAILS_CONTAINER} bash -xc 'export RAILS_ENV=test && bundle exec rake db:test:prepare && bundle exec rake test &&*`bundle exec rubocop`'
	- This last little bit is just making sure that all the code formatting is consistent across the project. Very nice to have for someone working on this for the first time.</b></li>

All said and done, it was about 18 lines of code and I wrote my first test, which failed, then passed, but broke other things, but then passed everything. As of this writing, the [PR](https://github.com/OperationCode/operationcode_backend/pull/509) is approved and just awaiting merge. Fingers crossed and time to move onto the next project.

As it stands right now my goals/ideas to work towards are:</p>

- ~~Resolve URL validation issue for Operation Code~~
- Setup old tower as home media server
- JavaScript30 (JS/HTML/CSS) - in progress still
- LearnRubyTheHardWay using only keyboard - in progress
- Finish Reading Clean Code by Bob Martin - in progress
- Work on FactionC2 Module
- Write a YNAB App for MagicMirror (Node.js/Electron)
- Port my RadonTestManager to Ruby on Rails