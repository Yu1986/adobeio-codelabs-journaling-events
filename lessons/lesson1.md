## Lesson 1: Create an Event Provider using Firefly

In this lesson, we will do the follow steps:
- Create an event provider using Project Firefly template
- Register the App as event provider 
- Fire Events
- Scheduling cron jobs with alarms

### Create an event provider using Project Firefly template
In this codelab, to provide an end to end solution, we need to have an event provider generating tons of events sending to journaling API, and the events provider need to be configurable to send x events/min to help user to test. so we choose to use OpenWhisk Alarms Package in Fierfly application to create 
cron jobs. 

First, let's create a new firefly App from template by follow the below codelab:
[here](https://adobeio-codelabs-custom-events-adobedocs.project-helix.page/?src=/lessons/lesson1.html)
please make sure you add `I/O management API` in console and choose `publish-event` in the cli template. 


### Register the App as Event Provider
Now we use cli to register the app as event provider, we need to install the Adobe I/O event ClI plugin, simply run below:
```bash
npm install -g @adobe/aio-cli-plugin-events
``` 
and then follow below codelab step by step:
[here](https://adobeio-codelabs-custom-events-adobedocs.project-helix.page/?src=/lessons/lesson2.html)

### Fire Events and set up consume Events 
Now we can set up fire event by follow [this](https://adobeio-codelabs-custom-events-adobedocs.project-helix.page/?src=/lessons/lesson3.html) and make sure that you choose journaling API as the way to consume events by follow [this](https://adobeio-codelabs-custom-events-adobedocs.project-helix.page/?src=/lessons/lesson4.html)

### Scheduling cron jobs with alarms
Follow this codelab to make the firing event automatically by using runtime alarms package [this](https://adobeio-codelabs-alarms-adobedocs.project-helix.page/?src=/README.html)

Your manifest file should look the same as below.
```bash
packages:
  __APP_PACKAGE__:
    license: Apache-2.0
    actions:
      publish-events:
        function: actions/publish-events/index.js
        runtime: 'nodejs:12'
        inputs:
          LOG_LEVEL: debug
          apiKey: $SERVICE_API_KEY
          providerId: $PROVIDER_ID
          eventCode: $EVENT_CODE
          client_id: $CLIENT_ID
          client_secret: $CLIENT_SECRET
          technical_account_email: $TECH_ACCOUNT_EMAIL
          technical_account_id: $TECH_ACCOUNT_ID
          ims_org_id: $IMS_ORG_ID
          private_key: $PRIVATE_KEY
        annotations:
          final: true
    triggers:
      everyMin:
        feed: /whisk.system/alarms/interval
        inputs:
          minutes: 1
    rules:
      everyMinRule:
        trigger: everyMin
        action: publish-events
```

In order to test the action, you could execute `aio app deploy` in the VSCode terminal. Once the deployment is finished, run `aio rt action invoke your-app-name/generic`, and then verify its result and logs using `aio rt activation get ID` and `aio rt activation logs ID`

If successful, the event provider should automatically send the events, you should be able to use postman or curl to verify the journaling API to receive the event. 

Next lesson: [lesson2](lesson2.md)