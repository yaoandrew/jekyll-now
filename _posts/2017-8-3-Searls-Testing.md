---
layout: post
title: Searls - How to stop hating your tests
---

![Searls Presentation Banner](/images/searls.png)
In Searls [video “How to stop hating your tests”](http://blog.testdouble.com/posts/2015-11-16-how-to-stop-hating-your-tests), Justin talks about 3 high level concepts with your tests - Structure, Isolation, and Feedback. The overall theme focuses on keeping the tests running quickly, easy to read and understand, and easy to change.

In discussing test structure he recommends keeping objects small. When there are too many dependencies there’s lots of test setup, when there are multiple side effects, there’s lots of verification, and when there are too many logical branches, there are too many potential outcomes to test.

He also recommends a very rigid structure to the tests so that they explicitly do 3 things - set stuff up, invoke a thing, verify behavior or otherwise known as- Given, When, Then. Sticking to this construct makes tests easier to read, can highlight certain code design smells, and may point out superfluous test code if it doesn’t fit within the construct. Some code design smells may be detected with too many “given” steps. You might think, are there too many dependencies are complex arguments? When there are multiple “when” steps you might consider if the API could be more user friendly or simplified and when there are many “then” steps you might consider if the code is doing too much or returning too complex a type.

He recommends keeping logic out of tests and keeping them easy to ready. You might be tempted to DRY out the test code, but that would require putting some logic in and test code is untested code, therefore, should not contain large amounts of logic. Simplicity is key.

He discusses the trade off between a small API that’s easy to learn but may lead to complex tests vs. a heavier DSL which does too much magical stuff but results in terse tests. In Ruby, this is analogous to minitest and rSpec. He recommends being very clean and consistent with the subject (what is being tested) and the result (what is being asserted). Tests should pass the squint test.

In the test isolation section, he reminds us to check that the purpose of the test is readily apparent and that the test suite is consistent. He discussed the testing pyramid and recommends that all test barbell towards the two extremes of high integration and low integration. At the top of the pyramid we’d be testing to see that the application is plugged together correctly. At the bottom, we’d be testing each thing in isolation to make sure it works correctly. Tests that are too realistic are bad since they can’t catch all potential issues and are slower. He give a few ways to identify and fix redundant test coverage.

In test feedback, Searls recommends making sure that test suite is giving good feedback and that the feedback loop is as fast and highly optimized as possible. He recommends less integration testing and states that they grow in time and complexity non-linearly. He even suggests capping the build time as a policy. Watch out for false negatives - failures of the test suite instead of failures of the build. Top causes are redundant coverage and slow tests.
