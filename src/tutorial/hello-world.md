# Hello, World

Let's start by seeing TaskCluster in action.

## Signing In

It's very easy to get started with TaskCluster, but we will need to know a little bit about you.
We support sign-in by Mozillians, as well as by developers and employees with LDAP credentials.
If that doesn't sound familiar to you, head over to [Mozillians](https://mozillians.org) and set up a new account for yourself.
Now you're a Mozillian -- thanks for rocking the free web with us!

Visit the [Task Creator](https://tools.taskcluster.net/task-creator) and click the "Sign In" link in the upper right corner.
Sign in using whatever method best suits you.
If you just set up a Mozillians account, use that.
Click the "Grant Permission" button, which will return you to the task creator.

What you see in the text box is a bare-bones task description, looking something like this (the details may evolve as features are added):

    {
      provisionerId:      'aws-provisioner-v1',
      workerType:         'tutorial',
      created:            '2015-06-15Z12:00:00,
      deadline:           '2015-06-22Z12:00:00,
      payload: {
        image:            'ubuntu:13.10',
        command:          ['/bin/bash', '-c', 'echo "hello World"'],
        maxRunTime:       60 * 10
      },
      metadata: {
        name:             "Example Task",
        description:      "Markdown description of **what** this task does",
        owner:            "name@example.com",
        source:           "http://tools.taskcluster.net/task-creator/"
      }
    }

Happily, this is already set up to print "hello world"!
Submit the task, and click the resulting task ID to load the task inspector while the task is scheduled and run.

The fields in the task description are explained in greater detail throughout the rest of this documentation, but briefly:

 * `provisionerId` identifies the TaskCluster provisioner responsible for the compute resources that will execute the task.
   In this case, it is the [AWS Provisioner](/services/aws-provisioner/), which runs its tasks on Amazon EC2 instances using Docker.
 * `workerType` is a parameter specific to the AWS provisioner which identifies the pool of EC2 resources within which the task should be executed.
   Pools may use different EC2 instance types, AMIs, etc.
   In this case, we are using a worker type dedicated to running tasks in this tutorial.

 * `created` and `deadline` give a time boundary for the task.
   If the task is not completed by its deadline, it will be resolved as `exception` with reason `"deadline-exceeded"`.

 * The `payload` is interpreted by the Docker worker.
   The `image` key specifies the docker image to pull, and the `command` gives the command to run within that image.

In the task inspector, you will see your task description as executed, and indications of the task's status: pending, executing, and then finished.

The log view shows the output of the task, including that from downloading the docker image.
Scrolling all the way to the bottom, you should see the greeting output by the `echo` command.

You've run your first task!

# See Also

 * ["TaskCluster Hello World" video by mrrrgn and dustin](https://vreplay.mozilla.com/replay/showRecordingExternal.html?key=7AvN2iczQYcI3lY)

# Next Steps

OK, that was pretty simple -- but I can think of easier ways to print "hello world".  What's next?

 * [I want to look at some real tasks](finding-tasks)
 * [I want to know how the tools site works](interactive)
 * [I'm a Firefox / Gecko developer - how do my commits get built?](gecko-tasks)