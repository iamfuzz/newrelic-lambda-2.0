+++
title = "New Relic Serverless for AWS Lambda: Distributed Tracing"
chapter = false
weight = 3
+++

Now that we have intentionally instituted an error in our code and generated some traffic on our Bookstore application since implementing that error, let's take a look at how New Relic for AWS Lambda's distributed tracing feature can help us diagnose problems like this that might occur in the real world.

Hop on over to the distributed tracing page by clicking on the **Distributed tracing** link located in the navigation menu on the left side of the screen in the section labeled *MONITOR*:

![Distributed Tracing](/images/distributed_tracing/distributed-tracing.png)

Click on the name of the most recent trace which should have *2* spans and *1* errors:

![Latest Trace](/images/distributed_tracing/latest-trace.png)

Other traces in your list should have shown as having *3* spans, which immediately tells us that part of our code that usually exectutes is no longer being executed.  Let's see if our logs have anything useful to tell us.  Click on the small **See logs** link at the top right hand corner of your screen:

![See Logs](/images/distributed_tracing/see-logs.png)

Here we can see the CloudWatch logs that were created during this particular execution of our Lambda function.  Note, the word *Error* is highlighted by default.  Looking at the line containing error, we can quickly see that we have an undefined variable by the name of *dynamoDB* and are presented with the filename and line number where the error occured:

![Log Error](/images/distributed_tracing/log-error.png)
