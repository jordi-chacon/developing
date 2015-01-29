##### Random failures kill a team's performance
*29-01-2015* In the systems I have worked with to this date, we have always suffered from randomly failing testcases. This is due to testcases depending on a really not obvious particular state of the system in order for them to succeed. Depending on the execution order of all tests, a particular test might succeed now and fail in the next run.

I cannot stress enough how this issue kills the productivity of a team and increases its frustration. Also, once your system has randomly failing testcases, it is hard to get rid of them completely. They always manage to come back.

Therefore, it is super important to put extra focus on avoiding this when building a new system.

<br />
##### Run all your tests in less than 10 minutes
*29-01-2015* In the systems I have worked with to this date, test runs took 90 minutes in average. This is another great way to kill productivity and team performance. An acceptable test run time is probably less than 10 minutes.

If your system is a monolyth, when you make a tiny little change, you just need to run all your tests. You will most likely end up having test runs that take forever, it's just a matter of time.

On the other hand, if your system is made up of a bunch of small services and you make a tiny change in service S1, you should only need to run the tests for S1 and all system tests that verify that the services work well together. This should be doable in less than 10 minutes.

<br />
