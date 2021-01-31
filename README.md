# Consume Events using Journaling API

This codelab will guide you through creating cron jobs in a Firefly application to consume events using jouranling API

## User Story
There is a class of Firefly apps in which customers want guarantees that the I/O Events are processed without losing any event especially 
when there is a surge of events, a runtime webhook would return 429 response beyond the concurrency limit, thereby causing the webhook to be 
marked unreachable and causing no further events to be delivered. In this use case, the journaling API of custom events would be useful here. 

## Solution
- Using [Journaling API](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/api/journaling_api.md) to retrieve the events instead of relying on the webhook approach.
- Use a runtime action that uses the [Alarm package](https://adobeio-codelabs-alarms-adobedocs.project-helix.page/?src=/README.html) to read the events every X minutes.
- The alarm action stores the events in the Firefly storage [aio-lib-state](https://github.com/adobe/aio-lib-state).
- Index of events has been recorded in storage that if the action fails, the next invocation will retrieve from the same index, thus no events are lost.

In order to demo how to using journaling API to consume events, we provide an end to end solution in this codelab, 
- Event provider - we need to create an event provider to automatically generate events sending to Jouranling API or if you already have event provider you could skip this step
- Event consumer - which is the main demo part of this codelab, we create another Project Firefly headless app to create cron jobs with alarms, we set up recurring jobs to pull from journalling API every x mins and write into project firefly storage.

Event provider and event consumer both need to be deployed as a Project Firefly app under different namespace to make sure end to end workflow.
So for that purpose, you may need to create two projects at Console follow below:
[Creating your First Project Firefly Application](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md)

If successfully set up, you should be able to see your event consumer will periodically pull events from journaling API and write into storage.
For your convenience, we provide a complete solution of this codelab at [here](https://github.com/AdobeDocs/adobeio-samples-journaling-events)

Next: [Requirements](/lessons/requirements.md).
  
