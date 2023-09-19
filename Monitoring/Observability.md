## Observability
Observability is the ability to collect data about programs' execution, modules' internal states, and the communication among components. In other words it means how well you can understand about what is going on internally in a system based on the outputs of the system.

## MELT
Observability is made up of datatypes that are necessary to understand the performance and health of the application.  
These datatypes are:
* Metrics
* Events 
* Logs 
* Traces

### Metrics
Metrics are measurements collected at regular intervals that must have timestamp, name, one or more numeric values and a count of how many events are represented. These include error rate, response time, and output.

### Event 
An event is a discrete action happening at any moment of the application runtime, where adding metadata to the event allows for very powerful insight on how the system is working, like the payment method when a purchase is done.

### Logs
Exports detailed data and detailed context about what  happened in an event.

### Traces 
Traces follow request from the initial request to the returned output, it records the chain of events to determine relationships between different entities. Traces are very important for highlighting inefficiencies, bottlenecks and roadblocks in the user experience.


# Tracing
## Context 
The metadata that an event will output is called context, context is divided into two types, **span context** and **correlation context**. 

Span Context represents the data required for moving trace information across boundaries it contains:
* Trace ID
* Span ID
* Trace Flags
* Trace State

Correlation Context represents user defined properties that gives application specific performance insights such as:
* Customer ID
* Host Name
* Region

## Propagation 
Is the metric that allows bundling of the context and transferring it across services.
