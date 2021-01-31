## Lesson 3: End to end test
In the previous lessons, we have setup two firefly apps:
- Event provider that automatically generating events 
- Event consumer that automatically pulling from journaling api and write to firefly storage

Let’s first set in `manifest.yml` and try the `/whisk.system/alarms/interval` feed of the OpenWhisk Alarm Package to fire trigger events on an interval base schedule. To see the effect instantly, we will make it run every minute. You will need a trigger set up with the `/whisk.system/alarms/interval` feed, and a rule to wire this trigger to the `publish-event` or `consume-event` action created earlier.

The only required param for the `interval` feed is `minutes`, which is an integer representing the length of the interval (in minutes) between trigger fires. Optional params are `trigger_payload`, `startDate` and `stopDate`.

Now we deployed these two apps seperately in different namespaces, we can configure these two apps at different paces to trigger. if succesful, the events will be stored in the firefly database. 


Next lesson: [Well done](welldone.md)