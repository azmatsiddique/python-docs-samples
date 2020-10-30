# App Engine Task Push Queue Migration Sample

This sample replaces the
[App Engine Tasks Queue Push Counter sample](../../../taskqueue/counter)
that used the `taskqueue` library
available only in the App Engine Standard for Python 2.7 runtime.

The sample uses a
[Cloud Tasks queue](https://cloud.google.com/tasks/docs)
as recommended in
[Migrating from Task Queues to Cloud Tasks](https://cloud.google.com/tasks/docs/migrating)
to perform the same functions as the earlier Task Queue sample.

The application has three functions:

* Viewing the home page will display a form to specify a task name, and add
  one more request for it. It will also show all requested tasks and their counts.

* Submitting the form on the home page will queue a task request.

* Tasks POSTed to `/push-task` will be processed by updating the count of
  the named task.

## Setup

Before you can run or deploy the sample, you will need to do the following:

1. Enable the Cloud Tasks API in the
[Google Developers Console](https://console.cloud.google.com/apis/library/cloudtasks.googleapis.com).

1. Set Firestore to Datastore mode in the
[Google Developers Console](https://console.cloud.google.com/datastore/welcome).

1. Create a queue in the
[Google Developers Console](https://console.cloud.google.com/cloudtasks).

1. Update the environment variables in ``app3.yaml`` for Python 3, or
``app.yaml`` for Python 2.7.

## Running locally

When running locally, you can use the [Google Cloud SDK](https://cloud.google.com/sdk)
to provide authentication to use Google Cloud APIs:

    $ gcloud init

Install dependencies, preferably with a virtualenv:

    $ virtualenv env
    $ source env/bin/activate
    $ pip install -r requirements.txt

Then set environment variables before starting your application:

    $ export GOOGLE_CLOUD_PROJECT=[YOUR_PROJECT_NAME]
    $ export LOCATION=[YOUR_PROJECT_LOCATION]
    $ export QUEUE=[YOUR_QUEUE_NAME]
    $ python main.py

## Running on App Engine

In the current directory, deploy using `gcloud`. For Python 2.7 you must first
install the required libraries in the `lib` folder:

    $ pip -t lib -r requirements.txt
    $ gcloud app deploy app.yaml

For Python 3, only need to run the deploy command:

    $ gcloud app deploy app3.yaml

You can now access the application using the `gcloud app browse` command.