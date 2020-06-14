# Using Travis

Evennia uses [Travis CI](http://travis-ci.org/) to check that it's building successfully after every commit to its Github repository (you can for example see the `build: passing` badge at the top of Evennia's [Readme file](https://github.com/evennia/evennia)). If your game is open source on Github you may also use Travis for free. See [the Travis docs](http://docs.travis-ci.com/user/getting-started/) for how to get started. 

After logging in you will get to point Travis to your repository on github. One further thing you need to set up yourself is a Travis config file named `.travis.yml` (note the initial period `.`). This should be created in the root of your game directory. The idea with this file is that it describes what Travis needs to import and build in order to create an instance of Evennia from scratch and then run validation tests on it. Here is an example: 

``` yaml
language: python
python:
  - "2.7"
install:
  - git clone https://github.com/evennia/evennia.git
  - cd evennia
  - pip install -e .
  - cd $TRAVIS_BUILD_DIR
script:
  - evennia migrate
  - evennia test evennia
  - evennia test
```

This will tell travis how to download Evennia, install it, set up a database and then run the test suite. 
You need to add this file to git (`git add .travis.yml`) and then commit your changes before Travis will be able to see it. 

For properly testing your game you of course also need to write unittests. [We have a page](Unit-Testing) on how we set those up for Evennia, you should be able to refer to that for making tests fitting your game. 