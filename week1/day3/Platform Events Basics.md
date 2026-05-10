### Learning Objective 

## Define a platform event 

Platform events are custom notifications used to communicate between the salesforce and external Systems.They end in __e and are used to send messages between systems. They cannot be edited, deleted, or viewed in the UI.

## Describe how platform event messages can be published in Apex.

Events are published using the EventBus.publish() method. It is asynchronous; the method returns a Database.SaveResult to confirm if the event was successfully queued, but it does not throw exceptions if the publish fails.

## Use an Apex method to publish an event.

// Instantiate

Cloud_News__e news = new Cloud_News__e(Location__c='NYC', Urgent__c=true);

// Publish

Database.SaveResult sr = EventBus.publish(news);

// Check success

if (sr.isSuccess()) { 

  System.debug('Event published'); 
  
}

## Publish an event using clicks in a process or flow.

Use the Create Records element in Flow Builder. Select your platform event (e.g., Order_event__e) as the object and map the fields. "Creating" the record triggers the publication.

## Publish an event using REST API by inserting an sObject.

External systems can publish events by treating the event like a standard Salesforce object and performing an Insert.
**Endpoint:** /services/data/v60.0/sobjects/Order_Event__e/

**HTTP Method:** POST

**Header:** Authorization: Bearer <Your_Access_Token>

**Content-Type:** application/json

**Request Body Example:**
code
**JSON**
{
   "Order_Number__c" : "ABC-789",
   "Has_Shipped__c" : true
}

**Success Response (Status 201 Created):**
code
**JSON**
{
  "id" : "e00xx0000000001AAA",
  "success" : true,
  "errors" : [
       {
            "statusCode": "OPERATION ENQUEUED",
            "message": "unique-guid-id-here",
            "fields": []
       }
   ]
}
