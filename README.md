# Circle CI Jabba Orb

![CircleCI branch](https://img.shields.io/circleci/project/github/ayte-io/circle-ci-orb-jabba/release/0.1.svg?style=flat-square)

[Registry Link](https://circleci.com/orbs/registry/orb/ayte/jabba)

This orb provides interface to work with [shyiko/jabba][jabba] JVM 
version manager.

Sometimes you just need to change JVM during a step, in our case it was
necessity for javadoc with 9+ and JVM 8 for allure report generation
(since downstream jobs won't be triggered in case of failures, and it's 
either successful report from other job or no report at all).

Generally all you have to do to achieve that is just run `jabba/use` 
step:

```yaml
version: 2.1
orbs:
  jabba: ayte/jabba@<latest-version>
jobs:
  verify:
    docker:
      - image: circleci/openjdk:11
    steps:
      - checkout
      - run: java -version # 11
      - jabba/use:
          version: zulu@1.8
      - run: java -version # 1.8 
```

This project relies on `BASH_ENV` support, so other shells probably 
won't work.

## Licensing

Come on, it's free for all.

MIT / UPL-1.0

Ayte Labs, 2019

  [jabba]: https://github.com/shyiko/jabba
