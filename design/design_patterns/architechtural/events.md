# Introduction

## Publisher - Subscriber Model

The event publisher subscriber model is a design pattern used in software development where there are two main components: publishers and subscribers. The publishers generate events or notifications, and the subscribers receive and process them.

In this model, the publisher and the subscriber have no direct connection. Instead, a message broker, such as a bus or queue, is used to transmit messages between the publisher and the subscriber. Publishers publish events to the broker, which then dispatches them to all subscribers interested in consuming that event. Subscribers may register for specific types of events, and only receive notifications for those events.

The main advantage of the publisher subscriber model is that it decouples the sender and receiver of messages, making them more independent from each other. This allows for the implementation of scalable and extensible systems, as new publishers and subscribers can be easily added without affecting existing components.
