# Mongo

## Summary

### Mongo

This is a database that will is intented to work with Node app

### CHEF

Chef is a software development kit delivering a set of tools for developing and testing Chef Cookbooks. It integrates the best of the breed tools created by Chef Community with Chef Client. Chef has a steep learning curve with lots of concepts and tools that have to be learned.

### Pre Requisites

- ChefDK
- git
- AWS credentials (for ec2 driver)

### Cookbook

This cookbook tests to see if mongodb is installed, configured and ready to use

#### Installs

```
mongodb-org
```

To use to test on aws ec2 driver use kitchen_cloud.yml then kitchen test

#### Unit test

to run unit tests

```
chef exec rspec
```

Unit test is a level of testing of each individual components of the software.

These are what the unit tests look for

```
should add mongo to the sources list
should install mongod
should update the mongod service config
should update the mongod.config
should enable the mongod service
should start the mongod service
```

#### Integration Test

To run integration test

```
kitchen test
```

Integration test is the level of testing where certain components are combined with others and tested together and these are some of the intgration test for this cookbook


```
describe package 'mongodb-org' do
  it { should be_installed }
  its('version') { should match /3\./ }
end

describe service 'mongod' do
  it { should be_running }
  it { should be_enabled }
end

describe port(27017) do
  it { should be_listening }
  its('addresses') { should include '0.0.0.0' }
end
```

To use to test on aws ec2 driver use kitchen_cloud.yml then kitchen test