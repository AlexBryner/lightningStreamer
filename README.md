# Deprecated.  Archived.

## The new lightning:empApi (winter19 release) is the best way to stream events within Lightning Experience and Mobile, but is not yet supported in communities.









---

LightningStreamer

1. gets a sessionId via apex
2. subscribes to a push topic or platform event that you set as an attribute
3. listens for messages, and emits the messages uncensored as a lightning standard *application* event
4. Then your other components listen for that event

### Setup

* Install
* create a push topic or platform event (google if you don't know how)
* use in another component or in your app like this

```
<c:Streamer topic="someTopicYouMade"/>
```

or

```
<c:Streamer platformEvent="My_Event__e"/>
```

other components should listen thusly:

```
<aura:handler event="ltng:sendMessage" action="{!c.doSomething}"/>

```
in the controller handler function:

```
var message = event.getParam("message");
var channel = event.getParam("channel"); //channel = 'streamingAPISubscriber'
```

the message is the typical streaming api message: message.data.sobject (streaming topic) or message.data.payload (events)


### Philosopy
Streamer is very stupid, it just listens and repeats everthing it hears--no traffic control or directed communications.

It's the job of the other components to handle all messages, deciding what they should do with them, if anything.

<a href="https://githubsfdeploy.herokuapp.com?owner=mshanemc&repo=LightningStreamer">
  <img alt="Deploy to Salesforce"
       src="https://raw.githubusercontent.com/afawcett/githubsfdeploy/master/deploy.png"/>
</a>
